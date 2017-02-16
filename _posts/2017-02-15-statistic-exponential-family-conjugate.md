---
layout: post
title: sufficient statistic and conjugate
date: 2017-02-15 21:45
categories: MachineLearning
comments: true
---

### Statistic ###
- [**definition**]  
    Given random variables (vectors) $X\_1,...,X\_n$ w.r.t. sets of possible values $\\mathcal{X}\_1,...,\\mathcal{X}\_n$, respectively. A random vector $t\_n:\\mathcal{X}\_1 \\times \\mathcal{X}\_2 \\times ... \\times \\mathcal{X}\_n \\rightarrow R^{k(n)}$ is called a $k(n)$ dimensional statistic.

- [**example**]  
    + $t_n = \\frac{1}{n}(X\_1+X\_2+...+X\_n)$, $k(n)=1$
    + $t_n = [n,(X\_1+...+X\_n),(X\_1^2+...+X\_n^2)]$, $k(n)=3$.
    
- [**sufficient statistic**]  
    A statistic $t=T(x)$ is sufficient for underlying parameter $\\theta$ prcisely, if the conditional probability distribution of data $X$, given $t=T(x)$, does not depend on the parameter $\\theta$, i.e.,
    \\[
        p(x|\\theta,t)=p(x|t)
    \\]