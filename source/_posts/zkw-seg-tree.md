---
title: zkw线段树
date: 2024-04-25
categories:
- ICPC/OI
tag: 
- 数据结构
---

建站时本人正于高三，也就是OI和ICPC的空档期，不知道该写什么，最后选择写本人最擅长的数据结构：非递归线段树。

<!--more-->

# 前言

非递归线段树，是通过建树时将树建为满二叉树，从而利用满二叉树特性，实现$O(1)$查询叶节点，自下而上通过循环完成操作。虽然看起来建满二叉树会导致占用空间变大，但实际上经典线段树也要为了避免`MLE`开四倍空间，所以二者空间复杂度区别并不大。并且循环时间复杂度明显小于递归，所以非递归线段树平均时间复杂度远小于经典线段树。

# 满二叉树

需要求得一个常数`p`，作为树叶子节点的第一个，即可快速定位到所有叶子节点。

`p`的求法：

```cpp
for(p=1;p<n+2;p++);
```

烂尾待补。。。