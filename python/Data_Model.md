# 数据模型

## 1.对象，值和类型

Python中一切皆对象，不管是数值、字符串，还是列表、字典。甚至是函数和类都是对象。

每个对象都有身份（identity），属于的类型（type）和值（value）。每个对象在被创建后，其身份就不再改变。可以认为其身份就是在内存中的地址。

```python
is
```

操作符比较两个对象的身份是否相同。

```python
id()
```

函数返回一个整数，代表对象的身份，就像是每个人的身份证号码。cpython中返回的是对象在内存中的地址。

对象的类型在被创建后，类型也不可改变。对象的类型决定了该对象所能进行的操作，和可能的取值。

```python
type()
```

函数返回对象的类型。

有些对象的值可以改变（mutable），有些对象的值不能改变（immutable）。

对象不需要主动去销毁，当某个对象不再需要的时候，将会有垃圾回收程序将其回收。

*cpython垃圾回收机制：need to be done*

## 2.常见的类型

None

数字

​	整数

​	布尔

​	浮点数

​	复数

序列：可以通过索引访问其中的某个元素，可以用

```python
len()
```

方法返回其元素个数，可以进行切片。

​	字符串

​	元组

​	Bytes

​	列表

​	Byte arrays

集合：无法通过索引访问其中的元素，可以被遍历，可以用

```python
len()
```

函数返回元素个数。

​	集合

​	Frozen sets

映射

​	字典

Callable

​	用户定义的函数

​	类的实例的方法

​	生成器函数

​	内置的函数和方法

​	类

​	类的实例

## 3 特殊方法（魔法函数，dunder方法）

在自定义类中，可以通过实现某些具有特殊名字的方法，通过相应的调用语法（通常比直接调用特殊方法更简单），来达到赋予自定义的类某种特性或能够进行某种操作，从而保持整个程序的一致性。

名字的特殊指，这些方法必须要以双下划线开头，双下划线结尾，如

```python
__len__()
```

且中间的名字必须使用python预留的名字，否则将无法通过调用语法调用此方法。

一个例子：

```python
import collections
Card = collections.Namedtuple('Card', ['rank', 'suit'])
class FrenchDeck:
	ranks = [str(n) for n in range(2, 11)] + list('JQKA')
	suits = 'spades diamonds clubs heats'.split()
	
	def __init__(self):
		self._cards = [Card(rank, suit) for suit in self.suits for rank in self.ranks]
		
	def __len__(self):
		return len(self._cards)
		
	def __getitem__(self, index):
		return self._card[index]
```

上述的类实现了

```python
__len__(), __getitem__()
```

两个特殊方法后，分别可以通过

```python
card = FrenchDeck()
len(card)
card[1]
```

返回实例的长度和通过索引取值，实现了类似于序列的效果。

另一个例子：

```python
from math import hypot
class Vector:
	def __init__(self, x=0, y=0):
		self.x = x
		self.y = y
	
	def __repr__(self):
		return f"Vector({self.x}, {self.y})"
	
	def __abs__(self):
		return hypot(self.x, self.y)
		
	def __bool__(self):
		return bool(abs(self))
		
	def __add__(self, other):
		return Vector(self.x + other.x, self.y + other.y)
		
	def __mul__(self, scalar=1):
		return Vector(self.x * scalar, self.y * scalar)
```

在实现了

```python
__add__(), __mul__()
```

方法后，就是实现了两个实例间的 ‘+’ 和 ‘*’ 操作，这也叫操作符重载。

这也是python中所谓鸭子类型的基础，定义的什么类不重要，重要的是这个类中所实现的特殊函数，如果实现了某一特殊函数，那么这个类就可以用于某个操作的操作数（函数的参数）。

### 参考：

[[3. Data model — Python 3.9.2 documentation](https://docs.python.org/3/reference/datamodel.html)](https://docs.python.org/3/reference/datamodel.html)

《fluent python》

