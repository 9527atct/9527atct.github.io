---
layout: postarticle
title: Wishart Distribution
date: 2017-02-12 14:11:05 +1000
categories: MachineLearning
comments: true
---



----------

### Inverse Wishart Distribution ###
-----------------
$S^{-1}$ is said to have an inverse wishart distribution $W\_p^{-1}(\\Sigma,r)$, if its pdf ($M=S^{-1}$)
\\[
p(M)=\\frac{|M|^{-\\frac{r+p+1}{2}} \\cdot ETr(-\\frac{1}{2} \\Sigma^{-1} M^{-1})}{2^{rp/2} \\cdot \\pi^{p(p-1)/4} \\cdot |\\Sigma |^{r/2} \\cdot \\prod\_{i=1}^p \\Gamma (\\frac{r+1-i}{2}) }
\\]





### Reference ###
-----------------
[Variational Bayesian methods](https://en.wikipedia.org/wiki/Variational_Bayesian_methods)

[Variational Inference](https://www.cs.princeton.edu/courses/archive/fall11/cos597C/lectures/variational-inference-i.pdf)
