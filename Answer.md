# 题目答案

## 2.3.1

对于1.1.1 如果要求的并不是最值，而是均值，他的算法逻辑应该是怎么样的？ 他的Python代码是什么样的？

```python



```


## 2.3.2

对于数组`[1,2,3,4,5,6,7,8,9,10]`, 求period=3的移动平均(MA, Moving Average)数组。

```python
# 基础版： 不适用于period较大的情况
size = len(arr)
MA = []
for i in range(2,size):
    ave = (arr[i-2]+arr[i-1]+arr[i])/3
    MA.append(ave)

# 进阶版：
# 考虑移动平均的计算中相邻数的差别仅在头尾值，因此记住窗口总和，移动窗口时做增减。避免重复运算
size = len(arr)
MA = []
sum = 0

for i in range(3):
    sum += arr[i]
MA.append(sum/3)

for i in range(3, size):
    sum -= arr[i-3]
    sum += arr[i]
    MA.append(sum/3)
```

## 2.3.3

基于上一问题，写一个函数，使之接受参数N, Arr，输出Arr关于N的移动平均MA数组。

```python
# 由进阶版改来：
def get_MA(Arr, N):
    size = len(Arr)
    MA = []
    sum = 0

    for i in range(N):
        sum += Arr[i]
    MA.append(sum/N)

    for i in range(N, size):
        sum -= Arr[i-N]
        sum += Arr[i]
        MA.append(sum/N)
```

使用大循环内套小循环 每次重新计算sum 也是对的。

## 2.3.4

根据ARIMA自回归得出某价格序列关系`a[t]=K*a[t-1]+M*a[t-2]+F(t)`,假设其他人的代码中已经定义F(t)函数，那么设计一个递归函数`def pred(prices: List[int], n, K, M)`使之能够依据已有过往prices数据预测n期之后的价格。

```python
from typing import List  # type hint, 类型List[int]给程序员自动补全代码用的。
# 这里假设prices最新数据在头部
# 解法1： a[n] = K*a[n-1]+M*a[n-2]+F(n), n>=0, 设定初始值n==0,1,2
def pred(prices: List[int], n, K, M):
    if (n==0):  return prices[0]
    elif (n==1):
        return K*prices[0]+M*prices[1] + F(n)
    elif (n==2):
        return K*pred(prices, n-1, K, M)+M*prices[1] + F(n)
    else:  # n>=3
        return K*pred(prices, n-1, K, M)+M*pred(prices, n-2, K, M)+F(n)

# 解法2：  不限定初始值n>=0。 对于预测过程，n==-1及0是过往值无需预测，转换思路，数列n从-1开始，初始值 n==-1 及 n==0。减少分支和代码量。
def pred(prices: List[int], n, K, M):
    if (n==-1): return prices[1]
    if (n== 0): return prices[0]
    else:  # n>0
        return K*pred(prices, n-1, K, M)+M*pred(prices, n-2, K, M)+F(n)

```