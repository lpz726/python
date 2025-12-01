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
>example
>```python
>class Example:
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
>```
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
## 字典推导式语法总结
##### {key_expression: value_expression for item in iterable if condition}
### example:
##### prices2 = {key: value for key, value in prices.items() if value > 100}
>**分解说明：**  
>> prices.items(): 返回字典中所有键值对的视图  
for key, value in prices.items(): 遍历每个股票代码和价格  
if value > 100: 筛选条件，只保留价格大于100的股票  
key: value: 保留原始的键值对结构  
