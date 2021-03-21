# Exceptions

## 1.语法错误与异常

python程序在执行的过程中，如果遇到错误，python程序的执行会马上停止。在python中，错误可以分为语法错误和异常。语法错误是指所写的语句违反了python的语法规则；而异常则是语法正确的python语句导致的程序运行时出现错误。

python中内置了许多种不同类型的异常，用户也可以自已自定义异常的类型。

## 2.主动抛出异常，raise与assert

如果某一条件发生的时候，我们想立即终止程序的运行，可以利用如下语句：

```python
raise Exception("There is a exception")
```

我们也可以在这一条件之前加上assert，当该条件判定为真时，程序正常运行，当该条件判定为假时，抛出

```python
AsserionError
```

异常，如以下的代码所示：

```python
import sys
assert ('linux' in sys.platform)
```

## 3.异常处理，try，except，else和finally

![image-20210321133410258](C:\Users\YAO\AppData\Roaming\Typora\typora-user-images\image-20210321133410258.png)

python的异常处理机制是，当`try`中的代码执行出现异常时，程序立即进入`except`代码块中执行相应的异常处理代码。执行完`except`中的代码后，程序继续执行，不会中止（除非`except`中有`raise`或`assert`语句）。

可以通过在`except`中指定异常的类型和使用多条`except`语句实现对异常的精细化处理。如：

```python
try:
	#code_block1
	#code_block2
except KeyError as ke:
	#handle1
	print(ke)
except ValueErroe as ve:
	#handle2
	print(ve)
```

当程序出现第一个异常时，即进入对应的`except`代码块中，即只会执行一次`except`。注意到，未在`except`中指明的异常将不会处理，此时程序将停止运行。

`else`中的代码只有在`try`中的代码没有出现异常时才会执行。

`finally`中的代码则是不管有没有异常出现时都要执行。

## 4. Best practices

永远不要使用如下所示的异常处理方式：

```python
try：
	do_something()
except:
	pass

try:
	do_something()
except Exception:
	pass
```

以上的处理方式会将原本容易发现的异常悄悄地吞噬，导致bug出现时难以找到真正的原因。

对策是只去捕获较为具体的意料之中会出现的异常类型，让其他意料之外的异常显示地终止程序运行。如：

```python
try：
	do_something()
except ValueError:
	pass
```

如果必须去捕获所有的异常类型，那么每次异常的捕获都必须将函数调用栈的追踪信息写入log或其他文件中。

如果使用python的`logging`模块，那么可以用如下的方式自动记录异常信息：

```python
import logging
try:
	do_something()
except Exception as ex:
	logging.exception('Caught an error')
```

如果没有使用python的`logging`模块，那么可以使用如下的方式，直接获取并生成异常的追踪信息。如：

```python
import traceback

def log_traceback(ex):
	tb_lines = traceback.format_exception(ex.__class__, ex, ex.__traceback__)
	tb_text = ''.join(tb_lines)
	#implement a ExceptionLogger class
	exception_logger.log(tb_text)
	
try:
	do_something()
except Exception as ex:
	log_traceback(ex)
```

### 参考：

[[Python Exceptions: An Introduction – Real Python](https://realpython.com/python-exceptions/)](https://realpython.com/python-exceptions/)

[[The Most Diabolical Python Antipattern – Real Python](https://realpython.com/the-most-diabolical-python-antipattern/)](https://realpython.com/the-most-diabolical-python-antipattern/)





