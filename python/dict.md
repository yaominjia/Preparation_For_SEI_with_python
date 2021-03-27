# dict

## 1. define

```python
>>> MLB_team = {
...     'Colorado' : 'Rockies',
...     'Boston'   : 'Red Sox',
...     'Minnesota': 'Twins',
...     'Milwaukee': 'Brewers',
...     'Seattle'  : 'Mariners'
... }
```

```python
>>> MLB_team = dict([
...     ('Colorado', 'Rockies'),
...     ('Boston', 'Red Sox'),
...     ('Minnesota', 'Twins'),
...     ('Milwaukee', 'Brewers'),
...     ('Seattle', 'Mariners')
... ])
```

```python
>>> MLB_team = dict(
...     Colorado='Rockies',
...     Boston='Red Sox',
...     Minnesota='Twins',
...     Milwaukee='Brewers',
...     Seattle='Mariners'
... )
```

```python
>>> MLB_team
{'Colorado': 'Rockies', 'Boston': 'Red Sox', 'Minnesota': 'Twins',
'Milwaukee': 'Brewers', 'Seattle': 'Mariners'}
```

## 2. access

```python
>>> MLB_team['Minnesota']
'Twins'
>>> MLB_team['Colorado']
'Rockies'
```

访问不存在的key将会抛出异常

```python
>>> MLB_team['Toronto']
Traceback (most recent call last):
  File "<pyshell#19>", line 1, in <module>
    MLB_team['Toronto']
KeyError: 'Toronto'
```

添加与更新

```python
>>> MLB_team['Kansas City'] = 'Royals'
>>> MLB_team
{'Colorado': 'Rockies', 'Boston': 'Red Sox', 'Minnesota': 'Twins',
'Milwaukee': 'Brewers', 'Seattle': 'Mariners', 'Kansas City': 'Royals'}
```

```python
>>> MLB_team['Seattle'] = 'Seahawks'
>>> MLB_team
{'Colorado': 'Rockies', 'Boston': 'Red Sox', 'Minnesota': 'Twins',
'Milwaukee': 'Brewers', 'Seattle': 'Seahawks', 'Kansas City': 'Royals'}
```

删除

```python
>>> del MLB_team['Seattle']
>>> MLB_team
{'Colorado': 'Rockies', 'Boston': 'Red Sox', 'Minnesota': 'Twins',
'Milwaukee': 'Brewers', 'Kansas City': 'Royals'}
```

```python
>>> MLB_team.pop('Boston')
>>> MLB_team
{'Colorado': 'Rockies', 'Minnesota': 'Twins',
'Milwaukee': 'Brewers', 'Kansas City': 'Royals'}
```

```python
>>> MLB_team.popitem()
>>> MLB_team
{'Colorado': 'Rockies', 'Minnesota': 'Twins',
'Milwaukee': 'Brewers'}
```

## 3. keys must be immutable

```python
>>> d = {[1, 1]: 'a', [1, 2]: 'b', [2, 1]: 'c', [2, 2]: 'd'}
Traceback (most recent call last):
  File "<pyshell#20>", line 1, in <module>
    d = {[1, 1]: 'a', [1, 2]: 'b', [2, 1]: 'c', [2, 2]: 'd'}
TypeError: unhashable type: 'list'
```

而对于value则没有任何限制

## 4. methods

检查key是否在字典中

```python
>>> MLB_team = {
...     'Colorado' : 'Rockies',
...     'Boston'   : 'Red Sox',
...     'Minnesota': 'Twins',
...     'Milwaukee': 'Brewers',
...     'Seattle'  : 'Mariners'
... }

>>> 'Milwaukee' in MLB_team
True
>>> 'Toronto' in MLB_team
False
>>> 'Toronto' not in MLB_team
True
```

`d.clear()`

```python
>>> d = {'a': 10, 'b': 20, 'c': 30}
>>> d
{'a': 10, 'b': 20, 'c': 30}

>>> d.clear()
>>> d
{}
```

`d.get(key, default=None)`

```python
>>> d = {'a': 10, 'b': 20, 'c': 30}

>>> print(d.get('b'))
20
>>> print(d.get('z'))
None
```

```python
>>> print(d.get('z', -1))
-1
```

`d.items()`

```python
>>> d = {'a': 10, 'b': 20, 'c': 30}
>>> d
{'a': 10, 'b': 20, 'c': 30}

>>> list(d.items())
[('a', 10), ('b', 20), ('c', 30)]
>>> list(d.items())[1][0]
'b'
>>> list(d.items())[1][1]
20
```

`d.keys()`

```python
>>> d = {'a': 10, 'b': 20, 'c': 30}
>>> d
{'a': 10, 'b': 20, 'c': 30}

>>> list(d.keys())
['a', 'b', 'c']
```

`d.values()`

```python
>>> d = {'a': 10, 'b': 20, 'c': 30}
>>> d
{'a': 10, 'b': 20, 'c': 30}

>>> list(d.values())
[10, 20, 30]
```

`d.pop(key, default)` 返回key的value，如果key不存在返回default

```python
>>> d = {'a': 10, 'b': 20, 'c': 30}

>>> d.pop('b')
20
>>> d
{'a': 10, 'c': 30}
```

```python
>>> d = {'a': 10, 'b': 20, 'c': 30}

>>> d.pop('z')
Traceback (most recent call last):
  File "<pyshell#4>", line 1, in <module>
    d.pop('z')
KeyError: 'z'
```

```python
>>> d = {'a': 10, 'b': 20, 'c': 30}
>>> d.pop('z', -1)
-1
>>> d
{'a': 10, 'b': 20, 'c': 30}
```

`d.popitem()` 返回dict中的最后一组，空dict出现异常

```python
>>> d = {'a': 10, 'b': 20, 'c': 30}

>>> d.popitem()
('c', 30)
>>> d
{'a': 10, 'b': 20}

>>> d.popitem()
('b', 20)
>>> d
{'a': 10}
```

```python
>>> d = {}
>>> d.popitem()
Traceback (most recent call last):
  File "<pyshell#11>", line 1, in <module>
    d.popitem()
KeyError: 'popitem(): dictionary is empty'
```

`d.update(obj)`

```python
>>> d1 = {'a': 10, 'b': 20, 'c': 30}
>>> d2 = {'b': 200, 'd': 400}

>>> d1.update(d2)
>>> d1
{'a': 10, 'b': 200, 'c': 30, 'd': 400}
```

```python
>>> d1 = {'a': 10, 'b': 20, 'c': 30}
>>> d1.update([('b', 200), ('d', 400)])
>>> d1
{'a': 10, 'b': 200, 'c': 30, 'd': 400}
```

```python
>>> d1 = {'a': 10, 'b': 20, 'c': 30}
>>> d1.update(b=200, d=400)
>>> d1
{'a': 10, 'b': 200, 'c': 30, 'd': 400}
```

`d.copy()`返回一个dict的shallow copy

```python
>>> d1 = {'a': 10, 'b': 20, 'c': 30}
>>> d2 = d1.copy()
>>> d2.pop('a')
>>> d1
{'a': 10, 'b': 200, 'c': 30, 'd': 400}
>>> d2
{'b': 200, 'c': 30, 'd': 400}
```

