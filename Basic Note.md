# python
python learning
## 目录
[特征对比表](#特征对比表)
[高级函数](#高级函数)
[自定义高阶函数](#自定义高阶函数)
[装饰器](装饰器)
[类](#类)
[嵌套](#嵌套列表)
[工具模块](#工具模块)
[拷贝](#拷贝)
[锁](#锁的详细解释)
[面对对象编程](#面对对象编程)
[抽象类](#抽象类)
[Linux操作指令](#操作指令)
[Linux用户管理](#用户管理)
[Linux文件系统](#文件系统)
[前端](#Web)
[关系数据库](#关系型数据库概述)

## 易错语法        
列表是可变对象，不能作为字典的键（可以转换成元组，或者int，string等数据类型）

## 特性对比表
| 特性  	|列表(List)|	元组(Tuple)|	字典(Dict)|集合(Set)|	类(Class)|
| ------- | ------------|------------|------------|------------|------|
|可变性|	可变	|不可变	|可变|可变（只可以添加）	|可变（实例属性）
|有序性	|有序|	有序	|有序（3.7+）|无序	|属性无序|
|索引方式|	数字索引	|数字索引	|键索引	|无索引|属性名|
|内存效率	|较低	|较高|	中等|	|取决于实现|
|查找速度	|O(n)	|O(n)|	O(1)平均|	|O(1)属性访问|
|使用场景	|同构数据集合|	异构数据记录	|键值映射|	|复杂数据结构|
|哈希性	|不可哈希	|可哈希（元素也需可哈希）|	不可哈希| |自定义|
|构造函数|list()|tuple()|dict()|set()||
|添加|list.append(add),list.insert(num,add)||dic.update()
|删除|list.pop(num or del),list.remove(del)，del list[num]| |dic.pop(),del dic[]|
|排序|list.sort()|||
|反转|list.reverse()|||
|查找|| | dic.value=dic.get(key)|
>add:代表所添加元素  
>num：代表元素在结构中的位置  
>del：代表删除的元素

取值的用法

<img width="1180" height="586" alt="image" src="https://github.com/user-attachments/assets/8fbbec32-934d-41b8-b64d-56a274aecd90" />

<img width="1190" height="915" alt="image" src="https://github.com/user-attachments/assets/02bfb9f6-8a0a-4bc2-8559-33249800ae8a" />



#### 列表方法
|方法|	描述|
|------|-----|
|append()|	在列表的末尾添加一个元素
clear()|	删除列表中的所有元素
copy()	|返回列表的副本
count()	|返回具有指定值的元素数量
extend()|	将列表元素（或任何可迭代的元素）添加到当前列表的末尾
index()	|返回具有指定值的第一个元素的索引
insert()|	在指定位置添加元素
pop()	|删除指定位置的元素
remove()|	删除具有指定值的项目
reverse()|	颠倒列表顺序
|sort()|	对列表进行排序|
#### 集合方法
|方法|	描述|
|-----|----|
|add()|	向集合添加元素
clear()	|删除集合中的所有元素
copy()	|返回集合的副本
difference()|	返回包含两个或更多集合之间差异的集合
difference_updata()|	删除此集合中也包含在另一个指定集合中的项目
discard()	|删除指定集合
intersection()|	返回为两个其他集合的交集的集合
intersection_update()	|删除此集合中不存在于其他指定集合中的项目
isdisjoint()|	返回两个集合是否有交集
issubset()	|返回另一个集合是否包含此集合
issuperset()|	返回此集合是否包含另一个集合
pop()	|从集合中删除一个元素
remove()|	删除指定元素
symmetric_difference()|	返回具有两组集合的对称差集的集合
symmetric_difference_update()|插入此集合和另一个集合的对称差集
union()	|返回包含集合并集的集合
|update()	|用此集合和其他集合的并集来更新集合

#### 字典方法
|方法|	描述|
|-----|-----|
|clear()	|删除字典中的所有元素
copy()|	返回字典的副本
fromkeys()|	返回拥有指定键和值的字典
get()	|返回指定键的值
items()	|返回包含每个键值对的元组的列表
keys()	|返回包含字典键的列表
pop()	|删除拥有指定键的元素
popitem()	|删除最后插入的键值对
setdefault()|	返回指定键的值。如果该键不存在，则插入具有指定值的键。
update()	|使用指定的键值对字典进行更新
|values()|	返回字典中所有值的列表

### 字符转换

''.join() 将列表中的字符连接成一个字符串        

## 函数   
### 高级函数 

map 函数
>原理：对可迭代对象中的每个元素应用指定函数，返回一个迭代器
```python
# 基本用法
numbers = [1, 2, 3, 4, 5]

# 使用 map 对每个元素求平方
squared = map(lambda x: x ** 2, numbers)
print(list(squared))  # [1, 4, 9, 16, 25]

# 等价于列表推导式
squared_list = [x ** 2 for x in numbers]
print(squared_list)   # [1, 4, 9, 16, 25]

# 多个可迭代对象
nums1 = [1, 2, 3]
nums2 = [4, 5, 6]
sums = map(lambda x, y: x + y, nums1, nums2)
print(list(sums))  # [5, 7, 9]
# 对应位置元素相加
# 使用内置函数
names = ['alice', 'BOB', 'Charlie']
capitalized = map(str.capitalize, names)
print(list(capitalized))  # ['Alice', 'Bob', 'Charlie']
```
filter 函数
>原理：过滤可迭代对象，保留使函数返回 True 的元素
```python
# 基本用法：过滤满足条件的元素
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# 过滤偶数
evens = filter(lambda x: x % 2 == 0, numbers)
print(list(evens))  # [2, 4, 6, 8, 10]

# 过滤非空字符串
words = ['hello', '', 'world', '', 'python', '']
non_empty = filter(None, words)  # None 表示 bool(item)
print(list(non_empty))  # ['hello', 'world', 'python']

# 使用函数对象
def is_positive(n):
    return n > 0

# 过滤特定类型
mixed = [1, 'hello', 3.14, True, [1, 2], {'a': 1}]
ints_only = filter(lambda x: isinstance(x, int), mixed)
print(list(ints_only))  # [1, True]
```
 reduce() 函数
 >原理：对可迭代对象中的元素进行累积计算（需要从 functools 导入）
```python
from functools import reduce

# 基本用法：计算累加
numbers = [1, 2, 3, 4, 5]
sum_result = reduce(lambda x, y: x + y, numbers)
print(sum_result)  # 15

# 计算阶乘
factorial = reduce(lambda x, y: x * y, range(1, 6))
print(factorial)  # 120

# 带初始值
numbers = [1, 2, 3]
result = reduce(lambda x, y: x + y, numbers, 10)
print(result)  # 16 (10 + 1 + 2 + 3)
#执行过程分析：
# reduce(lambda x, y: x + y, [1, 2, 3, 4]) 的执行步骤：
# 步骤1: 1 + 2 = 3
# 步骤2: 3 + 3 = 6  
# 步骤3: 6 + 4 = 10
# 结果: 10
```
sorted() 函数
>原理：对可迭代对象排序，可通过 key 参数指定排序依据
```python
# 基本排序
numbers = [3, 1, 4, 1, 5, 9, 2]
print(sorted(numbers))  # [1, 1, 2, 3, 4, 5, 9]

# 使用 key 参数
words = ['apple', 'banana', 'cherry', 'date']
print(sorted(words, key=len))  # 按长度排序: ['date', 'apple', 'banana', 'cherry']

# 复杂对象排序
students = [
    {'name': 'Alice', 'score': 85},
    {'name': 'Bob', 'score': 92},
    {'name': 'Charlie', 'score': 78}
]

# 按分数排序
by_score = sorted(students, key=lambda s: s['score'])
print(by_score)
# [{'name': 'Charlie', 'score': 78}, {'name': 'Alice', 'score': 85}, {'name': 'Bob', 'score': 92}]
```
### 自定义高阶函数
接受函数作为参数
```python
def apply_operation(data, operation):
    """
    对数据应用操作的高阶函数
    
    参数:
        data: 输入数据
        operation: 操作函数
    """
    return [operation(item) for item in data]

# 使用示例
numbers = [1, 2, 3, 4, 5]

# 应用平方操作
squared = apply_operation(numbers, lambda x: x ** 2)
print(squared)  # [1, 4, 9, 16, 25]

# 应用加倍操作
doubled = apply_operation(numbers, lambda x: x * 2)
print(doubled)  # [2, 4, 6, 8, 10]

# 使用预定义的函数
def increment(x):
    return x + 1

incremented = apply_operation(numbers, increment)
print(incremented)  # [2, 3, 4, 5, 6]
```
返回函数的函数（函数工厂）
```python
def create_multiplier(factor):
    """
    创建乘法器函数
    
    参数:
        factor: 乘数因子
    返回:
        一个乘法函数
    """
    def multiplier(x):
        return x * factor
    return multiplier

# 使用函数工厂
double = create_multiplier(2)
triple = create_multiplier(3)

print(double(5))  # 10
print(triple(5))  # 15
#和嵌套函数类似
# 在 map 中使用
numbers = [1, 2, 3, 4]
double_all = list(map(create_multiplier(2), numbers))
print(double_all)  # [2, 4, 6, 8]
```
装饰器作为高阶函数
```python
def retry(max_attempts=3):
    """
    重试装饰器
    
    参数:
        max_attempts: 最大重试次数
    """
    def decorator(func):
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise e
                    print(f"尝试 {attempt + 1} 失败，重试...")
            return None
        return wrapper
    return decorator
'''
三层嵌套函数的角色
retry(max_attempts=3) → 返回 decorator 函数
decorator(func) → 返回 wrapper 函数  
wrapper(*args, **kwargs) → 实际执行重试逻辑
'''
# 使用装饰器
@retry(max_attempts=3)
def risky_operation():
    import random
    if random.random() < 0.7:  # 70% 概率失败
        raise ValueError("操作失败")
    return "操作成功"

# 测试
result = risky_operation()
print(result)
```
## 装饰器  
概念：装饰器是一种设计模式，允许在不修改原函数代码的情况下，动态地扩展函数的功能。  

```python
def record_time(func):
    
    def wrapper(*args, **kwargs):
        
        result = func(*args, **kwargs)
        
        return result
    
    return wrapper
```
`record_time`函数的参数`func`代表了一个被装饰的函数，函数里面定义的`wrapper`函数是带有装饰功能的函数，它会执行被装饰的函数`func`，它还需要返回在最后产生函数执行的返回值。不知大家是否留意到，上面的代码我在第4行和第6行留下了两个空行，这意味着我们可以这些地方添加代码来实现额外的功能。`record_time`函数最终会返回这个带有装饰功能的函数`wrapper`并通过它替代原函数`func`，当原函数`func`被`record_time`函数装饰后，我们调用它时其实调用的是`wrapper`函数，所以才获得了额外的能力。`wrapper`函数的参数比较特殊，由于我们要用`wrapper`替代原函数`func`，但是我们又不清楚原函数`func`会接受哪些参数，所以我们就通过可变参数和关键字参数照单全收，然后在调用`func`的时候，原封不动的全部给它。这里还要强调一下，Python 语言支持函数的嵌套定义，就像上面，我们可以在`record_time`函数中定义`wrapper`函数，这个操作在很多编程语言中并不被支持。
### example：  
``` python
def record_time(func):  # 接收一个函数作为参数
    def wrapper(*args, **kwargs):  # 内部包装函数，接受任意参数
        start = time.time()  # 记录开始时间
        result = func(*args, **kwargs)  # 执行原函数
        end = time.time()  # 记录结束时间
        print(f'{func.__name__}执行时间: {end - start:.2f}秒')
        return result  # 返回原函数的执行结果
    return wrapper  # 返回包装函数   
@record_time  # 语法糖，相当于 download = record_time(download)
def download(filename):
    print(f'开始下载{filename}.')
    time.sleep(random.random() * 6)  # 模拟下载耗时
    print(f'{filename}下载完成.')
```
```python
# 简单比喻：给函数"穿衣服"
def wear_jacket(func):  # 这件"衣服"就是装饰器
    def dressed_function():
        print("穿上夹克")  # 新增功能
        func()            # 原函数
        print("脱下夹克")  # 新增功能
    return dressed_function
@wear_jacket
def go_out():
    print("出门逛街")
go_out()
# 输出：
# 穿上夹克
# 出门逛街  
# 脱下夹克
```
 装饰器的本质
 ```python
 # 语法糖 @decorator 的实际含义
def decorator(func):
    def wrapper():
        print("装饰器逻辑")
        return func()
    return wrapper

# 方式1：使用@语法糖（推荐）
@decorator
def function():
    print("原函数")

# 方式2：手动装饰（实际执行过程）
def function():
    print("原函数")
function = decorator(function)  # 将function替换为wrapper

# 两种方式完全等价！
```
### 装饰器的实现原理
>基本结构
```python
# 三层嵌套结构
def decorator(func):           # 第一层：接收被装饰函数
    def wrapper(*args, **kwargs):  # 第二层：接收函数参数
        # 前置处理
        result = func(*args, **kwargs)  # 执行原函数
        # 后置处理
        return result
    return wrapper             # 返回包装函数

# 使用
@decorator
def target_function():
    pass
```
### 无参数装饰器（基础版）
```python
def timer(func):
    """计时装饰器"""
    import time    
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"{func.__name__} 执行时间: {end_time - start_time:.4f}秒")
        return result    
    return wrapper
@timer
def slow_function():
    import time
    time.sleep(0.5)
    return "完成"
print(slow_function())
```
### 带参数装饰器（三层嵌套）
```python
def repeat(times):
    """重复执行装饰器"""
    def decorator(func):
        def wrapper(*args, **kwargs):
            results = []
            for i in range(times):
                print(f"第 {i+1} 次执行")
                result = func(*args, **kwargs)
                results.append(result)
            return results
        return wrapper
    return decorator

# 使用带参数装饰器
@repeat(times=3)
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))
# 输出：
# 第 1 次执行
# 第 2 次执行  
# 第 3 次执行
# ['Hello, Alice!', 'Hello, Alice!', 'Hello, Alice!']
```

### wraps函数    
``` python
from functools import wraps  # 导入 wraps 装饰器
def record_time(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)  # 调用原始函数
        end = time.time()
        print(f'执行时间: {end - start:.2f}秒')
        return result
    
    # @wraps 会自动设置 __wrapped__ 属性
    # wrapper.__wrapped__ = func
    return wrapper
# 装饰后：
# download = record_time(original_download)
# download.__wrapped__ == original_download
```
#### functools.wraps 的工作原理：
函数元数据：  
>__name__: 函数名    
__doc__: 文档字符串    
__module__: 模块名    
>__annotations__: 类型注解    

不使用 wraps：    
>函数名变成了 “wrapper”    
文档字符串丢失     
>其他元数据可能不完整     

使用 wraps：     
>保留原始函数名 “say_hello”     
保留原始文档字符串      
>保留其他元数据

example:
```python
# 不使用 wraps 的情况
def simple_decorator(cls):
    def wrapper(*args, **kwargs):
        return cls(*args, **kwargs)
    return wrapper

@simple_decorator
class MyClass:
    """我的类"""
    pass

print(MyClass.__name__)   # 输出: wrapper（不是 MyClass）
print(MyClass.__doc__)    # 输出: None（丢失了文档字符串）

# 使用 wraps 的情况
def better_decorator(cls):
    @wraps(cls)
    def wrapper(*args, **kwargs):
        return cls(*args, **kwargs)
    return wrapper

@better_decorator
class MyClass2:
    """我的类2"""
    pass

print(MyClass2.__name__)  # 输出: MyClass2
print(MyClass2.__doc__)   # 输出: 我的类2
```
详细的解答[wraps](https://blog.csdn.net/weixin_44705554/article/details/145440001?ops_request_misc=elastic_search_misc&request_id=3ed4841d1c829e84b2c64fd90f515688&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-145440001-null-null.142^v102^pc_search_result_base9&utm_term=python%E8%A3%85%E9%A5%B0%E5%99%A8&spm=1018.2226.3001.4187)    

由于对带装饰功能的函数添加了@wraps装饰器，可以通过func.__wrapped__方式获得被装饰之前的函数或类来取消装饰器的作用。
### 装饰器堆叠
```python
def decorator1(func):
    print("装饰器1执行")
    def wrapper():
        print("装饰器1前")
        result = func()
        print("装饰器1后")
        return result
    return wrapper

def decorator2(func):
    print("装饰器2执行")
    def wrapper():
        print("装饰器2前")
        result = func()
        print("装饰器2后")
        return result
    return wrapper

def decorator3(func):
    print("装饰器3执行")
    def wrapper():
        print("装饰器3前")
        result = func()
        print("装饰器3后")
        return result
    return wrapper

@decorator1
@decorator2
@decorator3
def target_function():
    print("目标函数")
    return "完成"

print("开始调用...")
result = target_function()
print(f"结果: {result}")
# @decorator1
# @decorator2  
# @decorator3
# def target_function():
#     pass

# 等价于：
# target_function = decorator1(decorator2(decorator3(target_function)))

# 执行顺序：
# 1. 先装饰：decorator3 → decorator2 → decorator1（由内向外）
# 2. 后执行：wrapper1 → wrapper2 → wrapper3 → 原函数 → wrapper3后 → wrapper2后 → wrapper1后（由外向内的前部，然后原函数，再由内向外的后部）
```
## 类   
### 可见性和属性装饰器   
```python
class Student:

    def __init__(self, name, age):
        self.__name = name
        self.__age = age
#__name表示一个私有属性，_name表示一个受保护
#private 类内部使用，避免被外部或子类意外修改
#子类可用，不建议外部访问
    def study(self, course_name):
        print(f'{self.__name}正在学习{course_name}.')


stu = Student('王大锤', 20)
stu.study('Python程序设计')
print(stu.__name)  # AttributeError: 'Student' object has no attribute '__name'
```
### 动态属性   
```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age


stu = Student('王大锤', 20)
stu.sex = '男'  # 给学生对象动态添加sex属性
#如果不希望在使用对象时动态的为对象添加属性，可以使用 Python 语言中的__slots__
class Student:
    __slots__ = ('name', 'age')

    def __init__(self, name, age):
        self.name = name
        self.age = age


stu = Student('王大锤', 20)
# AttributeError: 'Student' object has no attribute 'sex'
stu.sex = '男'
```
### 静态方法和类方法
```python
class Triangle(object):
    """三角形"""

    def __init__(self, a, b, c):
        """初始化方法"""
        self.a = a
        self.b = b
        self.c = c

    @staticmethod
    def is_valid(a, b, c):
        """判断三条边长能否构成三角形(静态方法)"""
        return a + b > c and b + c > a and a + c > b

    @property
    def perimeter(self):
        """计算周长"""
        return self.a + self.b + self.c

    @property
    def area(self):
        """计算面积"""
        p = self.perimeter / 2
        return (p * (p - self.a) * (p - self.b) * (p - self.c)) ** 0.5


t = Triangle(3, 4, 5)
print(f'周长: {t.perimeter}')
print(f'面积: {t.area}')
```
| 特性 | 实例方法 | 类方法（@classmethod） | 静态方法（@staticmethod） |
|------|----------|------------------------|---------------------------|
| 第一个参数 | self（实例本身） | cls（类本身） | 无特殊参数 |
| 调用方式 | 实例.方法() | 类.方法() 或 实例.方法() | 类.方法() 或 实例.方法() |
| 访问实例属性 | √ 可以 | X 不能 | X 不能 |
| 访问类属性 | 通过 self.__class__ 或类名 | √ 通过 cls | 通过类名 |
| 修改类状态 | 可以，但不直接 | √ 可以 | X 不能 |
| 多态性 | √ 支持 | √ 支持（通过 cls） | X 不支持 |
#### example:
>类方法
```python
class Example:
    class_var = "类变量"
    
    def __init__(self):
        self.instance_var = "实例变量"
    @staticmethod
    def static_method():
        # 不能直接访问实例属性
        # print(self.instance_var)  # ❌ 错误：没有self
        # 可以访问类属性，但需要通过类名
        print(Example.class_var)   # ✓ 可以
        return "静态方法"
    
    # 带参数的静态方法
    @staticmethod
    def calculate(operation, a, b):
        if operation == "add":
            return a + b
        elif operation == "subtract":
            return a - b
        else:
            return None
```
### 继承和多态
```python
class Person:
    """人"""

    def __init__(self, name, age):
        self.name = name
        self.age = age
    3
    def eat(self):
        print(f'{self.name}正在吃饭.')
    
    def sleep(self):
        print(f'{self.name}正在睡觉.')
class Student(Person):
    """学生"""
    
    def __init__(self, name, age):
        super().__init__(name, age)
    
    def study(self, course_name):
        print(f'{self.name}正在学习{course_name}.')
class Teacher(Person):
    """老师"""
    def __init__(self, name, age, title):
        super().__init__(name, age)
        self.title = title
    def teach(self, course_name):
        print(f'{self.name}{self.title}正在讲授{course_name}.')
stu1 = Student('白元芳', 21)
stu2 = Student('狄仁杰', 22)
tea1 = Teacher('武则天', 35, '副教授')
stu1.eat()
stu2.sleep()
tea1.eat()
stu1.study('Python程序设计')
tea1.teach('Python程序设计')
stu2.study('数据科学导论')
```
>super().__init__()来调用父类初始化方法，super函数是 Python 内置函数中专门为获取当前对象的父类对象而设计的。从上面的代码可以看出，子类除了可以通过继承得到父类提供的属性和方法外，还可以定义自己特有的属性和方法，所以子类比父类拥有的更多的能力。在实际开发中，我们经常会用子类对象去替换掉一个父类对象，这是面向对象编程中一个常见的行为，也叫做“里氏替换原则”（Liskov Substitution Principle）。
## 生成式
```python
prices = {
    'AAPL': 191.88,
    'GOOG': 1186.96,
    'IBM': 149.24,
    'ORCL': 48.44,
    'ACN': 166.89,
    'FB': 208.09,
    'SYMC': 21.29
}
# 用股票价格大于100元的股票构造一个新的字典
prices2 = {key: value for key, value in prices.items() if value > 100}
print(prices2)
```
## 嵌套列表
语法
```python
# 正确方式 - 创建独立的列表
scores = [[None] * len(courses) for _ in range(len(names))]
#分解理解
# 1. [None] * len(courses) = [None] * 3 = [None, None, None]
# 2. for _ in range(len(names)) = for _ in range(5)
# 3. 每次循环都创建一个新的 [None, None, None]
# 4. 结果是5个独立的列表

# 相当于：
scores = []
for i in range(5):
    row = [None, None, None]  # 每次都新建一个列表
    scores.append(row)
```
## [Python Tutor](http://pythontutor.com/) - VISUALIZE CODE AND GET LIVE HELP
## 工具模块
>heapq模块（堆排序）
### 什么是堆（Heap）？  
堆是一种特殊的完全二叉树，满足以下性质：   
最小堆：每个节点的值都 ≤ 其子节点的值（根节点最小）
最大堆：每个节点的值都 ≥ 其子节点的值（根节点最大）
>Python 的 heapq 模块实现的是最小堆。
```python
import heapq

# 示例数据
list1 = [34, 25, 12, 99, 87, 63, 58, 78, 88, 92]

# 1. 找出最大的3个元素
print(heapq.nlargest(3, list1))  # 输出: [99, 92, 88]

# 2. 找出最小的3个元素
print(heapq.nsmallest(3, list1))  # 输出: [12, 25, 34]

# 复杂数据结构
list2 = [
    {'name': 'IBM', 'shares': 100, 'price': 91.1},
    {'name': 'AAPL', 'shares': 50, 'price': 543.22},
    {'name': 'FB', 'shares': 200, 'price': 21.09},
    {'name': 'HPQ', 'shares': 35, 'price': 31.75},
    {'name': 'YHOO', 'shares': 45, 'price': 16.35},
    {'name': 'ACME', 'shares': 75, 'price': 115.65}
]

# 3. 找出价格最高的2只股票
print(heapq.nlargest(2, list2, key=lambda x: x['price']))
# 输出: [{'name': 'AAPL', 'shares': 50, 'price': 543.22},
#        {'name': 'ACME', 'shares': 75, 'price': 115.65}]

# 4. 找出份额最高的2只股票
print(heapq.nlargest(2, list2, key=lambda x: x['shares']))
# 输出: [{'name': 'FB', 'shares': 200, 'price': 21.09},
#        {'name': 'IBM', 'shares': 100, 'price': 91.1}]

#heapify() - 将列表转为堆
# 创建一个普通列表
nums = [3, 1, 4, 1, 5, 9, 2, 6, 5]
print("原始列表:", nums)  # [3, 1, 4, 1, 5, 9, 2, 6, 5]
# 转换为堆（原地修改）
heapq.heapify(nums)
print("堆化后:", nums)  # [1, 1, 2, 3, 5, 9, 4, 6, 5]
# 注意：堆不是完全排序的，但保证第一个元素最小

# 验证堆性质
print("最小元素:", nums[0])  # 1

#heappush() - 添加元素到堆
# 创建一个空堆（用普通列表）
heap = []
# 添加元素
heapq.heappush(heap, 5)
heapq.heappush(heap, 2)
heapq.heappush(heap, 9)
heapq.heappush(heap, 1)
heapq.heappush(heap, 6)

print("堆:", heap)  # [1, 2, 9, 5, 6]
print("堆顶元素（最小）:", heap[0])  # 1

#heappop() - 弹出最小元素
heap = [1, 2, 9, 5, 6]
# 弹出最小元素
min_element = heapq.heappop(heap)
print("弹出的最小元素:", min_element)  # 1
print("弹出后的堆:", heap)  # [2, 5, 9, 6]

#heapreplace() - 弹出最小并添加新元素
heap = [1, 3, 5, 7, 9]
heapq.heapify(heap)
# 弹出最小元素，同时插入新元素
old_min = heapq.heapreplace(heap, 4)
print("被替换的最小元素:", old_min)  # 1
print("替换后的堆:", heap)  # [3, 4, 5, 7, 9]

# heappushpop() - 先添加再弹出
heap = [2, 5, 8]
heapq.heapify(heap)
# 先添加3，然后弹出最小元素
result = heapq.heappushpop(heap, 3)
print("弹出的元素:", result)  # 2（原本的最小值）
print("操作后的堆:", heap)  # [3, 5, 8]

# 对比heapreplace：如果新元素比堆顶大，heappushpop效率更高

#实现最大堆
class MaxHeap:
    """通过取反实现最大堆"""
    def __init__(self):
        self.heap = []
    def push(self, value):
        heapq.heappush(self.heap, -value)  # 存负值
    def pop(self):
        return -heapq.heappop(self.heap)  # 取负值恢复
    def peek(self):
        return -self.heap[0] if self.heap else None    
    def __len__(self):
        return len(self.heap)
# 测试最大堆
max_heap = MaxHeap()
for num in [3, 1, 4, 1, 5, 9]:
    max_heap.push(num)
print("最大堆内容（从大到小弹出）:")
while len(max_heap) > 0:
    print(max_heap.pop(), end=" ")  # 9 5 4 3 1 1
```
### itertools模块
```python
"""
迭代工具模块
"""
import itertools

# 产生ABCD的全排列
itertools.permutations('ABCD')
# 产生ABCDE的五选三组合
itertools.combinations('ABCDE', 3)
# 产生ABCD和123的笛卡尔积
itertools.product('ABCD', '123')
# 产生ABC的无限循环序列
itertools.cycle(('A', 'B', 'C'))
```
### collections模块
>常用的工具类：   
> - namedtuple：命令元组，它是一个类工厂，接受类型的名称和属性列表来创建一个类。    
> - deque：双端队列，是列表的替代实现。Python中的列表底层是基于数组来实现的，而deque底层是双向链表，因此当你需要在头尾添加和删除元素时，deque会表现出更好的性能，渐近时间复杂度为$O(1)$。    
> - Counter：dict的子类，键是元素，值是元素的计数，它的most_common()方法可以帮助我们获取出现频率最高的元素。Counter和dict的继承关系我认为是值得商榷的，按照CARP原则，Counter跟dict的关系应该设计为关联关系更为合理。   
> - OrderedDict：dict的子类，它记录了键值对插入的顺序，看起来既有字典的行为，也有链表的行为。    
> - defaultdict：类似于字典类型，但是可以通过默认的工厂函数来获得键对应的默认值，相比字典中的setdefault()方法，这种做法更加高效。  
>example
```python
"""
找出序列中出现次数最多的元素
"""
from collections import Counter
words = [
    'look', 'into', 'my', 'eyes', 'look', 'into', 'my', 'eyes',
    'the', 'eyes', 'the', 'eyes', 'the', 'eyes', 'not', 'around',
    'the', 'eyes', "don't", 'look', 'around', 'the', 'eyes',
    'look', 'into', 'my', 'eyes', "you're", 'under'
]
counter = Counter(words)
print(counter.most_common(3))
```
## 拷贝
[ : ] - 切片创建浅拷贝
```python
original = [1, 2, 3, [4, 5]]

# 切片操作创建新列表
copy1 = original[:]       # 完整切片，等价于 [0:len(original)]
copy2 = original[1:3]     # 部分切片 [2, 3]

print("original id:", id(original))  # 原列表的id
print("copy1 id:", id(copy1))        # 新列表的id，不同！
print("copy2 id:", id(copy2))        # 另一个新列表的id

print("original == copy1:", original == copy1)  # True（值相等）
print("original is copy1:", original is copy1)  # False（不是同一个对象）
```
切片操作特性：
>创建新的列表对象   
>但只拷贝一层（浅拷贝）   
>对嵌套结构，内部对象仍然是引用


浅拷贝 vs 深拷贝
```python
import copy

# 原始数据结构（包含嵌套）
original = [1, 2, [3, 4], {'a': 5}]

# 1. 直接赋值（引用）
reference = original
reference[0] = 100
print("直接赋值后 original[0]:", original[0])  # 100（被修改）

# 重置
original = [1, 2, [3, 4], {'a': 5}]
# 2. 浅拷贝（list() 或 [:]）
shallow_copy = list(original)[:]
shallow_copy[0] = 100  # 修改第一层
shallow_copy[2][0] = 300  # 修改嵌套列表
print("\n浅拷贝后:")
print("original:", original)       # [1, 2, [300, 4], {'a': 5}]
print("shallow_copy:", shallow_copy) # [100, 2, [300, 4], {'a': 5}]
# 注意：嵌套列表被修改了！
# 重置
original = [1, 2, [3, 4], {'a': 5}]
# 3. 深拷贝
deep_copy = copy.deepcopy(original)
deep_copy[0] = 100
deep_copy[2][0] = 300
print("\n深拷贝后:")
print("original:", original)       # [1, 2, [3, 4], {'a': 5}]（不变）
print("deep_copy:", deep_copy)     # [100, 2, [300, 4], {'a': 5}]
```
## 字典推导式语法总结
##### {key_expression: value_expression for item in iterable if condition}
### example:
##### prices2 = {key: value for key, value in prices.items() if value > 100}
>**分解说明：**  
>> prices.items(): 返回字典中所有键值对的视图  
for key, value in prices.items(): 遍历每个股票代码和价格  
if value > 100: 筛选条件，只保留价格大于100的股票  
key: value: 保留原始的键值对结构  

## 线程安全的单例装饰器
 单例模式：确保一个类只有一个实例，并提供一个全局访问点。
```python
from functools import wraps
from threading import RLock


def singleton(cls):
    """线程安全的单例装饰器"""
    instances = {}
    locker = RLock()

    @wraps(cls)
    def wrapper(*args, **kwargs):
        if cls not in instances:   # 第一次检查（不加锁，快速）
            with locker:           # 获取锁
                if cls not in instances:   # 第二次检查（加锁，确保安全）
                    instances[cls] = cls(*args, **kwargs)  # 创建实例
        return instances[cls]

    return wrapper
```
基本用法
```python
@singleton
class DatabaseConnection:
    def __init__(self, connection_string):
        self.connection_string = connection_string
        print(f"创建数据库连接: {connection_string}")
    
    def query(self, sql):
        return f"执行查询: {sql}"

# 测试
db1 = DatabaseConnection("mysql://localhost:3306/mydb")
db2 = DatabaseConnection("mysql://localhost:3306/otherdb")

print(f"db1 is db2: {db1 is db2}")  # True
print(f"db1.connection_string: {db1.connection_string}")  # mysql://localhost:3306/mydb
print(f"db2.connection_string: {db2.connection_string}")  # mysql://localhost:3306/mydb（相同）
```
### RLock vs Lock
### [锁的详细解释](https://blog.csdn.net/qdPython/article/details/132585697?ops_request_misc=&request_id=&biz_id=102&utm_term=python%E7%9A%84%E9%94%81%E6%9C%89%E4%BB%80%E4%B9%88%E7%94%A8&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-132585697.142^v102^pc_search_result_base9&spm=1018.2226.3001.4187)
```python
from threading import Lock, RLock, Thread
import time

class TestLock:
    def __init__(self):
        self.lock = Lock()
        self.rlock = RLock()
    
    def method_a(self):
        with self.lock:
            print("Lock: 在 method_a 中获取了锁")
            time.sleep(0.1)
            # self.method_b()  # 如果用 Lock，这里会死锁
    
    def method_b(self):
        with self.lock:
            print("Lock: 在 method_b 中获取了锁")
    
    def method_c(self):
        with self.rlock:
            print("RLock: 在 method_c 中获取了锁")
            time.sleep(0.1)
            self.method_d()  # RLock 允许重入，不会死锁
    
    def method_d(self):
        with self.rlock:
            print("RLock: 在 method_d 中获取了锁")

test = TestLock()
# 如果用 Lock，调用 method_a 会尝试获取已经持有的锁，导致死锁
# 用 RLock 则允许同一个线程多次获取锁
```
Lock：标准锁，同一线程不能多次获取，否则会死锁
RLock：可重入锁，同一线程可以多次获取，必须有相同次数的释放
## 面对对象编程
三大支柱：封装、继承、多态
### 抽象类  
抽象类就是对一堆类共同内容的抽取，包括：属性和方法。   
抽象类的特点
> - （1）抽象类必须包含一个或多个抽象方法，也可以包含普通方法。
> - （2）抽象类的抽象方法，在抽象类中并不作实现。
> - （3）抽象类不能被实例化

**抽象类的子类要想进行实例化，必须先实现抽象父类中的所有抽象方法！！！！！！！！！！！！！**
普通父类的示例
```python
# coding:utf-8

# 不是抽象类,是一个普通父类
class Parent(object):
    # 构造方法
    def __init__(self, sex, surname, job):
        self.sex = sex
        self.surname = surname
        self.job = job

    # 已经实现的普通方法
    def run(self):
        print("running...")

    def say(self):
        print("saying...")

    def is_adult(self):
        print("True")
    # 未实现的普通方法
    def hobby(self):
        pass
# 子类
class Son(Parent):
    # 重写
    def is_adult(self):
        print("False")
# 实例化
s = Son(sex="male", surname="Zhang", job="student")
s.is_adult()
s.hobby()

#运行输出 False
```
抽象父类的示例
```python
#coding:utf-8
# 从abc库中导入ABC, abstractmethod模块
from abc import ABC, abstractmethod

# 抽象父类
class Parent(ABC):
    # 构造方法
    def __init__(self, sex, surname, job):
        self.sex = sex
        self.surname = surname
        self.job = job

    # 已经实现的普通方法
    def run(self):
        print("running...")

    def say(self):
        print("saying...")

    def is_adult(self):
        print("True")

    # 抽象方法
    @abstractmethod
    def hobby(self):
        pass

# 子类
class Son(Parent):
    # 重写
    def is_adult(self):
        print("False")


# 实例化
s = Son(sex="male", surname="Zhang", job="student")
s.is_adult()
s.hobby()
#运行发生报错：原因不能实例化带有抽象方法的抽象类son
#修改如下
# 子类
class Son(Parent):
    # 重写
    def is_adult(self):
        print("False")
    # 实现抽象父类的抽象方法
    def hobby(self):
        print("basketball")
#运行结果  False basketball
#子类实现抽象父类中的抽象方法后的输出
```
#### [抽象类详解](https://blog.csdn.net/elon15/article/details/127176217?ops_request_misc=elastic_search_misc&request_id=7b27982cb17299ad09aece63a358d204&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-127176217-null-null.142^v102^pc_search_result_base9&utm_term=python%E6%8A%BD%E8%B1%A1%E7%B1%BB&spm=1018.2226.3001.4187)
example:    
工资结算系统
```python
"""
月薪结算系统 - 部门经理每月15000 程序员每小时200 销售员1800底薪加销售额5%提成
"""
from abc import ABCMeta, abstractmethod


class Employee(metaclass=ABCMeta):
    """员工(抽象类)"""

    def __init__(self, name):
        self.name = name

    @abstractmethod
    def get_salary(self):
        """结算月薪(抽象方法)"""
        pass


class Manager(Employee):
    """部门经理"""

    def get_salary(self):
        return 15000.0


class Programmer(Employee):
    """程序员"""

    def __init__(self, name, working_hour=0):
        self.working_hour = working_hour
        super().__init__(name)

    def get_salary(self):
        return 200.0 * self.working_hour


class Salesman(Employee):
    """销售员"""

    def __init__(self, name, sales=0.0):
        self.sales = sales
        super().__init__(name)

    def get_salary(self):
        return 1800.0 + self.sales * 0.05


class EmployeeFactory:
    """创建员工的工厂（工厂模式 - 通过工厂实现对象使用者和对象之间的解耦合）"""

    @staticmethod
    def create(emp_type, *args, **kwargs):
        """创建员工"""
        all_emp_types = {'M': Manager, 'P': Programmer, 'S': Salesman}
        cls = all_emp_types[emp_type.upper()]
        return cls(*args, **kwargs) if cls else None


def main():
    """主函数"""
    emps = [
        EmployeeFactory.create('M', '曹操'), 
        EmployeeFactory.create('P', '荀彧', 120),
        EmployeeFactory.create('P', '郭嘉', 85), 
        EmployeeFactory.create('S', '典韦', 123000),
    ]
    for emp in emps:
        print(f'{emp.name}: {emp.get_salary():.2f}元')


if __name__ == '__main__':
    main()
```
### 类与类的关系
is-a关系：继承    
has-a关系：关联 / 聚合 / 合成     
use-a关系：依赖   

example
```python
"""
经验：符号常量总是优于字面常量，枚举类型是定义符号常量的最佳选择
"""
from enum import Enum, unique

import random


@unique
class Suite(Enum):
    """花色"""

    SPADE, HEART, CLUB, DIAMOND = range(4)

    def __lt__(self, other):
        return self.value < other.value


class Card:
    """牌"""

    def __init__(self, suite, face):
        """初始化方法"""
        self.suite = suite
        self.face = face

    def show(self):
        """显示牌面"""
        suites = ['♠︎', '♥︎', '♣︎', '♦︎']
        faces = ['', 'A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K']
        return f'{suites[self.suite.value]}{faces[self.face]}'

    def __repr__(self):
        return self.show()


class Poker:
    """扑克"""

    def __init__(self):
        self.index = 0
        self.cards = [Card(suite, face)
                      for suite in Suite
                      for face in range(1, 14)]

    def shuffle(self):
        """洗牌（随机乱序）"""
        random.shuffle(self.cards)
        self.index = 0

    def deal(self):
        """发牌"""
        card = self.cards[self.index]
        self.index += 1
        return card

    @property
    def has_more(self):
        return self.index < len(self.cards)


class Player:
    """玩家"""

    def __init__(self, name):
        self.name = name
        self.cards = []

    def get_one(self, card):
        """摸一张牌"""
        self.cards.append(card)

    def sort(self, comp=lambda card: (card.suite, card.face)):
        """整理手上的牌"""
        self.cards.sort(key=comp)


def main():
    """主函数"""
    poker = Poker()
    poker.shuffle()
    players = [Player('东邪'), Player('西毒'), Player('南帝'), Player('北丐')]
    while poker.has_more:
        for player in players:
                player.get_one(poker.deal())
    for player in players:
        player.sort()
        print(player.name, end=': ')
        print(player.cards)


if __name__ == '__main__':
    main()
```

Python使用了自动化内存管理，这种管理机制以引用计数为基础，同时也引入了标记-清除和分代收集两种机制为辅的策略。

导致引用计数+1的情况：
> - 对象被创建，例如a = 23
> - 对象被引用，例如b = a
> - 对象被作为参数，传入到一个函数中，例如f(a)
> - 对象作为一个元素，存储在容器中，例如list1 = [a, a]

导致引用计数-1的情况：

> - 对象的别名被显式销毁，例如del a
> - 对象的别名被赋予新的对象，例如a = 24
> - 一个对象离开它的作用域，例如f函数执行完毕时，f函数中的局部变量（全局变量不会）
> - 对象所在的容器被销毁，或从容器中删除对象

引用计数可能会导致循环引用问题，而循环引用会导致内存泄露，如下面的代码所示。为了解决这个问题，Python中引入了“标记-清除”和“分代收集”。在创建一个对象的时候，对象被放在第一代中，如果在第一代的垃圾检查中对象存活了下来，该对象就会被放到第二代中，同理在第二代的垃圾检查中对象存活下来，该对象就会被放到第三代中。

```python
# 循环引用会导致内存泄露 - Python除了引用技术还引入了标记清理和分代回收
# 在Python 3.6以前如果重写__del__魔术方法会导致循环引用处理失效
# 如果不想造成循环引用可以使用弱引用
list1 = []
list2 = [] 
list1.append(list2)
list2.append(list1)
```
## Linux system
### 操作指令
#### 文件和文件夹操作
#### ls命令（list）：列出当前目录下的内容
>- ls -a 显示以点开头的文件和目录（隐藏文件）
>- ls -l 以列表的形式展示当前目录和内容
>> ls -al为上面两者的组合使用与ls -la,ls -l-a效果相同
>- ls -l -h 以列表的形式展示当前目录下的内容以及它们的大小
>- -R：遇到目录要进行递归展开（继续列出目录下面的文件和目录）。
>- -d：只列出目录，不列出其他内容。
>- -S / -t：按大小/时间排序
>- 查看文件内容 - cat / tac / head / tail / more / less / rev / od。
#### cd命令（Change Directory）：切换当前工作目录
>- cd命令后面可以跟相对路径（以当前路径作为参照）或绝对路径（以/开头）来切换到指定的目录cd命令后面可以跟相对路径（以当前路径作为参照）或绝对路径（以/开头）来切换到指定的目录
>- cd ..来返回上一级目录
>- cd ../..返回上上级
>- cd/ 切换到根目录
>- cd 切换到home目录
#### pwd命令（Print Work Directory）：查看当前工作目录
>-  pwd命令，无选项，无参数，直接输入pwd即可

#### 创建/删除空目录 - mkdir / rmdir。  
```python
[root ~]# mkdir abc   
[root ~]# mkdir -p xyz/abc
[root ~]# mkdir ./abc    表示在当前目录下创建    
[root ~]# mkdir ../abc   表示在上一层目录下创建
[root ~]# mkdir ~/abc    表示在home目录下创建
[root ~]# mkdir -p test4/good/nb666  --可以通过-p选项，将一整个链条都创建完成。
[root ~]# ls    
test1  test2  test20250103  test3  test4   
[root ~]# cd test4
[root2 test4]# ls
good
[root ~]# rmdir abc
```
##### 注意：mkdir创建文件夹需要修改权限，请确保操作均在HOME目录内，不要在HOME外操作。涉及到权限问题，HOME外无法成功。
#### 创建/删除文件 - touch / rm。
```python
[root ~]# touch readme.txt
[root ~]# touch error.txt
[root ~]# rm error.txt
rm: remove regular empty file ‘error.txt’? y
[root ~]# rm -rf xyz
```
touch命令用于创建空白文件或修改文件时间。在Linux系统中一个文件有三种时间：
>- 更改内容的时间 - mtime。
>- 更改权限的时间 - ctime。
>- 最后访问时间 - atime。
     
rm的几个重要参数：
>- -i：交互式删除，每个删除项都会进行询问。
>- -r：删除目录并递归的删除目录中的文件和目录。
>- -f：强制删除，忽略不存在的文件，没有任何提示。
#### 拷贝/移动文件 - cp / mv
```python
[root ~]# mkdir backup
[root ~]# cp sohu.html backup/
[root ~]# cd backup
[root backup]# ls
sohu.html
[root backup]# mv sohu.html sohu_index.html
[root backup]# ls
sohu_index.html
```
#### 文件重命名 - rename。
```python
[root@iZwz97tbgo9lkabnat2lo8Z ~]# rename .htm .html *.htm
```
#### 查找文件和查找内容 - find / grep。
```python
[root@iZwz97tbgo9lkabnat2lo8Z ~]# find / -name "*.html"
/root/sohu.html
/root/backup/sohu_index.html
[root@iZwz97tbgo9lkabnat2lo8Z ~]# grep "<script>" sohu.html -n
20:<script>
```
#### cat命令：查看文件内容
语法：cat Linux路径   
cat命令同样没有选项，参数必填，参数表示：被查看的文件路径，相对、绝对、特殊路径符都可以使用。    
####  more命令：分页查看文件内容（内容过多时支持翻页展示）
more命令同样可以查看文件内容，同cat不同的是： cat是直接将内容全部显示出来，more支持翻页，如果文件内容过多，可以一页页的展示。       
语法：more Linux路径      
more同样没有选项，参数必填，参数表示：被查看的文件路径，相对、绝对、特殊路径符都可以使用。      
>Linux系统内置有一个文件，路径为：/etc/services，可以使用more命令查看     
more /etc/services     
在查看的过程中，通过空格翻页    
>通过按q 即可退出查看
#### which命令（查找命令）：查找各命令的程序文件存放在哪个路径
##### 语法：which  要查找的命令  无需选项，只需要参数表示要查找哪个命令
#### find命令（查找文件）：按文件名/文件大小，查找该文件存放在哪个路径
##### 语法：find 起始路径   -name  "被查找的文件名"
也可使用通配符*
>  test*，表示匹配任何以test开头的内容。
> *test，表示匹配任何以test结尾的内容 。
>  *test*，表示匹配任何包含test的内容。

find命令 - 按文件大小查找文件    
语法：find 起始路径  -size  +|-   n[KMG]   
>  +、-表示 大于和小于
>  n表示 大小数字。
>  kMG表示 大小单位，k(小写字母)表示kb，M表示MB，G表示GB。

example
```sql
语法：find 起始路径  -size  +|-  n[KMG]
示例： 
从根目录/开始查找小于10KB的文件： find / -size -10k 
从根目录/开始查找大于100MB的文件：find / -size +100M 
从根目录/开始查找大于1GB的文件：find / -size +1G
```
### [更多linux指令](https://blog.csdn.net/weixin_45806267/article/details/144500055?ops_request_misc=elastic_search_misc&request_id=53c32cf07f8c7c0cd5cf4f6b9afaf9c0&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-144500055-null-null.142^v102^pc_search_result_base9&utm_term=linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F&spm=1018.2226.3001.4187)

### 用户管理
#### 创建和删除用户 - useradd / userdel。
[root home]# useradd hellokitty     
[root home]# userdel hellokitty     
> -d - 创建用户时为用户指定用户主目录    
> -g - 创建用户时指定用户所属的用户组
#### 创建和删除用户组 - groupadd / groupdel。
说明：用户组主要是为了方便对一个组里面所有用户的管理。     
#### 修改密码 - passwd。
```sql
[root ~]# passwd hellokitty
New password: 
Retype new password: 
passwd: all authentication tokens updated successfully.
```
说明：输入密码和确认密码没有回显且必须一气呵成的输入完成（不能使用退格键），密码和确认密码需要一致。如果使用passwd命令时没有指定命令作用的对象，则表示要修改当前用户的密码。如果想批量修改用户密码，可以使用chpasswd命令。
> -l / -u - 锁定/解锁用户。
> -d - 清除用户密码。
> -e - 设置密码立即过期，用户登录时会强制要求修改密码。
> -i - 设置密码过期多少天以后禁用该用户。

#### 查看和修改密码有效期 - chage。
设置hellokitty用户100天后必须修改密码，过期前15天通知该用户，过期后7天禁用该用户。    
##### 语法 chage -M 100 -W 15 -I 7 hellokitty

#### 切换用户 - su。
```sql
[root ~]# su hellokitty
[hellokitty root]$
```
#### 以管理员身份执行命令 - sudo。
```sql
[hellokitty ~]$ ls /root
ls: cannot open directory /root: Permission denied
[hellokitty ~]$ sudo ls /root
[sudo] password for hellokitty:
```
> 说明：如果希望用户能够以管理员身份执行命令，用户必须要出现在sudoers名单中，sudoers文件在 /etc目录下，如果希望直接编辑该文件也可以使用下面的命令

### [more details](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E7%94%A8%E6%88%B7%E7%AE%A1%E7%90%86)

### 文件系统
#### 目录结构
/bin - 基本命令的二进制文件。    
/boot - 引导加载程序的静态文件。    
/dev - 设备文件。     
/etc - 配置文件。     
/home - 普通用户主目录的父目录。     
/lib - 共享库文件。       
/lib64 - 共享64位库文件。     
/lost+found - 存放未链接文件。    
/media - 自动识别设备的挂载目录。    
/mnt - 临时挂载文件系统的挂载点。    
/opt - 可选插件软件包安装位置。     
/proc - 内核和进程信息。      
/root - 超级管理员用户主目录。      
/run - 存放系统运行时需要的东西。     
/sbin - 超级用户的二进制文件。     
/sys - 设备的伪文件系统。      
/tmp - 临时文件夹。     
/usr - 用户应用目录。     
/var - 变量数据目录。       
#### [磁盘管理](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E7%A3%81%E7%9B%98%E7%AE%A1%E7%90%86)

#### [编辑器 - vim](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E7%BC%96%E8%BE%91%E5%99%A8---vim)

#### [软件安装和配置](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E8%BD%AF%E4%BB%B6%E5%AE%89%E8%A3%85%E5%92%8C%E9%85%8D%E7%BD%AE)

#### [源代码构建安装](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E6%BA%90%E4%BB%A3%E7%A0%81%E6%9E%84%E5%BB%BA%E5%AE%89%E8%A3%85)

#### [配置服务](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E9%85%8D%E7%BD%AE%E6%9C%8D%E5%8A%A1)

#### [计划任务](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E8%AE%A1%E5%88%92%E4%BB%BB%E5%8A%A1)

#### [网络访问和管理](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E7%BD%91%E7%BB%9C%E8%AE%BF%E9%97%AE%E5%92%8C%E7%AE%A1%E7%90%86)

#### [进程管理](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E8%BF%9B%E7%A8%8B%E7%AE%A1%E7%90%86)

#### [系统诊断](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E7%B3%BB%E7%BB%9F%E8%AF%8A%E6%96%AD)

#### [Shell编程](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#shell%E7%BC%96%E7%A8%8B)

#### [Linux命令行常用快捷键](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/34-35.%E7%8E%A9%E8%BD%ACLinux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F.md#%E7%9B%B8%E5%85%B3%E8%B5%84%E6%BA%90)


## Web前端

### 结构
>- html
>>- head
>>>- title
>>>- meta
>>- body

### 文本
> 标题（heading）和段落（paragraph）
>- h1 ~ h6
>- p
> 上标（superscript）和下标（subscript）
>- sup
>- sub
> 空白（白色空间折叠）
> 折行（break）和水平标尺（horizontal ruler）
>- br
>- hr
> 语义化标签
>- 加粗和强调 - strong
>- 引用 - blockquote
>- 缩写词和首字母缩写词 - abbr / acronym
>- 引文 - cite
>- 所有者联系信息 - address
>- 内容的修改 - ins / del

> 列表（list）
>- 有序列表（ordered list）- ol / li
>- 无序列表（unordered list）- ul / li
>- 定义列表（definition list）- dl / dt / dd


## [前端详细介绍](https://github.com/lpz726/Python-100-Days/blob/master/Day31-35/32-33.Web%E5%89%8D%E7%AB%AF%E5%85%A5%E9%97%A8.md)    

## 关系型数据库和MySQL概述
### 关系型数据库概述
#### [MySQL 基本命令](https://github.com/lpz726/Python-100-Days/blob/master/Day36-45/36.%E5%85%B3%E7%B3%BB%E5%9E%8B%E6%95%B0%E6%8D%AE%E5%BA%93%E5%92%8CMySQL%E6%A6%82%E8%BF%B0.md#mysql-%E5%9F%BA%E6%9C%AC%E5%91%BD%E4%BB%A4)


### [DDL](https://github.com/lpz726/Python-100-Days/blob/master/Day36-45/37.SQL%E8%AF%A6%E8%A7%A3%E4%B9%8BDDL.md)
(数据定义语言)
### [DML](https://github.com/lpz726/Python-100-Days/blob/master/Day36-45/38.SQL%E8%AF%A6%E8%A7%A3%E4%B9%8BDML.md)
(数据操作语言)
### [DQL](https://github.com/lpz726/Python-100-Days/blob/master/Day36-45/39.SQL%E8%AF%A6%E8%A7%A3%E4%B9%8BDQL.md)
(数据查询语言)
### [DCL](https://github.com/lpz726/Python-100-Days/blob/master/Day36-45/40.SQL%E8%AF%A6%E8%A7%A3%E4%B9%8BDCL.md)
(数据控制语言)

### [json](https://github.com/lpz726/Python-100-Days/blob/master/Day36-45/41.MySQL%E6%96%B0%E7%89%B9%E6%80%A7.md#json%E7%B1%BB%E5%9E%8B)

### [窗口函数](https://github.com/lpz726/Python-100-Days/blob/master/Day36-45/41.MySQL%E6%96%B0%E7%89%B9%E6%80%A7.md#%E7%AA%97%E5%8F%A3%E5%87%BD%E6%95%B0)

