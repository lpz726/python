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
## 字典推导式语法总结
##### {key_expression: value_expression for item in iterable if condition}
### example:
##### prices2 = {key: value for key, value in prices.items() if value > 100}
>**分解说明：**  
>> prices.items(): 返回字典中所有键值对的视图  
for key, value in prices.items(): 遍历每个股票代码和价格  
if value > 100: 筛选条件，只保留价格大于100的股票  
key: value: 保留原始的键值对结构  
