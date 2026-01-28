## data preparation
```python
class DataPreparationModule:
    """数据准备模块 - 负责数据加载、清洗和预处理"""

    def __init__(self, data_path: str):
        self.data_path = data_path
        self.documents: List[Document] = []  # 父文档（完整食谱）
        self.chunks: List[Document] = []     # 子文档（按标题分割的小块）
        self.parent_child_map: Dict[str, str] = {}  # 子块ID -> 父文档ID的映射
```
documents: 存储完整的菜谱文档（父文档）    
chunks: 存储按标题分割的小块（子文档）    
parent_child_map: 维护父子关系映射 

```python
def load_documents(self) -> List[Document]:
    """加载文档数据"""
    documents = []
    data_path_obj = Path(self.data_path)
```
为什么用 **Path**      
pathlib.Path 是 跨平台、可组合、可递归 的路径抽象,企业级系统中，禁止硬编码字符串路径        

```python
for md_file in data_path_obj.rglob("*.md"):
```
rglob = recursive glob  
自动扫描所有子目录

<img width="989" height="799" alt="image" src="https://github.com/user-attachments/assets/18707bb9-68c2-4b9a-bf02-ee4cfeb17b5b" />

```python
from pathlib import Path

# 示例目录结构：
# data/
#   ├── doc1.md
#   ├── subdir/
#   │   ├── doc2.md
#   │   └── nested/
#   │       └── doc3.md
#   └── doc4.txt

data_path_obj = Path("./data")

# 遍历所有.md文件
for md_file in data_path_obj.rglob("*.md"):
    print(md_file)  # 输出: data/doc1.md, data/subdir/doc2.md, data/subdir/nested/doc3.md
    print(md_file.name)  # 文件名: doc1.md, doc2.md, doc3.md
    print(md_file.parent)  # 父目录: data, data/subdir, data/subdir/nested
```



```python

with open(md_file, 'r', encoding='utf-8') as f:
    content = f.read()
```
### with open(...) as f:
**with** 语句：上下文管理器，确保文件在使用后正确关闭，即使发生异常          
**open()**：Python 内置函数，用于打开文件        
**md_file**要打开的文件路径（字符串变量）      
**'r'**：打开模式，r 表示只读（read）        
**encoding='utf-8'**：指定使用 UTF-8 编码读取文件，正确处理中文等非 ASCII 字符      
**as f**：将打开的文件对象赋值给变量 f        

### content = f.read()    
f.read()：读取文件的全部内容      
将读取的内容赋值给变量 content

### 其他常见的文件打开模式    
```python
'w'  # 写入（会覆盖原有内容）    
'a'  # 追加（在文件末尾添加）    
'rb' # 二进制读取    
'wb' # 二进制写入      
```
```python

data_root = Path(self.data_path).resolve()

```
把你传入的 **data_path**：        
转成 Path 对象            
再转成规范的绝对路径            
**resolve()** 的作用            
转为绝对路径        
消除 . / ..            
解析符号链接（如果存在）            

```python

Path(md_file).resolve().relative_to(data_root).as_posix()

```
从 md_file 的绝对路径中，去掉 data_root 这一段前缀                
as_posix() 将路径全部转换成POSIX风格的字符串            

```python
try:
    A
    B
    C
except Exception:
    D
E
```
先执行 A → B → C            
如果中途任何一行抛异常：            
立即跳到 except        
执行 D                    
try 成功 or except 执行完        
继续执行 E            

```python

parent_id = hashlib.md5(relative_path.encode("utf-8")).hexdigest()

```

对“相对路径字符串”进行 UTF-8 编码，然后计算其 MD5 哈希值，并用 32 位十六进制字符串作为父文档的唯一 ID。

为什么使用MD5
| 需求           | MD5 是否满足 |
| ------------ | -------- |
| 同一文件 ID 稳定   | ✅        |
| 跨机器、跨系统      | ✅        |
| 输入短 → 输出固定长度 | ✅        |
| 计算速度快        | ✅        |
| 易存储（字符串）     | ✅        |

[详情](https://chatgpt.com/s/t_6979697e530c8191b6eab5ffcce5127d)


```python
doc = Document(
    page_content=content,
    metadata={
        "source": str(md_file),
        "parent_id": parent_id,
        "doc_type": "parent"  # 标记为父文档
    }
)
documents.append(doc)
```
把一个 Markdown 文件，封装成一个 LangChain 的 Document 对象，作为“父文档”，并加入待处理文档列表。

Document 不是普通类
```python
from langchain_core.documents import Document
```
Document 是 LangChain 中的统一文档数据结构，它的设计目标是：            
把 文本内容（用于 LLM / embedding）            
和 结构化元数据（用于检索 / 过滤 / 关联）                

Document 的两个核心字段
```python
Document(
    page_content: str,
    metadata: dict
)
```
|字段|	作用|
|----|-----|
|page_content|	真正要被模型“读”的文本|
|metadata|	模型不直接读，但系统逻辑要用的信息

metadata={...}（核心设计）        
metadata 是什么？                
                                                            
👉 不参与向量计算，但参与检索 / 管理 / 关联      
```python
"source": str(md_file)
```
记录原始文件路径用于：            
日志    
调试    
回溯来源            
错误定位            
为什么 str(md_file)？        
md_file 是 Path 对象,metadata 通常要求 JSON 可序列化        
Path 不能直接 JSON 序列化           

<img width="1231" height="910" alt="image" src="https://github.com/user-attachments/assets/3ad35b41-2065-4e3e-8a08-426303ed3109" />            

<img width="1345" height="784" alt="image" src="https://github.com/user-attachments/assets/07bbd086-831c-420a-b2b3-ed9195657cce" />            

<img width="1270" height="521" alt="image" src="https://github.com/user-attachments/assets/70de0824-e773-4eb5-9f22-291ccef970a8" />                        

它放进整个 load_documents() 的流程里看              
```txt
md 文件
  ↓
读取文本 content
  ↓
计算 relative_path
  ↓
计算 parent_id
  ↓
封装成 Document(page_content, metadata)
  ↓
加入 documents 列表

```


一个完整的 Document 实例长什么样？        
```python
Document(
    page_content="# 宫保鸡丁\n\n## 原料\n...",
    metadata={
        "source": "data/recipes/meat_dish/kongpao.md",
        "parent_id": "9f0b2c2a2f7e4e3a8f7f0a2e0d9c6b12",
        "doc_type": "parent",
        "category": "荤菜",
        "dish_name": "kongpao",
        "difficulty": "中等"
    }
)
```

```python
except Exception as e:
    logger.warning(f"读取文件 {md_file} 失败: {e}")
```
当 try 块中读取或处理某个 Markdown 文件出错时，捕获异常、记录警告日志，但不中断整个程序流程。

<img width="789" height="648" alt="image" src="https://github.com/user-attachments/assets/55a602be-3bea-482c-ada7-cecbe061dfeb" />            

e 里面包含：        
异常类型    
错误信息        
有时还有系统错误码        

<img width="1374" height="1121" alt="image" src="https://github.com/user-attachments/assets/90ca127c-bf7c-422f-9ff0-e8b8062f6740" />            

```python
for doc in documents:
    self._enhance_metadata(doc)

```
遍历所有已加载的 Document，对每一个文档调用一个内部方法，补充 / 规范 / 推导它的 metadata。            
换句话说：                
“原始文档 → 结构化、可检索、可过滤的文档”                

<img width="1269" height="875" alt="image" src="https://github.com/user-attachments/assets/581cc3c2-11ef-4a43-9524-5695163fd818" />        
<img width="734" height="462" alt="image" src="https://github.com/user-attachments/assets/e363fd6d-dda3-4eca-a409-2cffda427675" />            








