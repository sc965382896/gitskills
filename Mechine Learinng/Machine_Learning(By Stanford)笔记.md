# Machine Learning(By Stanford)

[TOC]

## 1 Introduction

### 1.1 Definition

* Informal Definition: the field of study that gives computers the ability to learn without being explicitly programmed.
* Modern definition: A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E.

![learning_process](./images/learning_process.png)

### 1.2 Supervised Learning

In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a **relationship** between the input and the output.

**Two categories**:

* Regression problem: To predict results within a **continuous** output, meaning that we are trying to map input variables to some **continuous function**.

* assification problem: To predict results in a **discrete** output. In other words, we are trying to map input variables into **discrete categories**.

### 1.3 Unsupervised Learning

Unsupervised learning allows us to approach problems with little or no idea what our results should look like. We can derive this structure by **clustering** the data based on relationships among the variables in the data.

**Example:**

* **Clustering**: Take a collection of 1,000,000 different genes, and find a way to automatically group these genes into groups that are somehow similar or related by different variables, such as lifespan, location, roles, and so on.

* **Non-clustering**: The "Cocktail Party Algorithm", allows you to find structure in a chaotic environment. 

## 2 Linear Regression

**线性回归（单变量）**的表示方式：

$$
h_\theta(x) = \theta_0+\theta_1x\tag{2.1}
$$

多变量的表示方式：
$$
h_\theta(x)
=\left[ \begin{array}{ccc}
\theta_0\quad\theta_1\quad...\quad\theta_n\end{array} 
\right] 
\left[ \begin{array}{ccc}
x_0\\
x_1\\
...\\
x_n
\end{array}\right]
=\theta^Tx\tag{2.2}
$$


### 2.1 Cost Function

We can measure the accuracy of our hypothesis function by using a **cost function**.

This takes an **average difference** (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's and the actual output y's.

**损失函数Cost Function**的表示方式:
$$
J(\theta_0,\theta_1)=\cfrac{1}{2m}\sum_{i=1}^m(\hat y^{(i)}-y^{(i)})^2=\cfrac{1}{2m}\sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})^2\tag{2.3}
$$
**Target**: minimize the cost function.

### 2.2 Gradient Descent

$$
\theta_j:=\theta_j-\alpha\cfrac{\partial}{\partial\theta_j}J(\theta_0,\theta_1)\tag{2.4}
$$

对于单变量的线性回归：
$$
\begin{split}
\mathrm{repeat until convergence: \{}\qquad\qquad\qquad\qquad\qquad\qquad\\
\theta_0:=\theta_0-\alpha\cfrac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})\\
\theta_1:=\theta_1-\alpha\cfrac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})x^{(i)}_1\\
\mathrm{\}}\qquad\qquad\qquad\qquad\qquad\qquad
\end{split}
$$
对于多变量的线性回归：
$$
\begin{split}
\mathrm{repeat\ until\ convergence: \{}\qquad\qquad\qquad\qquad\qquad\qquad\\
\theta_j:=\theta_j-\alpha\cfrac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})x^{(i)}_j\qquad\mathrm{for\quad j:=0...n}\\
\mathrm{\}}\qquad\qquad\qquad\qquad\qquad\qquad
\end{split}
$$

**在实际应用中两种加速梯度下降的方法**：

* feature scaling：将输入值除以输入量的范围（最大值减最小值）。

* mean normalization：将输入值减去输入量的平均值，然后除以范围或者标准差。
  $$
  x_i:=\frac{x_i-\mu_i}{s_i}\tag{2.5}
  $$

  > 之后进行预测时，需要对输入值进行同样的处理。

学习率对梯度下降的影响：

* If $\alpha$ is too small: slow convergence.
* If $\alpha$ is too large: ￼may not decrease on every iteration and thus may not converge.

### 2.3 Features and Polynomial Regression

We can improve our features and the form of our hypothesis function in a couple different ways.

> 例如将两个特征相乘得到一个新的特征。

**Polynomial Regression**

Our hypothesis function need not be linear (a straight line) if that does not fit the data well.
$$
\begin{split}
h_\theta(x) &= \theta_0+\theta_1x_1+\theta_2x_1^2\\h_\theta(x) &= \theta_0+\theta_1x_1+\theta_2\sqrt {x_1}
\end{split}\tag{2.6}
$$

### 2.4 Normal Equation

The **normal equation** formula is given below:
$$
\theta = (X^TX)^{-1}X^Ty\tag{2.7}
$$

| **Gradient Descent**       | **Normal Equation**                           |
| -------------------------- | --------------------------------------------- |
| Need to choose alpha       | No need to choose alpha                       |
| Needs many iterations      | No need to iterate                            |
| $O(kn^2)$                  | $O(n^3)$, need to calculate inverse of $X^TX$ |
| Works well when n is large | Slow if n is very large                       |

**Normal Equation Noninvertibility**

if$X^TX$is noninvertible, the common causs might be having:

* Redundant features, where two features are very closely related (i.e. they are linearly dependent)
* Too many features (e.g. m ≤ n). In this case, delete some features or use "regularization"

### 2. 5 Regularized Linear Regression

**Cost Function:** 
$$
J(\theta_0,\theta_1)=\cfrac{1}{2m}\sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})^2+\cfrac{\lambda}{2m}\sum^n_{j=1}\theta_j^2\tag{2.8}
$$
**Gradient Descent:** 
$$
\cfrac{\partial J(\theta)}{\partial \theta_0}=\cfrac{1}{m}\sum^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})x_0^{(i)}\\
\cfrac{\partial J(\theta)}{\partial \theta_j}=\cfrac{1}{m}\sum^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})x_j^{(i)}+\cfrac{\lambda}{m}\theta_j\tag{2.9}
$$
**Normal Equation:**
$$
\theta = (X^TX+\lambda\cdot L)^{-1}X^Ty\\
where\ L = 
\left[\begin{array}{ccc}
0\\
&1\\
&&\ddots\\
&&&1\\
\end{array}\right]\tag{2.10}
$$

## 3 Logistic Regression

### 3.1 Hypothesis Representation

Our new form uses the "Sigmoid Function," also called the "Logistic Function":
$$
\begin{split}
h_\theta(x) &= g(\theta^Tx)\\
z &= \theta^Tx\\
g(z) &= \cfrac{1}{1+e^{-z}}
\end{split}\tag{3.1}
$$

> 这里的$h_\theta(x)$代表的是输出为1的概率。

### 3.2 Cost Function

We can fully write out our entire cost function as follows:
$$
J(\theta)=-\cfrac{1}{m}\sum_{i=1}^m[y^{(i)}\log(h_\theta(x^{(i)}))+(1-y^{(i)})log(1-h_\theta(x^{(i)}))]\tag{3.2}
$$
We can work out the derivative part using calculus to get:
$$
Repeat\{ \qquad\qquad\qquad\qquad\qquad\qquad\\
    \theta_j:=\theta_j-\cfrac{\alpha}{m}\sum^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})x^{(i)}_{j}\\
\}\qquad\quad\qquad\qquad\qquad\qquad\qquad\qquad\tag{3.3}
$$

> 这里求导的时需要注意的一点：$\log(1-h_\theta(x))$中的“-”号

### 3.3 Overfitting

![Overfitting and Underfitting](.\images\过拟合欠拟合.png)

There are two main options to address the issue of overfitting: 

1. Reduce the number of features:
   - Manually select which features to keep.
   - Use a **model selection algorithm**.
2. Regularization
   * Keep all the features, but reduce the **magnitude** of parameters $\theta_j$ .
   * **Regularization** works well when we have a lot of slightly useful features.

### 3.4 Regularized Logistic Regression

**Cost Function:** 
$$
J(\theta)=-\cfrac{1}{m}\sum_{i=1}^m[y^{(i)}\log(h_\theta(x^{(i)}))+(1-y^{(i)})log(1-h_\theta(x^{(i)}))]+\cfrac{\lambda}{2m}\sum^n_{j=1}\theta_j^2\tag{3.4}
$$
**Gradient Descent:**
$$
\cfrac{\partial J(\theta)}{\partial \theta_0}=\cfrac{1}{m}\sum^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})x_0^{(i)}\\
\cfrac{\partial J(\theta)}{\partial \theta_j}=\cfrac{1}{m}\sum^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})x_j^{(i)}+\cfrac{\lambda}{m}\theta_j\tag{3.5}
$$

## 4 Neural Network

### 4.1 simplistic representation

$$
\left[ \begin{array}{ccc}
x_0\\
x_1\\
x_2
\end{array} 
\right]
\rightarrow
[\quad]
\rightarrow
h_\theta(x)
\tag{3.6}
$$

对于含有一层隐含层函数，可表示为：
$$
\left[ \begin{array}{ccc}
x_0\\
x_1\\
x_2
\end{array} 
\right]
\rightarrow
\left[ \begin{array}{ccc}
a_1^{2}\\
a_2^{2}\\
a_3^{2}
\end{array} 
\right]
\rightarrow
h_\theta(x)
\tag{3.7}
$$
各个激活节点表示方式如下：
$$
\begin{split}
a_1^{2} &= g(\Theta_{10}^{1}x_0+\Theta_{11}^{1}x_1+\Theta_{12}^{1}x_2+\Theta_{13}^{1}x_3) \\
a_2^{2} &= g(\Theta_{20}^{1}x_0+\Theta_{21}^{1}x_1+\Theta_{22}^{1}x_2+\Theta_{23}^{1}x_3) \\
a_3^{2} &= g(\Theta_{30}^{1}x_0+\Theta_{31}^{1}x_1+\Theta_{32}^{1}x_2+\Theta_{33}^{1}x_3)\\
h_{\Theta}(x)=a_1^{(1)}&=g(\Theta_{10}^{2}a_0^{(2)}+\Theta_{11}^{2}a_1^{(2)}+\Theta_{12}^{2}a_2^{(2)}+\Theta_{13}^{2}a_3^{(2)}) \\
\end{split}\tag{3.8}
$$

> * $a_i^{(j)}$："activation" of unit *i* in layer *j*
> * $\Theta^{(j)}$：matrix of weights controlling function mapping from layer *j* to layer *j*+1

### 4.2 Cost Function

首先定义如下变量：

* $L$：total number of layers in the network
* $s_l$：number of units (not counting bias unit) in layer l
* $K$：number of output units/classes

损失函数（Cost Function）可表示为：
$$
J(\Theta)
=
-\cfrac{1}{m}\sum_{i=1}^m\sum_{k=1}^K[y_k^{(i)}\log((h_\theta(x^{(i)}))_k)+(1-y_k^{(i)})log(1-(h_\theta(x^{(i)}))_k)] + 
\cfrac{\lambda}{2m}\sum^{L-1}_{l=1}\sum_{i=1}^{s_l}\sum_{j=1}^{s_{l+1}}(\Theta_{j,i}^{(l)})^2
\tag{3.9}
$$
Note: 

* the double sum simply adds up the logistic regression costs calculated for each cell in the output layer

* the triple sum simply adds up the squares of all the individual Θs in the entire network.
* the i in the triple sum does **not** refer to training example i

### 4.3 Backpropagation Algorithm

Given training set ${(x^{(1)},y^{(1)})⋯(x^{(m)},y^{(m)})}$

* Set $\Delta_{i,j}^{(l)}:=0$for all (l,i,j), (hence you end up having a matrix full of zeros)

For training example t =1 to m:

1. Set $a^{(1)}=x^{(t)}$

2. Perform forward propagation to compute $a^{(l)}$ for l=2,3,...,L

   ![](.\images\Gradient computation.png)

3. Using $y^{(t)}$, compute  $\delta^{(L)} = a^{(L)} - y^{(t)}$

4. Compute $δ^{(L−1)},\delta^{(L-2)},...,\delta^{(2)}$ using $\delta^{(l)}=((\Theta^{(l)})^T\delta^{(l+1)}.*a^{(l)}.*(1-a^{(l)}))$

5. $\Delta_{i,j}^{(l)}:=\Delta_{i,j}^{(l)}+a_j^{(l)}\delta_i^{(l+1)}$ or with vectorization, $ \Delta^{(l)} := \Delta^{(l)} + \delta^{(l+1)}(a^{(l)})^T$

Hence we update our new $\Delta$ matrix.

* $D_{i,j}^{(l)}:=\cfrac{1}{m}(\Delta_{i,j}^{(l)}+\lambda\Theta_{i,j}^{(l)})$, if $j\neq 0$.
* $D_{i,j}^{(l)}:=\cfrac{1}{m}(\Delta_{i,j}^{(l)})$, if$j=0$

### 4.4 Gradient Checking

Gradient checking will assure that our backpropagation works as intended. We can approximate the derivative of our cost function with:
$$
\cfrac{\part}{\part \Theta_j}J(\Theta)\approx\cfrac{J(\Theta+\epsilon)-J(\Theta-\epsilon)}{2\epsilon}
$$
With multiple theta matrices, we can approximate the derivative **with respect to** $\Theta_j$ as follows:
$$
\cfrac{\part}{\part \Theta_j}J(\Theta)\approx\cfrac{J(\Theta_1,\ldots,\Theta_j+\epsilon,\ldots,\Theta_n)-J(\Theta_1,\ldots,\Theta_j-\epsilon,\ldots,\Theta_n)}{2\epsilon}
$$

### 4.5 Random Initialization

Initializing all theta weights to zero does not work with neural networks. When we backpropagate, all nodes will update to the same value repeatedly. Instead we can randomly initialize our weights for our $\Theta$ matrices using the following method:

Initialize each $\Theta_{ij}^{(l)}$ to a random value in $[-\epsilon, \epsilon]$

* $\Theta^{(l)}:=rand(s_{l+1},s_l)*(2*\epsilon)-\epsilon$ 

## 5 Evaluating a Learning Algorithm

### 5.1 Model Selection and Train/Validation/Test Sets

One way to break down our dataset into the three sets is:

* Training set: 60%
* Cross validation set: 20%
* Test set: 20%

选择不同的多项式次数d时，分别计算不同集合的误差值：

1. 用训练集训练权重
2. 用验证集选择多项式次数d
3. 用测试集估计泛化误差

### 5.2 Bias vs. Variance

* We need to distinguish whether **bias** or **variance** is the problem contributing to bad predictions.
* High bias is underfitting and high variance is overfitting. Ideally, we need to find a golden mean between these two.

The training error will tend to **decrease** as we increase the degree d of the polynomial.

At the same time, the cross validation error will tend to **decrease** as we increase d up to a point, and then it will **increase** as d is increased, forming a convex curve.

![bias vs. variance](.\images\bias vs variance.png)

**Regularization and Bias/Variance**

1. 创建一系列$\lambda$值
2. 创建一系列不同次数的多项式模型
3. 在所有的$\lambda$上进行迭代学习$\Theta$
4. 在验证集上使用学习的$\Theta$计算不含正则化项或$\lambda=0$情况下的$J_{CV}(\Theta)$
5. 选择在验证集上产生最小偏差的参数组合
6. 在测试集上使用最佳参数组合检查是否该模型是否具有好的泛化。

### 5.3 Learning Curves

**Experiencing high bias:**

* **Low training set size**: causes $J_{train}(\Theta)$ to be low and $J_{CV}(\Theta)$ to be high.

* **Large training set size**: causes both $J_{train}(\Theta)$ and $J_{CV}(\Theta)$ to be high with $J_{train}(\Theta)\approx J_{CV}(\Theta)$.

![high bias](.\images\high bias.png)

**Experiencing high variance:**

* **Low training set size**: causes $J_{train}(\Theta)$ to be low and $J_{CV}(\Theta)$ to be high.

* **Large training set size**: $J_{train}(\Theta)$ increases with training set size and $J_{CV}(\Theta)$ continues to decrease without leveling off. Also, $J_{train}(\Theta)< J_{CV}(\Theta) $ but the difference between them remains significant.

![high variance](.\images\high variance.png)

Our decision process can be broken down as follows:

- **Getting more training examples:** Fixes high variance

- **Trying smaller sets of features:** Fixes high variance

- **Adding features:** Fixes high bias

- **Adding polynomial features:** Fixes high bias

- **Decreasing λ:** Fixes high bias

- **Increasing λ:** Fixes high variance.

**Error metrics for skewed classes**

| Predicted class/Actual class | 1              | 0              |
| :--------------------------- | -------------- | -------------- |
| **1**                        | True positive  | False positive |
| **0**                        | False negative | True negative  |

**Precision**(预测为真正确的占所有预测为真的比重)
$$
P = \cfrac{True\:positive}{True \:pos+False\:pos}\tag{5.1}
$$
**Recall**(预测为真正确的占所有真正为真的比重)
$$
R = \cfrac{True\:positive}{True\:pos+False \:neg}\tag{5.2}
$$
使用下述公式比较：
$$
2\cfrac{PR}{P+R}\tag{5.3}
$$
