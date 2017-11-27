---
title: python复习(一)
date: 2017-03-27 16:18:52
tags:
categories: python
---
最近工作不是很忙，在写代码的过程发现自己的基础还是很不牢靠，决定刷一遍python基础，如果不是很忙每天刷一章，let's go!
## 第一部分:python高级特性
<!-- more -->
### 切片
字符串'xxx'也可以看成是一种list，每个元素就是一个字符。因此，字符串也可以用切片操作，
只是操作结果仍是字符串：
``` python
list0 = [1,2,3,4,5,6,7,8,9]
print(list0[0:3])     #从第一个开始取到第三个元素      [1, 2, 3]
print(list0[:3])      #索引是0可不写                  [1, 2, 3]
print(list0[-3:-1])   #从倒数第三个取到倒数第一个元素  [7, 8]
print(list0[-3:])     #从倒数第三个取到最后           [7, 8, 9]
print(list0[:8:2])    #前8个数，每两个取一个          [1, 3, 5, 7]
print(list0[::5])     #所有数，每5个取一个            [1, 6]
print(list0[:])       #只写[:]就可以原样复制一个list  [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
### 列表生成式
``` python
list1 = list(range(1, 11))   #list1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
list2 = list(x*x for x in range(1,11))  #list2 = [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
list3 = list(d for d in os.listdir())   #列出当前目录下的所有文件和目录名
#practise :
L = ['Hello', 'World', 18, 'Apple', None]
print([s.lower() for s in L if isinstance(s,str)])

```
### 生成器
要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的[]改成()，就创建了一个generator：
``` python
g = (x*x for x in range(10))     #<generator object <genexpr> at 0x00000000023269D8>
#next(g)                         #不断调用next(g)获取生成器g里面的值
for i in g:                      #获取生成器g里面的值
    print(i)
```
定义generator的另一种方法。如果一个函数定义中包含yield关键字，那么这个函数就不再是一个普通函数，而是一个generator：
``` python
def fib(max):                   
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
```
``` python
#practise :
def triangles():
    L = [1]
    while True:
        yield L
        L.append(0)
        L = [L[i - 1] + L[i] for i in range(len(L))]
n = 0
for t in triangles():
    print(t)
    n = n + 1
    if n == 3:
        break
```
