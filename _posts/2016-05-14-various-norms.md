---
layout: post
title: Various Vector and Matrix norms
date: 2016-05-14 10:45
categories: Math
comments: true
---

### vector norms ###
-------
Given a vector $x=(x_1,...,x_n)^T $. Then we defined the vector norms as follow.

-  $ \| \| x \| \|_{0} $  = the number of non-zero members of the vector.

-  $ \| \| x \| \|_1 $ = $\| x_1 \| + ... + \| x_n \|$.

-  $ \| \| x \| \|_2 $ = $\sqrt{ \| x_1 \|^2 + ... + \| x_n \|^2 }$
-  $ \| \| x \| \|_{ \infty} $ =$ \max \left[ \|x_1 \|,..., \| x_n \| \right]$
-  $ \| \| x \| \|_p $  = $( \| x_1 \|^p,..., \|x_n \|^p)^{ \frac{1}{p}}$

### matrix norms ###
-------
Given a matrix $ A=(a_{ij}) \in C^{m \times n}$. Then we defined the following matrix norms.

- $  \| \| A \| \|_1  =  \max_{1 \leq j \leq n} \sum_{i=1}^m \| a_{ij} \| $.

- $ \| \| A \| \|_2  =  \sigma_1 (A) $, $\sigma_1(A)$ is the maximum singular value of the matrix $A$.

- $  \| \| A \| \|_{ \infty}  =  \max_{1 \leq i \leq n} \sum_{j=1}^n \| a_{ij} \| $

- $  \| \| A \| \|_*  =  \sum_i \sigma_i (A) $.

- $  \| \| A \| \|_F = ( \sum_{i=1}^m \sum_{j=1}^n \| a_{ij} \|^2)^{1/2} = (Tr(A^HA))^{1/2} $.
