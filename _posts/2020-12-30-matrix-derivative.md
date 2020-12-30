---
layout: postarticle
title: matrix derivatives
date: 2020-12-30 10:50
categories: math
comments: true
---

------------------------
### 矩阵变元的标题函数求导法 ###

标量函数$f(\mathbf{X})$对矩阵变元$\mathbf{X}$的导数为，
\\[
\frac{\partial f}{\partial \mathbf{X}}=\left[ \frac{\partial f}{\partial X_{ij}} \right]
\\]
即函数$f$对矩阵$\mathbf{X}$逐元素求导，并排列成与$\mathbf{X}$同尺度的矩阵。然而，这个定义在计算中并不友好，主要原因是对于较为复杂的函数难以逐元素求导，逐元素求导破坏了整体性。

我们知道，在一元微积分中，梯度与微分的关系为：
\\[
df=f'(x)dx
\\]
而在多元微积分中，梯度与微分也有着如下的联系：
\\[
df=\sum_i \frac{\partial f}{\partial x_i}dx_i = \left[ \frac{\partial f}{\partial \mathbf{x}} \right]^T d\mathbf{x}
\\]
因此，矩阵层数与微分之间的关系为
\\[
df=\sum_{i,j}\frac{\partial f}{\partial X_{ij}}dX_{ij}=tr\left( \left[\frac{\partial f}{\partial \mathbf{X}}\right]^T d\mathbf{X} \right)
\\]
