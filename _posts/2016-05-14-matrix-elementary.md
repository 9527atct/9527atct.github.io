---
layout: post
title: Matrix 
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
Given a matrix $ A=(a_{ij}) \in C^{m \times n}$. Then we defined the following matrix norms. Due to the sementic conflic with mathjax and markdown, so, all of the norms ignore the symbol with which to identify themselves are not in the normal format.

- $  \| \| A \| \|\_1  =  \\max_{1 \leq j \leq n} \\sum\_{i=1}^m \| a\_{ij} \| $.

- $ \| \| A \| \|\_2   =  \\sigma\_1 (A) $, $\\sigma\_1(A)$ is the maximum singular value of the matrix $A$.

- $  \| \| A \| \|\_{ \\infty}  =  \\max_{1 \leq i \leq n} \\sum\_{j=1}^n \| a\_{ij} \| $

- $  \| \| A \| \|\_*  =  \\sum_i \\sigma\_i (A) $.

- $  \| \| A \| \|\_F = ( \\sum\_{i=1}^m \\sum\_{j=1}^n \| a\_{ij} \|^2)^{1/2} = (Tr(A^HA))^{1/2} $.
