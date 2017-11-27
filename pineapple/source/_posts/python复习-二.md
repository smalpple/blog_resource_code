---
title: python复习(二)
date: 2017-03-28 15:59:54
tags:
categories: python
---
每天刷一章python，gogogo!
## 函数式编程
<!-- more -->
### 高阶函数
既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。
#### map函数
map()函数接收两个参数，一个是函数，一个是Iterable，map将传入的函数依次作用到序列的每个元素，并把结果作为新的Iterator返回。
``` python
def f(x):
    return x*x
r = map(f,[1,2,3,4,5])
list(r)                                 #[1, 4, 9, 16, 25]
list(map(str,[1,2,3,4,5]))              #['1','2','3','4','5']
```
#### reduce函数
reduce把一个函数作用在一个序列[x1, x2, x3, ...]上，这个函数必须接收两个参数，
reduce把结果继续和序列的下一个元素做累积计算，其效果就是：
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
``` python
from functools import reduce
def fn(x,y):
    return x*10+y
reduce(fn,[1,3,5,7,9])                  #13579
```
practice1
``` python
#practise 1                       利用map()函数，把用户输入的不规范的英文名字，变为首字母大写，其他小写的规范名字。
def name(x):
    return x[0].upper()+x[1::].lower()
a=['adam', 'LISA', 'barT']
print(list(map(name,a)))
```
practice2
``` python
#practise 2                       请编写一个prod()函数，可以接受一个list并利用reduce()求积：
def prod(L):
    return reduce(lambda x,y:x*y,L)
print(prod([1,2,3,4,5]))
```
#### filter函数
和map()类似，filter()也接收一个函数和一个序列。和map()不同的是，filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。
``` python
def is_odd(n):
    return n % 2 == 1

list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))                      # 结果: [1, 5, 9, 15]
#注意到filter()函数返回的是一个Iterator，也就是一个惰性序列，所以要强迫filter()完成计算结果，需要用list()函数获得所有结果并返回list。

```
``` python
def _odd_iter():#生成器，3,5,7,9,11.。。。。
    n=1
    while True:
        n = n+2
        yield n
```
``` python
def _not_divisible(n):#筛选函数
    return lambda x: x % n > 0
```
``` python
def primes():#定义一个生成器，不断返回下一个素数，这个生成器先返回第一个素数2，然后，利用filter()不断产生筛选后的新的序列。
    yield 2
    it = _odd_iter() # 初始序列
    while True:
        n = next(it) # 返回序列的第一个数
        yield n
        it = filter(_not_divisible(n), it) # 构造新序列
for n in primes():#由于primes()也是一个无限序列，所以调用时需要设置一个退出循环的条件：
    if n < 1000:
        print(n)
    else:
        break
```
practise1
``` python
#practise:回数是指从左向右读和从右向左读都是一样的数，例如12321，909。请利用filter()滤掉非回数：
def is_palindrome(n):
    return str(n)[::-1] == str(n)
output = filter(is_palindrome, range(1, 1000))
print(list(output))
```
#### sorted函数   
``` python
sorted([36, 5, -12, 9, -21])                    #[-21, -12, 5, 9, 36]
sorted([36, 5, -12, 9, -21], key=abs)           #[5, 9, -12, -21, 36]
```
key指定的函数将作用于list的每一个元素上，并根据key函数返回的结果进行排序。对比原始的list和经过key=abs处理过的list：
list = [36, 5, -12, 9, -21]
keys = [36, 5,  12, 9,  21]
然后sorted()函数按照keys进行排序，并按照对应关系返回list相应的元素：

keys排序结果 => [5, 9,  12,  21, 36]
                |  |    |    |   |
最终结果     => [5, 9, -12, -21, 36]
