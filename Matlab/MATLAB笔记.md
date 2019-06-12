unzip xxx.zip 解压缩指令

pause()

sprintf() 字符串格式化输出

fprintf() 字符串输出

X^2是矩阵的幂，而不是X中每个元素的平方

size()

matlab中的点运算也支持广播特性。

附加列用[a b]

附加行用[a; b]

fminuc()可以用来计算函数最优的自变量值，需要提供初始值

> 首先使用optimeset('GradObj', 'on', 'MaxIter', 400);设置参数
>
> [theta, cost] = fminunc(@(t)(costFunction(t, X, y)（计算损失函数和梯度的函数）), initial_theta（初始参数）, options（迭代的参数）);

...可以换行

contour()画等高线

max(A)返回列最大值的行向量

max(A, [], DIM) 可以设置返回最大值的维度