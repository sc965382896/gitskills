# python科学计算包——Numpy

[TOC]

## 一 Ndarray 对象

ndarray 对象是用于存放同类型元素的多维数组。索引从**零**开始。

ndarray 内部由以下内容组成：

* 一个指向数据（内存或内存映射文件中的一块数据）的指针。
* 数据类型或 dtype，描述在数组中的固定大小值的格子。
* 一个表示数组**形状**（shape）的**元组**，表示各维度的大小。
* 一个跨度元组（stride），其中的整数指的是为了前进到当前维度下一个元素需要"跨过"的**字节数**。

创建ndarray只需要使用NumPy中的array函数：

```python
numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
```

参数说明：

| 名称   | 描述                                                         |
| :----- | :----------------------------------------------------------- |
| object | 数组或嵌套的数列                                             |
| dtype  | 数组元素的数据类型，如int，float，complex                    |
| copy   | 对象是否需要复制，如True，False                              |
| order  | 创建内存中数组的样式，C为行方向，F为列方向，A为任意方向（默认） |
| subok  | 默认返回一个与基类类型一致的数组                             |
| ndmin  | 指定生成数组的最小维数，1是一维，2是二维，依次类推           |

> 导入numpy函数时通常命名为np：
>
> ```python
> import numpy as np
> ```

## 二 NumPy 数据类型

### 2.1 常见的NumPy数据类型

[常见的数据类型](http://www.runoob.com/numpy/numpy-dtype.html)

### 2.2 数据类型对象（dtype）

数据类型对象用来描述与数组对应的内存区域如何使用。

dtype 对象的构造语法：

> ```python
> numpy.dtype(object, align, copy)
> ```
>
> * object：要转换为的数据类型对象。
> * align：如果为 true，填充字段使其类似 C 的结构体。
> * copy - 复制 dtype 对象 ，如果为 false，则是对内置数据类型对象的引用。

创建dtype对象：

> ```python
> import numpy as np
> dt = np.dtype(np.int32)
> print(dt)
> ```
>
> 输出为：
>
> ```python
> int32
> ```

创建结构化数据类型：

> ```python
> import numpy as np
> dt = np.dtype([('age',np.int8)])
> print(dt)
> ```
>
> 输出为：
>
> ```python
> [('age', 'i1')]
> ```

将数据类型对象应用于ndarray对象：

> ```python
> import numpy as np
> dt = np.dtype([('age',np.int8)]) 
> a = np.array([(10,),(20,),(30,)], dtype = dt) 
> print(a)
> ```
>
> 输出为：
>
> ```python
> [(10,) (20,) (30,)]
> ```

可以使用类型字段名存取对应列：

> ```python
> import numpy as np
> dt = np.dtype([('age',np.int8)]) 
> a = np.array([(10,),(20,),(30,)], dtype = dt) 
> print(a['age'])
> ```
>
> 输出为：
>
> ```python
> [10 20 30]
> ```

结构化类型的综合应用：

> ```python
> import numpy as np
> student = np.dtype([('name','S20'), ('age', 'i1'), ('marks', 'f4')]) 
> a = np.array([('abc', 21, 50),('xyz', 18, 75)], dtype = student) 
> print(a)
> ```
>
> 输出为：
>
> ```python
> [('abc', 21, 50.0), ('xyz', 18, 75.0)]
> ```

每个内建类型都有一个唯一定义它的字符代码，如dtype = 'f'为浮点型

内建类型字符代码如下：

| 字符 | 对应类型              |
| :--- | :-------------------- |
| b    | 布尔型                |
| i    | (有符号) 整型         |
| u    | 无符号整型 integer    |
| f    | 浮点型                |
| c    | 复数浮点型            |
| m    | timedelta（时间间隔） |
| M    | datetime（日期时间）  |
| O    | (Python) 对象         |
| S, a | (byte-)字符串         |
| U    | Unicode               |
| V    | 原始数据 (void)       |

## 三 创建nparray

```
a = np.array([1, 2, 3])
print(a.shape)      # prints '(3, )'

a = np.zeros((2,2))   # Create an array of all zeros
print(a)              # Prints "[[ 0.  0.]
                      #          [ 0.  0.]]"
                      
b = np.ones((1,2))    # Create an array of all ones
print(b)              # Prints "[[ 1.  1.]]"

c = np.full((2,2), 7)  # Create a constant array
print(c)               # Prints "[[ 7.  7.]
                       #          [ 7.  7.]]"
                       
d = np.eye(2)         # Create a 2x2 identity matrix
print(d)              # Prints "[[ 1.  0.]
                      #          [ 0.  1.]]"
                      
e = np.random.random((2,2))  # Create an array filled with random values
print(e)                     # Might print "[[ 0.91940167  0.08143941]
                             #               [ 0.68744134  0.87236687]]"
```

## 数组索引和切片

