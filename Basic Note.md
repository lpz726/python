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
 装饰器堆叠
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
>-namedtuple：命令元组，它是一个类工厂，接受类型的名称和属性列表来创建一个类。
>-deque：双端队列，是列表的替代实现。Python中的列表底层是基于数组来实现的，而deque底层是双向链表，因此当你需要在头尾添加和删除元素时，deque会表现出更好的性能，渐近时间复杂度为$O(1)$。
>-Counter：dict的子类，键是元素，值是元素的计数，它的most_common()方法可以帮助我们获取出现频率最高的元素。Counter和dict的继承关系我认为是值得商榷的，按照CARP原则，Counter跟dict的关系应该设计为关联关系更为合理。
>-OrderedDict：dict的子类，它记录了键值对插入的顺序，看起来既有字典的行为，也有链表的行为。
>-defaultdict：类似于字典类型，但是可以通过默认的工厂函数来获得键对应的默认值，相比字典中的setdefault()方法，这种做法更加高效。
>>example
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

## 字典推导式语法总结
##### {key_expression: value_expression for item in iterable if condition}
### example:
##### prices2 = {key: value for key, value in prices.items() if value > 100}
>**分解说明：**  
>> prices.items(): 返回字典中所有键值对的视图  
for key, value in prices.items(): 遍历每个股票代码和价格  
if value > 100: 筛选条件，只保留价格大于100的股票  
key: value: 保留原始的键值对结构  
