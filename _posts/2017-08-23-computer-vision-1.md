---
layout: postarticle
title: computer vision 1
date: 2017-08-23 21:25:05 +1000
categories: ComputerVision
comments: true
---   

### 矩阵与图像      
---  
 **图像在Matlab中的存储形式为一个维度为3的矩阵**($m\times n\times 3$)。  以下图像操作都是基齐次坐标(Homogeneous	Coordinates)。 In homogeneous coordinates, the multiplication works out so the rightmost column of the matrix is a vector that gets added.  
--- 

**图像位移(Translation)**  
原位置：$P=(x,y)$, 新位置：$P'=(x+t\_x,y+t\_y)$,位移量：$t=(t\_x,t\_y)$,那么位移矩阵为：$T$,即，
\\[
\begin{bmatrix}
x+t\_x\\\y+t\_y\\\1
\end{bmatrix}=P'==TP=\begin{bmatrix}
1&0&t\_x\\\
0&1&t\_y\\\
0&0&1
\end{bmatrix}\cdot \begin{bmatrix}
x\\\y\\\1
\end{bmatrix}
\\]

---  

**图像缩放(Scaling)**  
原位置：$P=(x,y)$, 新位置：$P'=(s\_x x,s\_y y)$,缩放量：$s=(s\_x,s\_y)$,那么缩放矩阵为：$S$,即，
\\[
\begin{bmatrix}
s\_xx\\\s\_yy\\\1
\end{bmatrix}=P'==SP=\begin{bmatrix}
s\_x&0&0\\\
0&s\_y&0\\\
0&0&1
\end{bmatrix}\cdot \begin{bmatrix}
x\\\y\\\1
\end{bmatrix}
\\]

---  
**由于矩阵乘法的不可交换性，导致 Translation \& Scaling != Scaling \& Translation**  
---  

**图像旋转(Rotation)**  
原位置：$P=(x,y)$, 新位置：$P'=(x',y')$,旋转角度：$\theta=(\theta)$,那么旋转矩阵为：$R$,即
\\[
\begin{bmatrix}
r\_x\\\r\_y\\\1
\end{bmatrix}=P'==RP=\begin{bmatrix}
\text{cos}(\theta)&-\text{sin}(\theta)&0\\\
\text{sin}(\theta)&\text{cos}(\theta)&0\\\
0&0&1
\end{bmatrix}\cdot \begin{bmatrix}
x\\\y\\\1
\end{bmatrix}
\\]
旋转公式：
\\[
\begin{split}
r\_x &= \text{cos}(\theta)x-\text{sin}(\theta)y\\\
r\_y &= \text{sin}(\theta)x+\text{cos}(\theta)y
\end{split}
\\]
旋转矩阵性质：旋转矩阵的转置产生一个相反方向的旋转  
\\[
\begin{split}
RR^T &=R^TR=I \\\
det(R)&=1
\end{split}
\\]
旋转矩阵的行都是相互垂直的(正交)

---

**奇异值分解**Singular Value Decomposition (SVD)  
SVD represents any matrix $A$ as a product of three matrices: $U\Sigma V^T$. In MATLAB, the function is $[U,S,V]=svd(A)$.
\\[
\begin{bmatrix}
-0.39&-0.92\\\
-0.92&0.39
\end{bmatrix}\_{m\times m}\times\begin{bmatrix}
9.51&0&0\\\0&0.77&0
\end{bmatrix}\_{m\times n}\times\begin{bmatrix}
-0.42&-0.57&-0.70\\\0.81&0.11&-0.58\\\0.41&-0.82&0.41
\end{bmatrix}\_{n\times n}=\begin{bmatrix}
1&2&3\\\4&5&6
\end{bmatrix}\_{n\times n}
\\]

SVD的意义。先将缩放因子吸收进$U$,得到$[U\Sigma]\_{m\times n}$,
\\[
\begin{bmatrix}
-3.67&-0.71&0\\\-8.8&0.30&0
\end{bmatrix}\times \begin{bmatrix}
-0.42&-0.57&-0.70\\\0.81&0.11&-0.58\\\0.41&-0.82&0.41
\end{bmatrix}
\\]

矩阵$U\Sigma$第一列影响的部分为$V^T$的第一行,即，$V^T$的第一行$(V\_1)^T=\begin{bmatrix}
	-3.67\\\-8.8	\end{bmatrix}$只缩放了$U\Sigma$的第一列$[U\Sigma]\_1=\begin{bmatrix}
	-0.42&-0.57&-0.70
	\end{bmatrix}$，同理，第二列影响第二行，影响的结果分别为，
\\[
\begin{split}
A\_1&=\begin{bmatrix}
1.6&2.1&2.6\\\
3.8&5.0&6.2
\end{bmatrix}=[U\Sigma]\_1 \otimes (V\_1)^T\\\	
A_2&=\begin{bmatrix}
-0.6&-0.1&0.4 \\\
0.2&0&-0.2
\end{bmatrix}=[U\Sigma]\_2 \otimes (V\_2)^T
\end{split}
\\]
其中，"$\otimes$"为Kronecker Product，显然，$A=A\_1+A\_2$. 更具意义的是这个由$U,V$的第一列和$\Sigma\_1$张成的矩阵$A\_1$与$A$已经相差不是太大了。一般，我们称$U$中的这些少量的列向量为**主成分**。





