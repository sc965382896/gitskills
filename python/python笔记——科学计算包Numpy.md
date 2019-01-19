# python科学计算包——Numpy

[TOC]

## 第1部分 基础类型（array）

**array**，也就是数组，是Numpy中最基础的数据结构，关键属性是**维度**和**元素类型**。

```python
import numpy as np          #常用的重命名方法

a = [1, 2, 3, 4]
b = np.array(a)             # 定义一个数组
type(b)                     # 可以通过type()查看b的数据类型

b.shape                     # b的形状，(4,)
b.argmax()                  # b中最大值所对应的索引
b.max()                     # b中的最大值
b.mean()                    # b中元素的均值

c = [[1, 2], [3, 4],[5,6]]	    # 定义一个二维列表
d = np.array(c)         	# 定义一个二维numpy数组d
d.shape                   	# d的形状，2列2行d(2, 2)
d.size                   	# d的大小，4
d.max(axis=0)            	# 找维度0，也就是最后一个维度上的最大值，array([3, 4])
d.max(axis=1)            	# 找维度1，也就是倒数第二个维度上的最大值，array([2, 4])
d.mean(axis=0)          	# 找维度0，也就是最后一个维度上的均值，array([ 2.,  3.])
d.flatten()              	# 展开一个numpy数组为1维数组，array([1, 2, 3, 4])
np.ravel(c)                 # 展开一个可以解析的结构为1维数组，array([1, 2, 3, 4])


```

