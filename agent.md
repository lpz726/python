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
