## 启发式算法
贪心算法的升级版
在启发式搜索里面，会考虑两个集合，一个叫**Open set** 一个叫 **Closed set**

Open：表示当前需要考虑的，还未完成搜索的节点  
Closed：表示已经处理完毕，不会再考虑的节点  
启发式搜索的大概步骤是：  

1. 把初始的节点加入到Open集合中  
2. 将Open set中的节点按照评估函数f(x)的大小从小到大排序，选出最小的那个，设置成当前的节点（CS），如果已经没有可以选的了，结束，表示未搜索到  
3. 如果CS是终点，结束操作  
4. 将CS的所有可达节点进行以下操作：  
如果节点在Closed list中，继续下一个  
否则加入到 Open list中  
将CS加入Closed list中，回到第2步    
#### 算法的评估函数为：f(n) = g(n) + h(n)    
g(n) 表示从开始移动到节点 **n** 的实际代价    
h(n) 启发式估计当前节点**n**到目标节点的代价
#### 最优解函数为：f*(n)=g*(n)+h*(n)  
g*(n):从起点到**n**的最优代价  
h*(n):从**n**到目标的最优代价  
#### 算法保证：    
当 h(n) ≤ h*(n)（可采纳）且 h(n) 满足一致性（即对于任意节点 n 及其后继 n'，有 h(n) ≤ c(n,n') + h(n')）时，A* 算法在第一次扩展节点 n 时，就有 g(n) = g*(n)，并且能找到全局最优解。  
> c(n,n') 表示n到相邻节点的距离

 ## 推理
### 五大推理规则
|规则|	形式化表示|	通俗解释|
|---|----|-----|
|取式假言推理|	P, P→Q ⊢ Q|	如果P且P蕴含Q为真，则Q为真|
|拒式假言推理|	P→Q, ¬Q ⊢ ¬P|	如果P蕴含Q，且Q为假，则P为假|
|与消除	|P∧Q ⊢ P 或 P∧Q ⊢ Q|	如果P且Q为真，则P为真，Q也为真|
|与引入	|P, Q ⊢ P∧Q	|如果P为真且Q为真，则P且Q为真|
|全称例化	|∀X p(X) ⊢ p(a)|	如果对所有X都成立，则对某个具体a也成立|

∧逻辑与  
∨逻辑或  
¬ 取反    
P→Q P=T,Q=F为F,其余时候为T   
### 合一算法
合一：判断什么样的替换可以使两个谓词表达式匹配的算法   
合一表明了两个或多个表达式在什么条件下可以称为等价的。   
替换：   
一个替换(Substitution)就是形如**{t1/x1,t2/x2,….tn/xn}**的有限集合，x1,x2.,,,xn是互不相同的个体变元，ti不同于xi, xi也不循环出现在tj中  
如：{a/x,g(y)/y,f(g(b))/z}    正确！   
        {g(y)/x,f(x)/y}       错误！  

斯柯伦标准化：去掉所有的存在量词    
(X)(彐Y)(mother(X,Y))变为(X) (mother(X,m(X))     
组合(composition) ：在合一过程中，如果先后产生S和S’的替换，那么将S中的某个元素应用S’，所产生的新的替换，称为组合。   
    如：{X/Y, W/Z}, {V/X}, {a/V, f(b)/W}      
    组合过程： {X/Y, W/Z}, {V/X}组合产生{V/Y, W/Z}   
              {V/Y, W/Z},{a/V, f(b)/W} 组合产生{a/Y, f(b)/Z}    

#### 算法
UNIFY   
```python
case    
E1, E2 或者是常元或者是空表:    %递归终止   
        If  E1 ＝ E2  then return {  };    
        else  return FAIL;    
E1是一个变元:     
        if  E1在E2中出现 then  return FAIL;    
        else  return {E2/E1};    
E2是一个变元:     
        if  E2在E1中出现 then  return FAIL;    
        else  return {E1/E2};    
其他情况:  % E1和E2都是表     
```
核心算法
```python
begin
        HE1 = E1的第一个元素;
        HE2 = E2的第一个元素;
        SUBS1 = unify (HE1, HE2);
        if (SUBS1 ＝ FAIL) then return FAIL;
        TE1 = apply (SUBS1, E1的后半部);
        TE2 = apply (SUBS1, E2的后半部);
        SUBS2 = unify (TE1, TE2 );
        if  (SUBS2 ＝ FAIL) then  return FAIL;
        else return SUBS1与SUBS2 的并集;
 end
```
example 
```python
E1:parents(X, father(X), mother(bill)) 
E2:parents(bill, father(bill), Y)  
SUBS1 = unify (HE1, HE2);   
{bill/X}  
E1:parents(bill, father(bill), mother(bill))  
E2:parents(bill, father(bill), Y)   
 SUBS2 = unify (TE1, TE2 );     
{mother(bill)/Y} 
E1:parents(bill, father(bill), mother(bill))  
E2:parents(bill, father(bill), mother(bill))   
finally  
{bill/X, mother(bill)/Y}   组合
```

### 归结
算法步骤： 
1. 转换子句
> 消去蕴含： a→b ≡﹁a∨b   
> 全称量词直接省略，因为你可以用很多个替换实现  
> 然后把所有子句换成合取范式（内层是∨外层是∧的），然后拆分成只有﹁和∨的子句
    
2. 只使用消解规则和替换进行推导，弄出证明树














