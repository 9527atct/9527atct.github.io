---
layout: post
title: Matrix Elementary
date: 2017-02-13 20:45
categories: Math
comments: true
---

### Trace ###
- [**basic properties**]
\\[
\\begin{split}
tr(A+B) &= tr(A) + tr(B)\\\
tr(kA) &= ktr(A) \\\
tr(A^T) &= tr(A)
\\end{split}
\\]

- [**trace of a product**]
\\[
tr(X^TY)=tr(XY^T)=tr(Y^TX)=tr(YX^T)=\\sum_{ij}X\_{ij}Y\_{ij}
\\]
for **Hadamard product**,
\\[
tr(X^TY)=\\sum_{ij}(X \\circ Y)\_{ij}
\\]
for **vectorization**,
\\[
tr(X^TY)=vec(Y)^T vec(X)=vec(X)^Tvec(Y)
\\]
**invariant under cyclic permutation**,
\\[
tr(ABCD)=tr(BCDA)=tr(CDAB)=tr(DABC)
\\]
for **Kronecker product**,
\\[
tr(X \\otimes Y) = tr(X)tr(Y)
\\]

- [**spectrum of matrix**]
If $f(x)=(x-\\lambda\_1)^{d\_1}...(x-\\lambda\_k)^{d\_k} $ is the *characteristic polynomial* of a matrix A, then,
\\[
tr(A)=d\_1 \\lambda\_1 +...+d\_k\\lambda\_k
\\]


### Kronecker Product###
+ [**brief introduce**] In mathematics, the Kronecker Product, denoted by $\\otimes$, is an operation on two matrices of arbitrary size resulting in a block matrix. It is a generation of outer product from vectors to matrices, and gives the matrix of tensor product w.r.t. a standard choices of basis. The Kronecker Product is named after Leopold Kronecker, even though there is little evidence that he was the first to define and use it.

+ [**definition**] If $A$ is an $m\\times n$ matrix and $B$ is a $p\\times q$ matrix, then the Kronecker Product $A\\otimes B$ is the $mp\\times nq$ block matrix.
\\[
A \\otimes B = \\begin{pmatrix}
a\_{11}B & ... & a\_{1n}B \\\
\\vdots & \\ddots & \\vdots \\\
a\_{m1}B & ... & a\_{mn}B \\\
\\end{pmatrix}
\\]
more compactly, we have $(A\\otimes B)\_{p(r-1)+v,q(s-1)+w}=a\_{rs}b\_{vw}$.

+ [**bi-linearity and  associativity**] The Kronecker Product is a special case of tensor product.
\\[
\\begin{split}
A \\otimes (B+C) &= A \\otimes B + A\\otimes C \\\
(A+B) \\otimes C &= A \\otimes C + B\\otimes C \\\
(kA)\\otimes B &= k(A\\otimes B) = A \\otimes (kB)\\\
A\\otimes B \\otimes C &= (A\\otimes B) \\otimes C = A \\otimes (B \\otimes C)
\\end{split}
\\]

+ [**non-commutative**] $A\\otimes B$ and $B\\otimes A$ are different matrices. However, $A\\otimes B$ and $B\\otimes A$ are permutation equivalent, meaning that there exists permutation matrices $P,Q$ such that,
\\[
P(B\\otimes A)Q = A\\otimes B
\\]
If $A,B$ are square matrices, $P=Q^T$.

+ [**property 3**]
\\[
\\begin{split}
(A\\otimes C)(B\\otimes D) &=(AB)\\otimes (CD)\\\
(A\\otimes B)^{-1} &= A^{-1}\\otimes B^{-1}\\\
(A\\otimes B)^T &= A^T \\otimes B^T \\\
(A\\otimes B)^+ &= A^+ \\otimes B^+ \\\
\\end{split}
\\]

+ [**determinant**] Let $A$ be an $n\\times n$ matrix, $B$ be an $m\\times m$ matrix, then
\\[
|A\\otimes B|=|A|^{m=dim(B)} |B|^n
\\]

+ [**vectorization**] Consider for instance the equation $AXB=C$, $A,B,C$ are given matrices and the matrix $X$ is unknown, then
\\[
vec(C)=(B^T \\otimes A) \\times vec(X)
\\]
For an example, this formula comes into handy in showing that matrix normal distribution is a special case of the multivariate normal distribution.

### Bilinear Map###
+ [**brief introduce**] In mathematics, a bilinear map is a function combining elements of two vector space to yield an element of a third vector space, and is linear in each of its arguments. **matrix multiplication is an example**.

+ [**definition**] Let $V,W$ and $X$ be three vector space over the same base field $\\mathcal{F}$. A bilinear map is a function:
\\[
f: V\\times W \\rightarrow X
\\]
such that for any $w$ in $W$ the map,
\\[
v \\rightarrow f(v,w)
\\]
is a linear map from $V$ to $X$, and for any $v$ in $V$ the map,
\\[
w \\rightarrow f(v,w)
\\]
is a linear map from $W$ to $X$. In another words, when we hold the first entry of the bilinear map fixed while letting the second entry vary, the results is a linear operator, and similarly when we hold the second entry fixed.

### Block Matrix ###
- [**block matrix multiplication**] Given two matrix $A\_{m\\times p}, B\_{p\\times n}$, then turn it to a block partitioned matrix, using "conformable partition" Strategies, such as given A an arbitary column partition, the the matrix B using the same style to divide the rowes. Then,
\\[
C=A^TB
\\]

- [**schur complement**]
If $A$ is inversable, then for block matrix 
\\[
M=\\begin{pmatrix}
A & B \\\
C & D \\\
\\end{pmatrix}
\\]
we have the schur complement of block $A$ is,
\\[
M/A = D-CA^{-1}B
\\]
and, the schur complement of block $D$ is,
\\[
M/D = A-BD^{-1}C
\\]

- [**LDU decompose**]
\\[
\\begin{pmatrix}
A & B \\\
C & D \\\
\\end{pmatrix}=\\begin{pmatrix} I & 0 \\\ CA^{-1} & I \\end{pmatrix} \\begin{pmatrix} A & 0 \\\ 0 & D-CA^{-1}B \\end{pmatrix} \\begin{pmatrix} I & A^{-1}B \\\ 0 & I \\end{pmatrix}
\\]

- [**inverse of the block matrix**]
\\[
\\begin{pmatrix}
A & B \\\
C & D \\\
\\end{pmatrix}^{-1} = \\begin{pmatrix} 
A^{-1}+A^{-1}B(D-CA^{-1}B)^{-1}CA^{-1} & -A^{-1}B(D-CA^{-1}B)^{-1} \\\
-(D-CA^{-1}B)^{-1}CA^{-1} & (D-CA^{-1}B)^{-1} \\\
\\end{pmatrix}
\\]

    special case, for diagonal block matrix, we have,
\\[
\\begin{pmatrix}
A & 0 \\\
0 & B
\\end{pmatrix}^{-1} = \\begin{pmatrix} A^{-1} & 0  \\\
0 & B^{-1} \\\ \\end{pmatrix}
\\]

    for upper triangle block matrix,
\\[
\\begin{pmatrix}
A & C \\\
0 & B
\\end{pmatrix}^{-1} = \\begin{pmatrix} A^{-1} & -A^{-1}CB^{-1} \\\
0 & B^{-1} \\\ \\end{pmatrix}
\\]

    for lower triangle block matrix,
\\[
\\begin{pmatrix}
A & 0 \\\
C & B
\\end{pmatrix}^{-1} = \\begin{pmatrix} A^{-1} & 0  \\\
-B^{-1}CA^{-1} & B^{-1} \\\ \\end{pmatrix}
\\]

    for subordinary diagonal block matrix,
\\[
\\begin{pmatrix}
0 & A \\\
B & 0
\\end{pmatrix}^{-1} = \\begin{pmatrix} 0 & B^{-1} \\\
A^{-1} & 0 \\\ \\end{pmatrix}
\\]   



### Block Diagonal Matrices ###
- [**definition**] block diagonal matrix is a block matrix that is a square matrix, and having main diagonal block matrices.
\\[
A=\\begin{pmatrix}
A\_1 & 0 & ... & 0 \\\
0 & A\_2 & ... & 0 \\\
\\vdots & \\vdots & \\ddots & \\vdots \\\
0 & 0 & ... & A\_n \\\
\\end{pmatrix}
\\]
- [**determinat**] 
\\[
det(A)=det(A\_1)\\times ... \\times det(A\_n)
\\]
- [**trace**]
\\[
tr(A)= tr(A\_1)+...+tr(A\_n)
\\]







### Vector Norms ###
Given a vector $x=(x_1,...,x_n)^T $. Then we defined the vector norms as follow.

-  $ \| \| x \| \|_{0} $  = the number of non-zero members of the vector.

-  $ \| \| x \| \|_1 $ = $\| x_1 \| + ... + \| x_n \|$.

-  $ \| \| x \| \|_2 $ = $\sqrt{ \| x_1 \|^2 + ... + \| x_n \|^2 }$
-  $ \| \| x \| \|_{ \infty} $ =$ \max \left[ \|x_1 \|,..., \| x_n \| \right]$
-  $ \| \| x \| \|_p $  = $( \| x_1 \|^p,..., \|x_n \|^p)^{ \frac{1}{p}}$


### Matrix Norms ###
Given a matrix $ A=(a_{ij}) \in C^{m \times n}$. Then we defined the following matrix norms. Due to the sementic conflic with mathjax and markdown, so, all of the norms ignore the symbol with which to identify themselves are not in the normal format.

- $  \| \| A \| \|\_1  =  \\max_{1 \leq j \leq n} \\sum\_{i=1}^m \| a\_{ij} \| $.

- $ \| \| A \| \|\_2   =  \\sigma\_1 (A) $, $\\sigma\_1(A)$ is the maximum singular value of the matrix $A$.

- $  \| \| A \| \|\_{ \\infty}  =  \\max_{1 \leq i \leq n} \\sum\_{j=1}^n \| a\_{ij} \| $

- $  \| \| A \| \|\_*  =  \\sum_i \\sigma\_i (A) $.

- $  \| \| A \| \|\_F = ( \\sum\_{i=1}^m \\sum\_{j=1}^n \| a\_{ij} \|^2)^{1/2} = (Tr(A^HA))^{1/2} $.
