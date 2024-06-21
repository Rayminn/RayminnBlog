---
title: 中科大2024强基数学压轴题的算法解析
date: 2024-06-20
categories:
- 数学
tag: 
- 算法
---

最近，中科大2024年强基数学考试的压轴题引起了广泛关注。题目如下：

$$
\text{有数列}F_n = F_{n-1}+F_{n-2}, F_1 = 1, F_2 = 1, \text{求}F_{1958}\text{的个位数}
$$

这个数列是著名的斐波那契数列，对此类多项递推问题，我们可以采用改写矩阵形式的方法解决。

<!-- more -->

# 斐波那契数列的矩阵递推形式

我们可以将斐波那契数列的递推式写成**矩阵形式**：

$$
\begin{pmatrix} F_{n+1} \\ F_n \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} F_n \\ F_{n-1} \end{pmatrix}
$$

这就是一个典型的乘积递推问题，显然我们可以找到其通项公式：

$$
\begin{pmatrix} F_{n} \\ F_{n-1} \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}^{n-2} \begin{pmatrix} F_2 \\ F_1 \end{pmatrix}
$$

变换可知：

$$
F_{n} = | \begin{pmatrix} 1 & 0 \end{pmatrix} \begin{pmatrix} F_{n} \\ F_{n-1} \end{pmatrix} | = |\begin{pmatrix} 1 & 0 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}^{n-2} \begin{pmatrix} 1 \\ 1 \end{pmatrix} |
$$

至此我们可以用**矩阵快速幂**求解。

# 对模10意义下的性质解析

由于此题为笔试题，直接手算矩阵快速幂显然是不优雅的，在进行矩阵快速幂的同时，我们可以对模10意义下的性质进行分析。

不难发现，矩阵$\begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}$的$2^2$次方等于其$2^6$次方。

那么该矩阵模$10$意义下的$n$次幂存在周期$T$，且$T\leq 60$。

此时我们就可以对$n-2$取模以简化运算。

# 方阵幂算法

对于此类多项递推问题，我们还可以通过**方阵幂**算法求解其通项公式。

方阵幂算法的核心是对矩阵通过**矩阵的特征值**进行**对角化**，然后通过**对角化矩阵**的幂求解原矩阵的幂。

该数列的递推矩阵即可对角化过程如下：

求解其特征值：

$$

\begin{vmatrix} 1-\lambda & 1 \\ 1 & -\lambda \end{vmatrix} = 0

$$

解得$\lambda = \frac{1\pm\sqrt{5}}{2}$，对应特征向量为$\begin{pmatrix} \frac{1+\sqrt{5}}{2} \\ 1 \end{pmatrix}$和$\begin{pmatrix} \frac{1-\sqrt{5}}{2} \\ 1 \end{pmatrix}$。

那么我们可以得到：

$$
\begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} \frac{1+\sqrt{5}}{2} & \frac{1-\sqrt{5}}{2} \\ 1 & 1 \end{pmatrix} \begin{pmatrix} \left(\frac{1+\sqrt{5}}{2}\right) & 0 \\ 0 & \left(\frac{1-\sqrt{5}}{2}\right) \end{pmatrix} \begin{pmatrix} \frac{1+\sqrt{5}}{2} & \frac{1-\sqrt{5}}{2} \\ 1 & 1 \end{pmatrix}^{-1}
$$

此时利用矩阵对角化的特性：

$$
\begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}^{n-1} = \begin{pmatrix} \frac{1+\sqrt{5}}{2} & \frac{1-\sqrt{5}}{2} \\ 1 & 1 \end{pmatrix} \begin{pmatrix} \left(\frac{1+\sqrt{5}}{2}\right)^{n-1} & 0 \\ 0 & \left(\frac{1-\sqrt{5}}{2}\right)^{n-1} \end{pmatrix} \begin{pmatrix} \frac{1+\sqrt{5}}{2} & \frac{1-\sqrt{5}}{2} \\ 1 & 1 \end{pmatrix}^{-1}
$$

至此我们可以将以上结果代入矩阵形式通项公式得到结果。