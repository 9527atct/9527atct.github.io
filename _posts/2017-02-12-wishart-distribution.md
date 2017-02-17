---
layout: postarticle
title: wishart distribution
date: 2017-02-12 14:11:05 +1000
categories: MachineLearning
comments: true
---

### Wishart Distribution ###
+ **Definition**  
If $S=X^TX$, where $X\_{np}\\sim N(0,I\_n \\otimes \\Sigma)$, here, $p$ is the dimensions of the data, and, $n$ is the number of the data. Then $S$ is positive definite, and is said to have the wishart distribution with $n$ degree of  freedom and covariance matrix $\\Sigma$.
\\[
\\begin{split}
X^TX &= S \\sim W\_p(\\Sigma,n) \\\
&\\Updownarrow \\text{equivalence} \\\
X&\\sim N(0,I\_n \\otimes \\Sigma)
\\end{split}
\\]

1.  [**pdf.**]If $S$ is $W\_p(\\Sigma, r)$  , then the density function of $S$ is,
\\[
p(S)=\\frac{ |S|^{\\frac{r-p-1}{2}} \\cdot exp(-\\frac{1}{2} Tr(\\Sigma^{-1}S))  }{ 2^{rp/2} \\cdot \\pi^{\\frac{p(p-1)}{4}} \\cdot |\\Sigma |^{r/2} \\cdot \\prod\_{i=1}^p \\Gamma (\\frac{r-i+1}{2}) }
\\]

2. [**Decompose Properties**] Let $S\\sim W\_p(\\Sigma,r)$,$S\_{11.2}=S\_{11}-S\_{12}S\_{22}^{-1}S\_{21}$ (schur completement of $S\_{22}$),$\\Sigma\_{11.2}=\\Sigma\_{11}-\\Sigma\_{12}\\Sigma\_{22}^{-1}\\Sigma\_{21}$ (schur completement of $\\Sigma\_{22}$), then
  + $S\_{11}\\sim W\_p(\\Sigma\_{11},r)$
  + $S\_{22}\\sim W\_p(\\Sigma\_{22},r)$
  + $S\_{11.2}\\sim W\_p(\\Sigma\_{11.2},r-(p-q))$
  + $S\_{12} \| S\_{22} \\sim N\_{q,p-q}(\\Sigma_{12}\\Sigma\_{22}^{-1}S\_{22}, \\Sigma\_{11.2} \\otimes S\_{22})$




3. [**Sample Wishart Distribution**] Let $S\\sim W\_p(I\_p,r)$ and $S=T^TT$ where $T=(t\_{ij})$ is a upper triangle matrix, $t\_{ii}>0$ then,  
    + $t\_{ij}, 1\\leq j \\leq i \\leq p$ are independently distributed
    + $t\_{ii}^2 \\sim \\chi^2\_{r-i+1}$  
    + $t\_{ij}\\sim N(0,1),  1\\le j \le i \le p$  


  

### Inverse Wishart Distribution ###
+ [**definition**] $S^{-1}$ is said to have an inverse wishart distribution $W\_p^{-1}(\\Sigma,r)$, if its pdf ($M=S^{-1}$)
\\[
p(M)=\\frac{|M|^{-\\frac{r+p+1}{2}} \\cdot eTr(-\\frac{1}{2} \\Sigma^{-1} M^{-1})}{2^{rp/2} \\cdot \\pi^{p(p-1)/4} \\cdot |\\Sigma |^{r/2} \\cdot \\prod\_{i=1}^p \\Gamma (\\frac{r+1-i}{2}) }
\\]

+ [**transformation**]The inverse wishart distribution can be treated as the results after performing  transformation $(M\\rightarrow S^{-1})$.  
And the jacobin of the transformation $(M\\rightarrow S^{-1})$ is (using outer product, or, wedge product),  
\\[
(dM)=det(S)^{-2m} (dS)
\\]
if the $S$ is symmetric, then,
\\[
(dM)=det(S)^{-(m+1)}(dS)
\\]





