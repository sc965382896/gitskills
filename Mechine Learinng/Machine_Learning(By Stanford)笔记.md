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

### 2.1 Cost Function

We can measure the accuracy of our hypothesis function by using a **cost function**.

This takes an **average difference** (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's and the actual output y's.

**损失函数Cost Function**的表示方式:
$$
J(\theta_0,\theta_1)=\frac{1}{2m}\sum_{i=1}^m(\hat y^{(i)}-y^{(i)})^2=\frac{1}{2m}\sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})^2\tag{2.2}
$$
**Target**: minimize the cost function.

### 2.2 Gradient Descent

