# itertools

itertools模块是python实现的一系列作用于可迭代的对象，用于方便地生成更复杂的可迭代对象的函数。

## 1. 分类

1. 生成无限长的序列`count()`，`cycle()`和`repeat()`
2. 生成有限长的序列`accumulate()`，`chain()`，`compress()`，`dropwhile()`，`filterfalse()`和`zio_longest()`
3. 组合式的生成`product()`，`permutations()`，`combinations()`和`combinations_with_replacement()`

## 2. 函数与例子

`count()`

```python
itertools.count(start=0, step=1)
```

从start开始，以step为步长，无限地生成序列

```python
import itertools
for i in itertools.count(20, 3):
   print(i)
   if i > 30:
     break
```

```python
20
23
26
29
32
```

`cycle()`

```python
itertools.cycle(iterable)
```

不断地iter输入的iterable

```python
import itertools
# Create a list that shows several places
places = ["home", "school", "cafe", "gym","restaurants",  "park"]
places_cycle = itertools.cycle(places)
# If you didn't give a value, this would cycle forever
for i in range(9):
    # Then call next() whenever you want another one.
    place = next(places_cycle)
    # Print this value with format method
    print("Going {}".format(place))
```

```python
Going home
Going school
Going cafe
Going gym
Going restaurants
Going park
Going home
Going school
Going cafe
```

`repeat()`

```python
itertools.repeat(object[, times])
```

不断地重复输入的对象，除非传入了`times`参数

```python
for i in itertools.repeat(“Look at this! I'm repeat!”):
    print(i)
```

```python
Look at this! I'm repeat!
Look at this! I'm repeat!
Look at this! I'm repeat!
Look at this! I'm repeat!
...
```

```python
import itertools
print([i for i in itertools.repeat(‘example’, 5)])
```

```python
['example', 'example', 'example', 'example', 'example']
```

`accumulate()`

```python
itertools.accumulate(iterable[,func,*,initial=None])
```

直接上例子

```python
data = [1, 2, 3, 4, 5]
result = itertools.accumulate(data,operator.mul)
for each in result:
    print(each)
```

```python
1
2
6
24
120
```

```python
data = [5, 2, 6, 4, 5, 9, 1]
result = itertools.accumulate(data, max)
for each in result:
    print(each)
```

```python
5
5
6
6
6
9
9
```

如果不传入函数，就会默认累加

```python
data = [5, 2, 6, 4, 5, 9, 1]
result = itertools.accumulate(data)
for each in result:
    print(each)
```

```python
5
7
13
17
22
31
32
```

`chain()`

```python
itertools.chain(*iterables)
```

将多个iteralbes首尾相连

```python
from itertools import chain

odd =[1, 3, 5, 7, 9]
even =[2, 4, 6, 8, 10]
# chaining odd and even numbers
numbers = list(chain(odd, even))
print(numbers)
```

```python
[1, 3, 5, 7, 9, 2, 4, 6, 8, 10]
```

`compress()`

```python
itertools.compress(data, selectors)
```

两个等长的iterable，留下data里的对象，当selectors中相应位置的对象为`True`的时候

```python
import itertools 
  
prog_lang =['C', 'C++',"C#", 'Java', 'Python',"JavaScript"] 
selectors = [False, False, False, True, True, False] 
  
best_programming = itertools.compress(prog_lang, selectors) 
  
for each in best_programming: 
    print("One of the best programming language is " + each)
```

```python
One of the best programming language is Java
One of the best programming language is Python
```

`dropwhile()`

```python
itertools.dropwhile(predicate, iterable) 
```

predicate是一个callable，返回iterable中从predicate为`False`起的所有对象。

```python
import itertools 
data = [2, 4, 6, 7, 8, 9, 10, 11, 12]
result = itertools.dropwhile(lambda x: x%2==0, data)
for each in result:
    print(each)
```

```python
7
8
9
10
11
12
```

`filterfalse()`

```python
itertools.filterfalse(predicate, iterable)
```

返回predicate为`False`的对象

```python
from itertools import filterfalse  
   
li = [1, 2, 3, 4, 5, 7, 8]
  
print("Even numbers in the list:") 
print (list(itertools.filterfalse(lambda x : x % 2 == 0, li)))
print("If function is a None:") 
print (list(itertools.filterfalse(None, li)))
```

```python
Even numbers in the list:
[1, 3, 5, 7]
If function is a None:
[]
```

`groupby()`

```python
itertools.groupby(iterable, key=None)
```

key是一个callable，将iterable中按key的值进行分类

```python
import itertools 
  
li = [("a", 1), ("a", 2), ("b", 3), ("b", 4),("c", 5),(None, None)] 
  
key_func_1 = lambda x: x[0]
print("First key function:")
for key, group in itertools.groupby(li, key_func_1): 
    print(str(key) + " :", list(group))
key_func_2 = lambda x: x[1]
print("Second key function:")
for key, group in itertools.groupby(li, key_func_2): 
    print(str(key) + " :", list(group))
```

```python
Firt key function:
a : [('a', 1), ('a', 2)]
b : [('b', 3), ('b', 4)]
c : [('c', 5)]
None : [(None, None)]
Second key function:
1 : [('a', 1)]
2 : [('a', 2)]
3 : [('b', 3)]
4 : [('b', 4)]
5 : [('c', 5)]
None : [(None, None)]
```

`islice()`

```python
itertools.islice(iterable, start, stop[, step])
```

对iterable进行切片

```python
import itertools 
 
cities = [‘New York’, “Baku”, ‘London’, ‘Istanbul’, ‘Moscow’, ‘Paris’]
few_cities = itertools.islice(cities, 3)
print(list(few_cities))
```

```python
['New York', 'Baku', 'London']
```

`starmap()`

```python
itertools.starmap(function, iterable)
```

返回iterable中每个对象调用function的返回值

```python
import operator
from itertools import starmap 
  
li =[(2, 4), (3, 2), (4, 5)] 
  
new_li = list(starmap(operator.mul, li)) 
  
print(new_li)
```

```python
[8, 6, 20]
```

`takewhile()`

`dropwhile()`的反向操作，取iterable中的元素，直到predicate为`False`

```python
itertools.takwwhile(predicate, iterable)
```

```python
import itertools data = [2, 4, 6, 7, 8, 9, 10, 11, 12]
result = itertools.takewhile(lambda x: x%2==0, data)
for each in result:
    print(each)
```

```
2
4
6
```

`tee()`

```python
itertools.tee(iterable, n=2)
```

返回n个一样且独立的iterable

```python
import itertools 
    
# using tee() to make a list of iterators   
iterator1, iterator2, iterator3 = itertools.tee([1, 2, 3, 4, 5], 3) 
    
# printing the values of iterators  
print (list(iterator1))
# if we try to print the same list again, we get an empty list
print (list(iterator1))  
print (list(iterator2))  
print (list(iterator3))
```



```
[1, 2, 3, 4, 5]
[]
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5]
```

`zip_longest()`

```python
itertools.zip_longest(*iterables, fillvalue=None)
```

返回一个iterable，其中的对象是每个iterable的对象的聚合，如果iterable的长短不一，用fillvalue替代缺失的对象。

```python
import itertools 
    
colors = ['red', 'orange', 'yellow', 'green', 'blue']
data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for each in itertools.zip_longest(colors, data, fillvalue="anything"):
    print(each)
```

```
('red', 1)
('orange', 2)
('yellow', 3)
('green', 4)
('blue', 5)
('anything', 6)
('anything', 7)
('anything', 8)
('anything', 9)
('anything', 10)
```

`product()`

```python
itertools.product(*iterables, repeat=1)
```

product是一个有序对(a, b)，a和b分别来自不同的iterable

```python
import itertools 
    
num_data = [1, 2]
alpha_data = ['a', 'b', 'c']
result = itertools.product(num_data, alpha_data)
for each in result:
    print(each)
print("If we add repeat section:")
num_data_2 = [1]
alpha_data_2 = ['a', 'b']
result_2 = itertools.product(num_data_2, alpha_data_2, repeat=2)
for each in result_2:
    print(each)
```

```
(1, 'a')
(1, 'b')
(1, 'c')
(2, 'a')
(2, 'b')
(2, 'c')
If we add repeat section:
(1, 'a', 1, 'a')
(1, 'a', 1, 'b')
(1, 'b', 1, 'a')
(1, 'b', 1, 'b')
```

`permutations()`

```python
itertools.permutations(iterable, r=None)
```

返回长度为r的所有置换序列

```python
import itertools 
    
data = ['1', '2', '3']
result = itertools.permutations(data)
for each in result:
    print(each)
print("If r is specified (ex. r=2):")
data_2 = ['1', '2', '3']
result_2 = itertools.permutations(data_2, 2)
for each in result_2:
    print(each)
```

```python
('1', '2', '3')
('1', '3', '2')
('2', '1', '3')
('2', '3', '1')
('3', '1', '2')
('3', '2', '1')
If r is specified (ex. r=2):
('1', '2')
('1', '3')
('2', '1')
('2', '3')
('3', '1')
('3', '2')
```

`combinations()`

```python
itertools.combinations(iterable, r)
```

返回iterable中所有长度为r的序列

```python
shapes = ['circle', 'triangle', 'square',]
result = itertools.combinations(shapes, 2)for each in result:
    print(each)
```

```python
('circle', 'triangle')
('circle', 'square')
('triangle', 'square')
```

```python
shapes = ['circle', 'triangle', 'square',]
result = itertools.combinations(shapes, 3)for each in result:
    print(each)
```

```python
('circle', 'triangle', 'square')
```

`combinations_with_replacement()`

```python
itertools.combinations_with_replacement(iterable, r)
```

与上面类似，但是这个允许对象的重读

```python
shapes = ['circle', 'triangle', 'square',]
result = itertools.combinations_with_replacement(shapes, 2)
for each in result:
    print(each)
```

```
('circle', 'circle')
('circle', 'triangle')
('circle', 'square')
('triangle', 'triangle')
('triangle', 'square')
('square', 'square')
```

