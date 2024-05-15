---
title: 数模算法之线性规划
date: 2024-05-16
categories:
- 数学建模
tag: 
- 算法
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=436346833&auto=0&height=66"></iframe>

> OIer入门数模竞赛代码手之路

在生产实践中，经常会遇到如何利用现有资源安排生成，以取得最大效益的问题。运筹学的一个重要分支——数学规划应运而生，它是一种通过数学方法来解决实际问题的方法。线性规划是数学规划的一个重要分支，它是一种在给定约束条件下，求解线性目标函数最优值的方法。

> 本系列偏代码向，入门之前需要了解一些基本的数学知识，如线代、微积分等。本系列（由于一些懂得都懂的原因）以`Python`为主，也会涉及`Matlab`。

<!-- more -->

# 线性规划问题

## 举个例子

某厂家生产甲乙两种产品，每件利润分别为$4000,3000$元。生产甲产品需用$A,B$两种机器加工，每件分别需要$2h,1h$；生成乙产品需用$A,B,C$三种机器加工，每件每种机器$1h$。机器每天可运行时长为$10h,8h,7h$。问如何安排生产计划，使得利润最大？

对上述问题建立数学模型：设甲乙产品的生产量分别为$x_1,x_2$时，总利润$z=4000x_1+3000x_2$最大，则：

$$
\max z=4000x_1+3000x_2\\
s.t. \begin{cases}
2x_1 + x_2 \leq 10\\
x_1 + x_2 \leq 8\\
x_2 \leq 7\\
x_1 , x_2 \geq 0
\end{cases}
$$

其中，$x_1,x_2$称为决策变量，函数$z=4000x_1+3000x_2$称为目标函数，`s.t.`标记的不等式组称为约束条件（即`subject to`）。由于上述目标函数与约束条件均为线性，故称线性规划。

## 线性规划问题的解

一般线性规划问题的（`Matlab/Python`）标准形式为：

$$
\min z = f^T x\\
s.t.\begin{cases}
A\times x \leq b\\
Aeq \times x = Beq\\
lb \leq x \leq ub
\end{cases}
$$

式中`f,x,b,Beq,lb,ub`为列向量，`A,Aeq`为矩阵，其中称`f`为价值向量，`A`为不等式约束矩阵，`b`为不等式约束向量（价值向量），`Aeq`为等式约束矩阵，`Beq`为等式约束向量，`lb`为下界向量，`ub`为上界向量。

满足约束条件的`x`即称为线性规划的**可行解**。所有可行解构成的集合称为**可行域**，记作$R$。其中，目标函数`z`最小的可行解称为**最优解**。

## 代码实现

利用`Python`求解线性规划问题需要导入`numpy,scipy`库。以上述问题为例，其数学模型转化为标准形式为：

$$
\min z = -\begin{pmatrix}
-4000 \\ -3000
\end{pmatrix}^T \times \begin{pmatrix}
x_1 \\ x_2
\end{pmatrix}\\
s.t.\begin{cases}
\begin{pmatrix}
2 & 1\\
1 & 1\\
0 & 1
\end{pmatrix}
\begin{pmatrix}
x_1 \\ x_2
\end{pmatrix}
\leq \begin{pmatrix}
10 \\ 8 \\ 7
\end{pmatrix}\\
\begin{pmatrix}
x_1 \\ x_2
\end{pmatrix}
\geq\begin{pmatrix}
0 \\ 0
\end{pmatrix}
\end{cases}
$$

将参数定义为`numpy`矩阵后调用函数求解：

```python
from scipy import optimize
import numpy as np

f = np.array([-4000,-3000]).transpose()
A = np.array([[2,1],[1,1],[0,1]])
b = np.array([10,8,7])

#求解
res = optimize.linprog(c=f,A_ub=A,b_ub=b,bounds=np.array([[0,None],[0,None]]))
print(res)

'''
result:
message: Optimization terminated successfully. (HiGHS Status 7: Optimal)
success: True
status: 0
fun: -26000.0
x: [ 2.000e+00  6.000e+00]
nit: 2
lower: residual: [ 2.000e+00  6.000e+00]
       marginals: [ 0.000e+00  0.000e+00]
upper: residual: [ inf inf]
       marginals: [ 0.000e+00  0.000e+00]
eqlin: residual: []
       marginals: []
ineqlin: residual: [ 0.000e+00  0.000e+00  1.000e+00]
         marginals: [-1.000e+03 -2.000e+03 -0.000e+00]
mip_node_count: 0
mip_dual_bound: 0.0
mip_gap: 0.0
'''
```

其中`linprog`的完整参数：

```python
def linprog(c, A_ub=None, b_ub=None, A_eq=None, b_eq=None,
            bounds=None, method='interior-point', callback=None,
            options=None, x0=None)
```

其中：

|参数|意义|
|---|---|
|c|目标函数的决策变量对应的系数向量(行列向量都可以，下同)|
|A_ub|不等式约束组成的决策变量系数矩阵|
|b_ub|由A_ub对应不等式顺序的阈值向量|
|A_eq|等式约束组成的决策变量系数矩阵|
|b_eq|由A_ub对应等式顺序的阈值向量|
|bounds|表示决策变量x连续的定义域的n×2维矩阵，None表示无穷|
|method|调用的求解方法，2.2节给出详细解释|
|callback|选择的回调函数|
|options|求解器选择的字典|
|x0|初始假设的决策变量向量，若可行linprog会对方法优化|

求解线性规划问题的`Matlab`函数为：

```
[x,val] = linprog(f,A,b);
[x,val] = linprog(f,A,b,Aeq,Beq);
[x,val] = linprog(f,A,b,Aeq,Beq,lb,ub);
```

其中`x`为决策向量，`val`为此时目标函数值。

> 未完待续