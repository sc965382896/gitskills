[TOC]

# 1 公式的插入、编号、对齐

## 1.1 公式的插入

### 1.1.1 行内公式

* **语法：**\$数学公式\$

* **示例：**

  ```
  一元二次方程组$ax^2+bx+c=0$
  ```

* **显示：**

  一元二次方程组$ax^2+bx+c=0$

### 1.1.2 块级公式

- **语法：**>'空格'\$$数学公式\$\$

- **示例：**

  ```
  一元二次方程$$ax^2+bx+c=0$$
  ```

- **显示：**

  > 一元二次方程组
  >
  > $$ax^2+bx+c=0$$

## 1.2 公式的编号

### 1.2.1 手动编号

* **语法：**数学公式\tag{编号}（后面的内容将省略插入公式的符号）

* **示例：**

  ```
  ax^2+bx+c=0\tag{1.1}
  ```

* **显示：**

  > $$
  > ax^2+bx+c=0\tag{1.1}
  > $$
  >
  > 

### 1.2.2 自动编号

* **语法：**\begin{equation}...\end{equation}（Typora貌似不支持）

* **示例：**

  ```
  \begin{equation}ax^2+bx+c=0\end{equation}
  ```

* **显示：**

  > $$
  > \begin{equation}ax^2+bx+c=0\end{equation}\tag{1}
  > $$

## 1.3 公式的对齐

### 1.3.1 单个公式换行的对齐

* **语法：**使用`split`标签包含公式代码，换行处使用`\\`，使用`&`标识对齐的位置，结束处可以使用`\tag{...}`标签编号。

* **示例：**

  ```
  \begin{split}
  a &= b \\
  c &= d \\
  e &= f 
  \end{split}\tag{1.2}
  ```

* **显示：**

  > $$
  > \begin{split}
  > a &= b \\
  > c &= d \\
  > e &= f 
  > \end{split}\tag{1.2}
  > $$

### 1.3.2 多行独立公式的对齐

* **语法：**使用`equarray*`标签包含公式代码，换行处使用`\\`，使用`$...&`标识对齐的位置，两个`&`之间是对齐的位置，结束处可以使用`\tag{...}`标签编号。

* **示例：**

  ```
  \begin{eqnarray*}
  x^n+y^n &=& z^n \tag{1.3}
  x+y &=& z \tag{1.4}
  \end{eqnarray*}
  ```

* **显示：**

  > $$
  > \begin{eqnarray*}
  > x^n+y^n &=& z^n \tag{1.3} \\
  > x+y &=& z \tag{1.4}
  > \end{eqnarray*}
  > $$

# 2 上下标、占位符、分数表示、矩阵表示

## 2.1 上下标

* 上标符号为`^`，下标符号为`_`。

* 如果上下标中包含多个字符，可以使用`{}`将其包含在内。
* 如果想让左上左下也包含字符，可以使用`\sideset{}{}`

* 特别的，对于**argmax**和**argmin**，可以使用`\mathop`将下标置于下方。

举例：

| 例子                  | 显示                                         |
| --------------------- | -------------------------------------------- |
| x^2_2                 | $x^2_2$                                      |
| y^{15}_{15}           | $y^{15}_{15}$                                |
| \sideset{^1}{}z       | $\sideset{^1}{}z$                            |
| \mathop{\arg\max}_{x} | 只有在块级公式中会显示在argmax下方，显示如下 |

> $$
> \mathop{\arg\max}_{x}
> $$

## 2.2 占位符

| 描述         | 例子       | 显示         |
| ------------ | ---------- | ------------ |
| 两个quad空格 | x \qquad y | $x \qquad y$ |
| 一个quad空格 | x \quad y  | $x \quad y$  |
| 大空格       | x \ y      | $x \ y$      |
| 中空格       | x \: y     | $x \: y$     |
| 小空格       | x \, y     | $x \, y$     |
| 紧贴         | x \\! y    | $x \! y$     |

## 2.3 分数表示

有两种分数的表示方法，分别为`\frac`和`\cfrac`，前者较后者显示时更为紧凑。

| 例子         | 显示           |
| ------------ | -------------- |
| \frac{1}{3}  | $\frac{1}{3}$  |
| \cfrac{1}{4} | $\cfrac{1}{4}$ |

## 2.4 矩阵表示

举例：

```
\left[ \begin{array}{ccc}
1 & 0 & -1\\
1 & 0 & -1\\
1 & 0 & -1
\end{array} 
\right]
```

$$
\left[ \begin{array}{ccc}
1 & 0 & -1\\
1 & 0 & -1\\
1 & 0 & -1
\end{array} 
\right]
$$

\left[`和`\right]`表示左右括号的形式，`[]`可以替换为`{}`、`()`。

`{array}`标签代表之后的符号表示矩阵。

{ccc}表示数据在矩阵中的位置，c为居中，l为靠左，r为靠右。

`&`分隔不同的数据，`\\`表示换行。

# 3 各种运算的表示

## 3.1 四则运算

| 描述   | 例子          | 显示            |
| ------ | ------------- | --------------- |
| 加法   | x+y=z         | $x+y=z$         |
| 减法   | x-y=z         | $x-y=z$         |
| 加减   | x \pm y=z     | $x \pm y=z$     |
| 减加   | x \mp y =z    | $x \mp y =z$    |
| 乘法   | x \times y =z | $x \times y =z$ |
| 点乘   | x \cdot y=z   | $x \cdot y=z$   |
| 星乘   | x \ast y=z    | $x \ast y=z$    |
| 除法   | x \div y=z    | $x \div y=z$    |
| 斜除   | x/y=z         | $x/y=z$         |
| 绝对值 | \|x+y\|       | $|x+y|$         |

## 3.2 高级运算

| 描述       | 例子                                                         | 显示                                                         |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 平均数运算 | \overline{xyz}                                               | $\overline{xyz}$                                             |
| 开平方运算 | \sqrt x                                                      | $\sqrt x$                                                    |
| 开方运算   | \sqrt[3]{x+y}                                                | $\sqrt[3]{x+y}$                                              |
| 对数运算   | \log{x}                                                      | $\log{x}$                                                    |
| 极限运算   | \displaystyle \lim^{x \to \infty}\_{y \to 0}{\frac{x}{y}}\\\\\\lim^{x \to \infty}\_{y \to 0}{\frac{x}{y}} | $\displaystyle \lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}\\\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$ |
| 求和运算   | \displaystyle \sum^{x \to \infty}\_{y \to 0} {\frac{x}{y}}\\\\ \\sum^{x \to \infty}\_{y \to 0}{\frac{x}{y}} | $\displaystyle \sum^{x \to \infty}_{y \to 0} {\frac{x}{y}}\\\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$ |
| 积分运算   | \displaystyle \\int^{\infty}\_{0}{xdx} \\\\\int^{\infty}\_{0}{xdx} | $\displaystyle \int^{\infty}_{0}{xdx} \\\int^{\infty}_{0}{xdx}$ |
| 偏微分运算 | \frac{\partial x}{\partial y}                                | $\frac{\partial x}{\partial y}$                              |

## 3.3 逻辑运算

| 描述       | 例子         | 显示           |
| ---------- | ------------ | -------------- |
| 等于       | x+y=z        | $x+y=z$        |
| 大于       | x+y>z        | $x+y>z$        |
| 小于       | x+y<z        | $x+y<z$        |
| 大于等于   | x+y\geq z    | $x+y\geq z$    |
| 小于等于   | x+y\leq z    | $x+y\leq z$    |
| 不等于     | x+y\neq z    | $x+y\neq z$    |
| 不大于等于 | x+y\ngeq z   | $x+y \ngeq z$  |
| 不小于等于 | x+y\nleq z   | $x+y\nleq z$   |
| 约等于     | x+y\approx z | $x+y\approx z$ |
| 恒等于     | x+y\equiv z  | $x+y\equiv z$  |

## 3.4 集合运算

| 描述       | 代码         | 显示           |
| ---------- | ------------ | -------------- |
| 属于       | \in          | $\in$          |
| 不属于     | \notin       | $\notin$       |
| 子集       | \subset      | $\subset$      |
| 子集       | \supset      | $\supset$      |
| 非子集     | \not \subset | $\not \subset$ |
| 非子集     | \not \supset | $\not \supset$ |
| 真子集     | \subseteq    | $\subseteq$    |
| 真子集     | \supseteq    | $\supseteq$    |
| 非真子集   | \subsetneq   | $\subsetneq$   |
| 非真子集   | \supsetneq   | $\supsetneq$   |
| 并集       | \cup         | $\cup$         |
| 交集       | \cap         | $\cap$         |
| 差集       | \setminus    | $\setminus$    |
| 同或       | \bigodot     | $\bigodot$     |
| 同与       | \bigotimes   | $\bigotimes$   |
| 实数集合   | \mathbb{R}   | $\mathbb{R}$   |
| 自然数集合 | \mathbb{Z}   | $\mathbb{Z}$   |
| 空集       | \emptyset    | $\emptyset$    |

## 3.5 三角运算

| 描述   | 代码   | 显示     |
| ------ | ------ | -------- |
| 垂直   | \bot   | $\bot$   |
| 角度   | \angle | $\angle$ |
| 正弦   | \sin   | $\sin$   |
| 余弦   | \cos   | $\cos$   |
| 正切   | \tan   | $\tan$   |
| 反正弦 | \sec   | $\sec$   |
| 反余弦 | \csc   | $\csc$   |
| 反正切 | \cot   | $\cot$   |

# 4 数学符号、希腊字母

## 4.1 数学符号

| 描述                             | 代码          | 显示            |
| -------------------------------- | ------------- | --------------- |
| 无穷                             | \infty        | $\infty$        |
| 虚数                             | \imath        | $\imath$        |
| 虚数                             | \jmath        | $\jmath$        |
| 数学符号                         | \hat{a}       | $\hat{a}$       |
| 数学符号                         | \check{a}     | $\check{a}$     |
| 数学符号                         | \breve{a}     | $\breve{a}$     |
| 数学符号                         | \tilde{a}     | $\tilde{a}$     |
| 数学符号                         | \widetilde{a} | $\widetilde{a}$ |
| 数学符号                         | \overline{a}  | $\overline{a}$  |
| 数学符号                         | \bar{a}       | $\bar a$        |
| 矢量符号                         | \vec{a}       | $\vec{a}$       |
| 数学符号                         | \grave{a}     | $\grave{a}$     |
| 数学符号                         | \mathring{a}  | $\mathring{a}$  |
| 一阶导数                         | \dot{a}       | $\dot{a}$       |
| 二阶导数                         | \ddot{a}      | $\ddot{a}$      |
| 上箭头                           | \uparrow      | $\uparrow$      |
| 上箭头（以下箭头均具有相同形式） | \Uparrow      | $\Uparrow$      |
| 下箭头                           | \downarrow    | $\downarrow$    |
| 左箭头                           | \leftarrow    | $\leftarrow$    |
| 右箭头                           | \rightarrow   | $\rightarrow$   |
| 波浪线                           | \sim          | $\sim$          |
| 底端对齐的省略号                 | \ldots        | $\dots$         |
| 中线对齐的省略号                 | \cdots        | $\cdots$        |
| 竖直对齐的省略号                 | \vdots        | $\vdots$        |
| 斜对齐的省略号                   | \ddots        | $\ddots$        |

## 4.2 希腊字母

| 字母       | 代码     | 字母       | 代码     |
| ---------- | -------- | ---------- | -------- |
| $\Alpha$   | \Alpha   | $\alpha$   | \alpha   |
| $\Beta$    | \Beta    | $\beta$    | \beta    |
| $\Gamma$   | \Gamma   | $\gamma$   | \gamma   |
| $\Delta$   | \Delta   | $\delta$   | \delta   |
| $\Epsilon$ | \Epsilon | $\epsilon$ | \epsilon |
| $\Zeta$    | \Zeta    | $\zeta$    | \zeta    |
| $\Eta$     | \Eta     | $\eta$     | \eta     |
| $\Theta$   | \Theta   | $\theta$   | \theta   |
| $\Iota$    | \Iota    | $\iota$    | \iota    |
| $\Kappa$   | \Kappa   | $\kappa$   | \kappa   |
| $\Lambda$  | \Lambda  | $\lambda$  | \lambda  |
| $\Mu$      | \Mu      | $\mu$      | \mu      |
| $\Nu$      | \Nu      | $\nu$      | \nu      |
| $\Xi$      | \Xi      | $\xi$      | \xi      |
| $\Omicron$ | \Omicron | $\omicron$ | \omicron |
| $\Pi$      | \Pi      | $\pi$      | \pi      |
| $\Rho$     | \Rho     | $\rho$     | \rho     |
| $\Sigma$   | \Sigma   | $\sigma$   | \sigma   |
| $\Tau$     | \Tau     | $\tau$     | \tau     |
| $\Upsilon$ | \Upsilon | $\upsilon$ | \upsilon |
| $\Phi$     | \Phi     | $\Phi$     | \phi     |
| $\Chi$     | \Chi     | $\chi$     | \chi     |
| $\Psi$     | \psi     | $\psi$     | \psi     |
| $\Omega$   | \Omega   | $\omega$   | \omega   |

