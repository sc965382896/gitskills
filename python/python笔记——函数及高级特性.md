# python笔记——函数及高级特性

[TOC]

## 1 函数

### 1.1 定义函数

* 定义函数的一般格式：

		def 函数名(参数列表)：
	​		函数体

* 函数内部可不包含return语句，但仍会返回None。

### 1.2 调用函数

* 调用格式为：函数名(参数列表)

### 1.3 函数的参数

#### 1.3.1 参数传递

* 可变对象与不可变对象：
	* 不可变对象：如整型、字符串、元组。调用fun(a)时，传递的是a的值，在函数内部修改a的值，修改的是其的一个副本，不会影响a本身。
	* 可变对象：如列表、字典。调用fun(la)时，是将la本身传过去，函数内部修改la的值也会影响外部的la本身。

#### 1.3.2 参数

> 函数参数顺序：位置参数（也称必需参数、必选参数）、默认参数（如果其后还包含其他参数，则调用函数时会按顺序传入参数）、可变参数、命名关键字参数、关键字参数。

1. 位置参数，传入参数时按照顺序传入，并且缺一不可。
2. 默认参数，可以不按顺序传入参数，传入参数时需要注意的情况有：
   * 可以使用顺序或者关键字输入参数。
   * 使用关键字传入参数时必须在位置参数之后，包括可变参数。
   * 可变参数可以在默认参数之前，但此时只能用关键字传入参数。

  > 默认参数必须指向不变对象。

3. 可变参数，使用*接收多个参数，传入一个元组。

4. 关键字参数，使用**接收多个含参数名的参数，传入一个字典。

5. 命名关键字参数，用于限制关键字参数的参数名，输入参数时必须包含参数名，可以使用缺省值，调用时可不传入该参数。

  > 如果没有可变参数，必须加入*作为分隔符。

### 1.3.3 作用域

在函数中可以直接访问全局变量，要想给全局变量赋值，需要使用global在函数中声明这是一个全局变量（可变对象可以直接进行赋值）。

当局部变量与全局变量名称相同时，会被局部变量覆盖。

可以使用globals()获取全局变量的字典来访问被覆盖的全局变量。

## 2 函数式编程

### 2.1 高阶函数

以函数作为输入参数的函数称为高阶函数。

#### 2.1.1 zip

* zip()接收多个Iterable，返回Iterator。功能是将多个序列作为元组的元素缝合在一起，序列的元素个数可以不一致，以最短的为准。**可以实现同时遍历多个序列。**

#### 2.1.2 map/reduce

* map()接收两个参数，一个函数，一个Iterable，返回Iterator。功能为将输入的函数依次作用到序列中的各个元素上面。
* reduce()接收两个参数，一个函数（参数个数必须为2），一个Iterable，返回Iterator，将函数作用在序列上，并将结果与下个元素作为参数做累积计算。

#### 2.1.3 filter

* filter()接收两个参数，一个函数，一个Iterable，返回Iterator。功能是将函数依次作用在序列的元素上，保留返回值为True的元素。

#### 2.1.4 sorted

* sorted()接收一个序列对其进行排序，不会修改原序列，会返回一个排序后的序列。通过key参数输入函数对序列进行预处理后排序，通过reverse参数进行反向排序。

#### 2.1.5 reversed

* reversed()接收一个序列对其进行反转，不会改变原序列，返回一个反转后的序列。**可以实现对序列反向遍历**。

### 2.2 返回函数

高阶函数不仅可以接收函数作为参数，也可以把函数作为结果返回。

**返回闭包时牢记一点：返回函数不要引用任何循环变量，或者后续会发生变化的变量。**

```python
def count():
	def f(j):
  		def g():
        	return j*j
    	return g
	fs = []
	for i in range(1, 4):
    	fs.append(f(i))
	return fs
```
结果如下：

	>>> f1, f2, f3 = count()  
	>>> f1()
	1
	>>> f2()
	4
	>>> f3()
	9

原因就在于返回的函数引用了变量i，但它并非立刻执行。

### 2.3 匿名函数

匿名函数lambda可以用简短的表达式描述一个函数，可以没有名字。
格式为：

```python
lambda x,y,...: f(x, y, ...)
```

### 2.4 装饰器

用于在代码运行期间动态增加功能。

```python
import functools

def log(func):
	@functools.wraps(func) 
	def wrapper(*args, **kw):
		print('call %s():' % func.__name__)
		return func(*args, **kw)
	return wrapper
```

借助@语法将其置于函数定义处：

```python
@log
def now():
	pass
```
这种写法相当于：

```python
now = log(now)
```

如果需要输入参数，则可以采用三层嵌套的装饰器：

```python
import functools

	def log(text):
		def decorator(func):
  			@functools.wraps(func)
    		def wrapper(*args, **kw):
        		print('%s %s():' % (text, func.__name__))
        	return func(*args, **kw)
    	return wrapper
	return decorator
```

### 2.5 偏函数

使用functools模块中的.partial方法可以将函数的某些参数重新设置默认值，并返回一个新的函数。

```python
import functools
int2 = functools.partial(int, base=2)
```

### 2.6 闭包函数

```python
def mutiplier(factor):
	def multiplyByFactor(number):
		return number * factor
	return multiplyByFactor
```

函数multiplier返回一个函数，这个函数包含了multiplier的局部作用域，称为**闭包**。

要想给外部作用域中变量赋值，可以使用nonlocal。

### 2.7 递归

参考：[写递归函数的正确思维方法](https://blog.csdn.net/doncoder/article/details/79182542)

递归的定义：当函数直接或者间接调用自己时，则发生了递归。

递归的正确理解：

1. 当n=0, 1的时候, 结果正确.
2. 假设函数对于n是正确的, 函数对n+1结果也正确.
   如果这两点是成立的，我们知道这个函数对于所有可能的n都是正确的。

如何一个问题的递归算法？

1. 你必须要示范如何解决问题的一般情况, 通过将问题切分成有限小并更小的子问题.
2. 你必须要示范如何通过有限的步骤, 来解决最小的问题(基本用例).
   如果这两件事完成了, 那问题就解决了. 因为递归每次都将问题变得更小, 而一个有限的问题终究会被解决的, 而最小的问题仅需几个有限的步骤就能解决.

## 3 高级特性

### 3.1 列表推导式

类似如下形式的表达式：

```python
[x * x for x in range(1,11)]
```

返回值为列表。

* 列表推导式嵌套，由外向内生成列表：

  ```python
  matrix = [
  ...     [1, 2, 3, 4],
  ...     [5, 6, 7, 8],
  ...     [9, 10, 11, 12],
  ... ]
  
  [[row[i] for row in matrix] for i in range(4)]
  ```

  结果为：`[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]`.

### 3.2 生成器

* 生成器的创建方法：
	1. 将列表推导式中的[]换成()；
	2. 将函数中的return替换成yield。

* 调用方式：
	1. 使用for循环进行遍历；
	2. next()函数，获取下一个值；
	3. 方法.send()，向断点传送一个值，同时获取下一个值。

> 每次返回一个值后，生成器会保存一个断点，下次唤醒时从断点处执行。


### 3.3 迭代器

实现了__ietr()__方法的是可迭代对象，实现了__next__()方法的是迭代器。__iter__()返回对象本身，__next__()返回各个元素的值。

* list、tuple、dict、str等都是可迭代对象，生成器是迭代器，使用函数iter()可以获得可迭代对象的迭代器。

> for...in...循环的本质： 
> 先通过iter()函数获取可迭代对象 Iterable 的迭代器，然后对获取到的迭代器不断调用 next() 方法来获取下一个值并将其赋值给 item，当取出所有的值后，for循环会捕获异常StopIteration然后结束遍历。
