# 处理字典中不存在的键值

## 1.利用字典处理不存在的键值

在python的字典中，当访问的键值不存在于字典时，python会抛出`KeyError`。为了避免这种烦人的情况，可以采用如下四种方法。

1.使用`.setdefault()`

```python
a_dict = {}
a_dict.setdefault('miss_key', 'default_value')
```

当访问`a_dict['miss_key']`时，就会得到`'default_value'`值。

如果对已经存在的键值调用`.setdefault()`方法，将不会产生任何影响。

2.使用`.get()` 

```python
a_dict = {}
a_dict.get('miss_key', 'default_value')
```

当访问`a_dict['miss_key']`时，就会得到`'default_value'`值。但与上面不同的是，`.get()`只返回读取的键值，并不会把这个键值对写入字典中。

3.使用`if`语句

```python
a_dict = {}
if 'miss_key' in a_dict:
	#do something
else:
	a_dict['miss_key'] = 'default_value'
```

注意，`in`只能查找键，不能应用于值的查找。

4.使用`try`和`except`

```python
a_dict = {}
try:
	a_dict['miss_key']
except KeyError:
	a_dict['miss_key'] = 'default_value'
```

## 2.python 的`defaultdict`

要使用`defaultdict`,需引入

```python
from collections import defaultdict
```

创建一个`defaultdict`,需向其传入一个callable参数（当此参数为`None`时，`defaultdict`和`dict`没有区别，当此参数不为callable时，将会抛出`TypeError`），当访问不存在的键时，就会以调用此callable自动生成默认的值。

```python
def_dict = defaultdict(list)
def_dict['miss_key']
```

此时会调用`list`，生成一个空数组。

## 3.`defaultdict`的用法

1.分类

```python
dep = [('Sales', 'John Doe'),
       ('Sales', 'Martin Smith'),
       ('Accounting', 'Jane Doe'),
       ('Marketing', 'Elizabeth Smith'),
       ('Marketing', 'Adam Doe')]
       
from collections import defaultdict

dep_dd = defaultdict(list)
for department, employee in dep:
    dep_dd[department].append(employee)
```

此时得到的`defaultdict`为：

```python
defaultdict(<class 'list'>, {'Sales': ['John Doe', 'Martin Smith'],
'Accounting' : ['Jane Doe'],
'Marketing': ['Elizabeth Smith', 'Adam Doe']})
```

传统的做法：

```python
dep_d = dict()
for department, employee in dep:
	dep_d.setdefault(department, []).append(employee)
```

`defaultdict`明显具有更好的可读性，不仅如此，还能带来效率上的提升。

2.分类并去除重复元素

```python
dep = [('Sales', 'John Doe'),
       ('Sales', 'Martin Smith'),
       ('Accounting', 'Jane Doe'),
       ('Marketing', 'Elizabeth Smith'),
       ('Marketing', 'Elizabeth Smith'),
       ('Marketing', 'Adam Doe'),
       ('Marketing', 'Adam Doe'),
       ('Marketing', 'Adam Doe')]

dep_dd = defaultdict(set)
for department, employee in dep:
    dep_dd[department].add(employee)
```

3.对元素进行计数

```python
from collections import defaultdict
dep = [('Sales', 'John Doe'),
        ('Sales', 'Martin Smith'),
        ('Accounting', 'Jane Doe'),
        ('Marketing', 'Elizabeth Smith'),
        ('Marketing', 'Adam Doe')]
dd = defaultdict(int)
for department, _ in dep:
    dd[department] += 1
```

当调用`int()`时，产生一个整数0。可以用如下的方式，让初始化为1：

```python
def_dict = defaultdict(lambda: 1)
```

另一个例子：

```python
from collections import defaultdict
s = 'mississippi'
dd = defaultdict(int)
for letter in s:
    dd[letter] += 1
```

使用`collections.Counter`模块，可以让这一过程更简洁：

```python
from collections import Counter
counter = Counter('mississippi')
```

```python
Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
```

## 4.Diving deeper

对`defaultdict`使用`.get()`方法不会产生新的键值对，当`get()`的键不存在时，只会返回`None`。这是因为`.get()`不会call`.__missing__()`,其负责call`.default_factory`,生成default值。

可以中途改变`.default_factory`的值来改变默认生成的类型。也可以将`.default_factory`设为`None`,让其变成一个普通的`dict`。

