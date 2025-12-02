# python
python learning
## 特性对比表
| 特性  	|列表(List)|	元组(Tuple)|	字典(Dict)|	类(Class)|
| ------- | ------------|------------|------------|------------|
|可变性|	可变	|不可变	|可变	|可变（实例属性）
|有序性	|有序|	有序	|有序（3.7+）	|属性无序|
|索引方式|	数字索引	|数字索引	|键索引	|属性名|
|内存效率	|较低	|较高|	中等|	取决于实现|
|查找速度	|O(n)	|O(n)|	O(1)平均|	O(1)属性访问|
|使用场景	|同构数据集合|	异构数据记录	|键值映射	|复杂数据结构|
|哈希性	|不可哈希	|可哈希（元素也需可哈希）|	不可哈希|自定义|
|添加|list.append(add),list.insert(num,add)||dic.update()
|删除|list.pop(num or del),list.remove(del)，del list[num]| |dic.pop(),del dic[]|
|排序|list.sort()|||
|反转|list.reverse()|||
|查找|| | dic.value=dic.get(key)|
>add:代表所添加元素  
>num：代表元素在结构中的位置  
>del：代表删除的元素
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
### 装饰器  
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

## 字典推导式语法总结
##### {key_expression: value_expression for item in iterable if condition}
### example:
##### prices2 = {key: value for key, value in prices.items() if value > 100}
>**分解说明：**  
>> prices.items(): 返回字典中所有键值对的视图  
for key, value in prices.items(): 遍历每个股票代码和价格  
if value > 100: 筛选条件，只保留价格大于100的股票  
key: value: 保留原始的键值对结构  
