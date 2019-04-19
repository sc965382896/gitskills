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
\theta_0:=\theta_0-\alpha\cfrac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)}-y^{(i)})\\
\theta_1:=\theta_1-\alpha\cfrac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)}-y^{(i)})\\
\mathrm{\}}\qquad\qquad\qquad\qquad\qquad\qquad
\end{split}
$$
对于多变量的线性回归：
$$
\begin{split}
\mathrm{repeat until convergence: \{}\qquad\qquad\qquad\qquad\qquad\qquad\\
\theta_i:=\theta_i-\alpha\cfrac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)}-y^{(i)})\qquad\mathrm{for\quad j:=0...n}\\
\mathrm{\}}\qquad\qquad\qquad\qquad\qquad\qquad
\end{split}
$$

在实际应用中两种加速梯度下降的方法：

* feature scaling：将输入值除以输入量的范围（最大值减最小值）。

* mean normalization：将输入值减去输入量的平均值，然后除以范围或者标准差。
  $$
  x_i:=\frac{x_i-\mu_i}{s_i}\tag{2.5}
  $$

  > 之后进行预测时，需要对输入值进行同样的处理。

学习率对梯度下降的影响：

* If $\alpha$ is too small: slow convergence.

* If $\alpha$ is too large: ￼may not decrease on every iteration and thus may not converge.

## 3 Logistic Regression