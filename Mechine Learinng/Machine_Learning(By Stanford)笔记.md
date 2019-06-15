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
J(\theta)=\cfrac{1}{m}=\sum_{i=1}^m[y^{(i)}\log(h_\theta(x^{(i)}))+(1-y^{(i)})log(1-h_\theta(x^{(i)}))]\tag{3.2}
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

**simplistic representation**
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
