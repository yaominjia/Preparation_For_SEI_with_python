# tuple

# 1. define

```python
>>> t = ('foo', 'bar', 'baz', 'qux', 'quux', 'corge')
>>> t
('foo', 'bar', 'baz', 'qux', 'quux', 'corge')
```

```python
>>> my_list = ['foo', 'bar', 'baz', 'qux', 'quux', 'corge']
>>> t = tuple(my_list)
>>> t
('foo', 'bar', 'baz', 'qux', 'quux', 'corge')
```

be careful

```python
>>> t = (2)
>>> type(t)
<class 'int'>
```

this is valid

```python
>>> t = (2,)
>>> type(t)
<class 'tuple'>
>>> t[0]
2
>>> t[-1]
2
```

## 2. access

tuple中的元素也可以通过下标访问

```python
>>> t = ('foo', 'bar', 'baz', 'qux', 'quux', 'corge')
>>> t
('foo', 'bar', 'baz', 'qux', 'quux', 'corge')

>>> t[0]
'foo'
>>> t[-1]
'corge'
>>> t[1::2]
('bar', 'qux', 'corge')
>>> t[::-1]
('corge', 'quux', 'qux', 'baz', 'bar', 'foo')
```

但是tuple是不可更改的

```python
>>> t = ('foo', 'bar', 'baz', 'qux', 'quux', 'corge')
>>> t[2] = 'Bark!'
Traceback (most recent call last):
  File "<pyshell#65>", line 1, in <module>
    t[2] = 'Bark!'
TypeError: 'tuple' object does not support item assignment
```

## 3. tuple unpacking

```python
>>> t
('foo', 'bar', 'baz', 'qux')
>>> (s1, s2, s3, s4) = t
>>> s1
'foo'
>>> s2
'bar'
>>> s3
'baz'
>>> s4
'qux'
```

左边变量的数量必须和右边tuple中元素的数量相一致

```python
>>> (s1, s2, s3) = t
Traceback (most recent call last):
  File "<pyshell#16>", line 1, in <module>
    (s1, s2, s3) = t
ValueError: too many values to unpack (expected 3)

>>> (s1, s2, s3, s4, s5) = t
Traceback (most recent call last):
  File "<pyshell#17>", line 1, in <module>
    (s1, s2, s3, s4, s5) = t
ValueError: not enough values to unpack (expected 5, got 4)
```

利用unpacking实现魔法

```python
>>> a = 'foo'
>>> b = 'bar'
>>> a, b
('foo', 'bar')

>>># Magic time!
>>> a, b = b, a

>>> a, b
('bar', 'foo')
```

## 4. methods

`a.count(obj)` 返回元素出现的次数

`a.index(obj)` 返回元素首次出现的下标

