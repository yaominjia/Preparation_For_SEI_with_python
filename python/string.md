# string

## 1.string manipulation

操作符`+`和`*`

```python
>>> s = 'foo'
>>> t = 'bar'
>>> u = 'baz'

>>> s + t
'foobar'
>>> s + t + u
'foobarbaz'

>>> print('Go team' + '!!!')
Go team!!!
```

```python
>>> s = 'foo.'

>>> s * 4
'foo.foo.foo.foo.'
>>> 4 * s
'foo.foo.foo.foo.'
```

```python
>>> 'foo' * -8
''
```

`in`和`not in`

```python
>>> s = 'foo'

>>> s in 'That\'s food for thought.'
True
>>> s in 'That\'s good for now.'
False
```

```python
>>> 'z' not in 'abc'
True
>>> 'z' not in 'xyz'
False
```

内置函数

将字符转为ASCII值和Unicode值（如果是）

```python
>>> ord('a')
97
>>> ord('#')
35
```

```python
>>> ord('€')
8364
>>> ord('∑')
8721
```

将整数转为ASCII表示的值

```python
>>> chr(97)
'a'
>>> chr(35)
'#'
```

```python
>>> chr(8364)
'€'
>>> chr(8721)
'∑'
```

字符长度

```python
>>> s = 'I am a string.'
>>> len(s)
14
```

将其他类型转化为字符

```python
>>> str(49.2)
'49.2'
>>> str(3+4j)
'(3+4j)'
>>> str(3 + 29)
'32'
>>> str('foo')
'foo'
```

字符下标与切片

```python
>>> s = 'foobar'

>>> s[0]
'f'
>>> s[1]
'o'
>>> s[3]
'b'
>>> len(s)
6
>>> s[len(s)-1]
'r'
```

字符串是不可修改的！

## 2. methods

`s.capitalize()`

```python
>>> s = 'foO BaR BAZ quX'
>>> s.capitalize()
'Foo bar baz qux'
```

`s.lower()`

```python
>>> 'FOO Bar 123 baz qUX'.lower()
'foo bar 123 baz qux'
```

`s.swapcase()`

```python
>>> 'FOO Bar 123 baz qUX'.swapcase()
'foo bAR 123 BAZ Qux'
```

`s.title()`

```python
>>> 'the sun also rises'.title()
'The Sun Also Rises'
```

`s.upper()`

```python
>>> 'FOO Bar 123 baz qUX'.upper()
'FOO BAR 123 BAZ QUX'
```

`s.count(obj, [start, end])`

```python
>>> 'foo goo moo'.count('oo')
3
```

```python
>>> 'foo goo moo'.count('oo', 0, 8)
2
```

`s.endwith(obj, [start, end])`

```python
>>> 'foobar'.endswith('bar')
True
>>> 'foobar'.endswith('baz')
False
```

```python
>>> 'foobar'.endswith('oob', 0, 4)
True
>>> 'foobar'.endswith('oob', 2, 4)
False
```

`s.find(obj, [start, end])` 返回第一个找到的下标

```python
>>> 'foo bar foo baz foo qux'.find('foo')
0
```

```python
>>> 'foo bar foo baz foo qux'.find('grault')
-1
```

```python
>>> 'foo bar foo baz foo qux'.find('foo', 4)
8
>>> 'foo bar foo baz foo qux'.find('foo', 4, 7)
-1
```

`s.index(obj, [start, end])`

和`s.find(obj, [start, end])`相似，在没找到时抛出异常

```python
>>> 'foo bar foo baz foo qux'.index('grault')
Traceback (most recent call last):
  File "<pyshell#0>", line 1, in <module>
    'foo bar foo baz foo qux'.index('grault')
ValueError: substring not found
```

`s.rfind(obj, [start, end])` 返回最后一个找到的下标

```python
>>> 'foo bar foo baz foo qux'.rfind('foo')
16
```

```python
>>> 'foo bar foo baz foo qux'.rfind('grault')
-1
```

```python
>>> 'foo bar foo baz foo qux'.rfind('foo', 0, 14)
8
>>> 'foo bar foo baz foo qux'.rfind('foo', 10, 14)
-1
```

`s.rindex(obj, [start, end])`

```python
>>> 'foo bar foo baz foo qux'.rindex('grault')
Traceback (most recent call last):
  File "<pyshell#1>", line 1, in <module>
    'foo bar foo baz foo qux'.rindex('grault')
ValueError: substring not found
```

`s.startwith(obj, [start, end])`

```python
>>> 'foobar'.startswith('foo')
True
>>> 'foobar'.startswith('bar')
False
```

```python
>>> 'foobar'.startswith('bar', 3)
True
>>> 'foobar'.startswith('bar', 3, 2)
False
```

`s.isalnum()` 返回`True`如果字符串全由字符和数字组成

```python
>>> 'abc123'.isalnum()
True
>>> 'abc$123'.isalnum()
False
>>> ''.isalnum()
False
```

`s.isalpha()`

```python
>>> 'ABCabc'.isalpha()
True
>>> 'abc123'.isalpha()
False
```

`s.isdigit()`

```python
>>> '123'.isdigit()
True
>>> '123abc'.isdigit()
False
```

`s.isidentifier()`返回`True`如果字符串为一个有效的python标识符

```python
>>> 'foo32'.isidentifier()
True
>>> '32foo'.isidentifier()
False
>>> 'foo$32'.isidentifier()
False
```

`s.islower()`

```python
>>> 'abc'.islower()
True
>>> 'abc1$d'.islower()
True
>>> 'Abc1$D'.islower()
False
```

`s.isprintable()`

```python
>>> 'a\tb'.isprintable()
False
>>> 'a b'.isprintable()
True
>>> ''.isprintable()
True
>>> 'a\nb'.isprintable()
False
```

`s.isspace()`

```python
>>> ' \t \n '.isspace()
True
>>> '   a   '.isspace()
False
```

`s.istitle()`

```python
>>> 'This Is A Title'.istitle()
True
>>> 'This is a title'.istitle()
False
>>> 'Give Me The #$#@ Ball!'.istitle()
True
```

`s.isupper()`

```python
>>> 'ABC'.isupper()
True
>>> 'ABC1$D'.isupper()
True
>>> 'Abc1$D'.isupper()
False
```

`s.center(width, [fill])`

```python
>>> 'foo'.center(10)
'   foo    '
```

```python
>>> 'bar'.center(10, '-')
'---bar----'
```

```python
>>> 'foo'.center(2)
'foo'
```

`s.expandtabs(tabsize=8)`

```python
>>> 'a\tb\tc'.expandtabs()
'a       b       c'
>>> 'aaa\tbbb\tc'.expandtabs()
'aaa     bbb     c'
```

```python
>>> 'a\tb\tc'.expandtabs(4)
'a   b   c'
>>> 'aaa\tbbb\tc'.expandtabs(tabsize=4)
'aaa bbb c'
```

`s.ljust(width, [fill])`

```python
>>> 'foo'.ljust(10)
'foo       '
```

```python
>>> 'foo'.ljust(10, '-')
'foo-------'
```

```python
>>> 'foo'.ljust(2)
'foo'
```

`s.lstrip([chars])`

```python
>>> '   foo bar baz   '.lstrip()
'foo bar baz   '
>>> '\t\nfoo\t\nbar\t\nbaz'.lstrip()
'foo\t\nbar\t\nbaz'
```

```python
>>> 'http://www.realpython.com'.lstrip('/:pth')
'www.realpython.com'
```

`s.replace(old, new, [count])`

```python
>>> 'foo bar foo baz foo qux'.replace('foo', 'grault')
'grault bar grault baz grault qux'
```

```python
>>> 'foo bar foo baz foo qux'.replace('foo', 'grault', 2)
'grault bar grault baz foo qux'
```

`s.rjust(width, [fill])`

```python
>>> 'foo'.rjust(10)
'       foo'
```

```python
>>> 'foo'.rjust(10, '-')
'-------foo'
```

```python
>>> 'foo'.rjust(2)
'foo'
```

`s.rstrip([chars])`

```python
>>> '   foo bar baz   '.rstrip()
'   foo bar baz'
>>> 'foo\t\nbar\t\nbaz\t\n'.rstrip()
'foo\t\nbar\t\nbaz'
```

```python
>>> 'foo.$$$;'.rstrip(';$.')
'foo'
```

`s.strip([chars])`

```python
>>> 'www.realpython.com'.strip('w.moc')
'realpython'
```

`s.zfill(width)` 左边填充0

```python
>>> '42'.zfill(5)
'00042'
```

```python
>>> '+42'.zfill(8)
'+0000042'
>>> '-42'.zfill(8)
'-0000042'
```

```python
>>> '-42'.zfill(3)
'-42'
```

## 3. list和string之间的转换

`s,join(iterable)`

```python
>>> ', '.join(['foo', 'bar', 'baz', 'qux'])
'foo, bar, baz, qux'
```

```python
>>> ':'.join('corge')
'c:o:r:g:e'
```

```python
>>> '---'.join(['foo', 23, 'bar'])
Traceback (most recent call last):
  File "<pyshell#0>", line 1, in <module>
    '---'.join(['foo', 23, 'bar'])
TypeError: sequence item 1: expected str instance, int found
```

`s.partiton(sep)` 在第一次出现`sep`的时候分割，返回一个含有3个字符串的tuple

```python
>>> 'foo.bar'.partition('.')
('foo', '.', 'bar')
>>> 'foo@@bar@@baz'.partition('@@')
('foo', '@@', 'bar@@baz')
```

```python
>>> 'foo.bar'.partition('@@')
('foo.bar', '', '')
```

`s.rpartition(sep)` 在最后出现`sep`的地方分割

```python
>>> 'foo@@bar@@baz'.partition('@@')
('foo', '@@', 'bar@@baz')

>>> 'foo@@bar@@baz'.rpartition('@@')
('foo@@bar', '@@', 'baz')
```

`s.rsplit(sep=None, maxsplit=-1)`

```python
>>> 'foo bar baz qux'.rsplit()
['foo', 'bar', 'baz', 'qux']
>>> 'foo\n\tbar   baz\r\fqux'.rsplit()
['foo', 'bar', 'baz', 'qux']
```

```python
>>> 'foo.bar.baz.qux'.rsplit(sep='.')
['foo', 'bar', 'baz', 'qux']
```

连续的分隔符会分出空字符

```python
>>> 'foo...bar'.rsplit(sep='.')
['foo', '', '', 'bar']
```

但是连续的空格不会

```python
>>> 'foo\t\t\tbar'.rsplit()
['foo', 'bar']
```

设置分割的次数

```python
>>> 'www.realpython.com'.rsplit(sep='.', maxsplit=1)
['www.realpython', 'com']
```

```python
>>> 'www.realpython.com'.rsplit(sep='.', maxsplit=-1)
['www', 'realpython', 'com']
>>> 'www.realpython.com'.rsplit(sep='.')
['www', 'realpython', 'com']
```

`s.split(sep=None, maxsplit=-1)`

```python
>>> 'www.realpython.com'.split('.', maxsplit=1)
['www', 'realpython.com']
>>> 'www.realpython.com'.rsplit('.', maxsplit=1)
['www.realpython', 'com']
```

