# python
python learning
字典推导式语法总结
{key_expression: value_expression for item in iterable if condition}
example:
prices2 = {key: value for key, value in prices.items() if value > 100}
分解说明：

prices.items(): 返回字典中所有键值对的视图

for key, value in prices.items(): 遍历每个股票代码和价格

if value > 100: 筛选条件，只保留价格大于100的股票

key: value: 保留原始的键值对结构
