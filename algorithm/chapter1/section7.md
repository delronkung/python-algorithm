# Python内置类型性能分析

## list的操作测试

```python
def test1():
   l = []
   for i in range(1000):
      l = l + [i]
def test2():
   l = []
   for i in range(1000):
      l.append(i)
def test3():
   l = [i for i in range(1000)]
def test4():
   l = list(range(1000))

from timeit import Timer

t1 = Timer("test1()", "from __main__ import test1")
print("concat ",t1.timeit(number=1000), "milliseconds")
t2 = Timer("test2()", "from __main__ import test2")
print("append ",t2.timeit(number=1000), "milliseconds")
t3 = Timer("test3()", "from __main__ import test3")
print("comprehension ",t3.timeit(number=1000), "milliseconds")
t4 = Timer("test4()", "from __main__ import test4")
print("list range ",t4.timeit(number=1000), "milliseconds")

# ('concat ', 1.7890608310699463, 'milliseconds')
# ('append ', 0.13796091079711914, 'milliseconds')
# ('comprehension ', 0.05671119689941406, 'milliseconds')
# ('list range ', 0.014147043228149414, 'milliseconds')
```

**pop操作测试**

```python
x = list(range(2000000))
pop_zero = Timer("x.pop(0)","from __main__ import x")
print("pop_zero ",pop_zero.timeit(number=1000), "milliseconds")
x = list(range(2000000))
pop_end = Timer("x.pop()","from __main__ import x")
print("pop_end ",pop_end.timeit(number=1000), "milliseconds")

# ('pop_zero ', 1.9101738929748535, 'milliseconds')
# ('pop_end ', 0.00023603439331054688, 'milliseconds')
```
**测试pop操作：从结果可以看出，pop最后一个元素的效率远远高于pop第一个元素**

> 可以自行尝试下list的append(value)和insert(0,value),即一个后面插入和一个前面插入？？？

## list内置操作的时间复杂度
![list操作](/images/list操作.png)

## dict内置操作的时间复杂度
![dict操作](/images/dict操作.png)
