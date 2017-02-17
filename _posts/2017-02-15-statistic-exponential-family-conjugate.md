---
layout: postarticle
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
    - [**from wiki**]  
    A statistic $t=T(x)$ is sufficient for underlying parameter $\\theta$ prcisely, if the conditional probability distribution of data $X$, given $t=T(x)$, does not depend on the parameter $\\theta$, i.e.,
    \\[
        p(x|\\theta,t)=p(x|t)
    \\]
    - [**from prof. zhang manuscript**]  
    The sequence $t\_1,...,t\_n$ is a sufficient statistic for $X\_1,...,X\_n$, if for $n\\geq 1$, the joint density for $X\_1,...,X\_n$ given $\\theta$ has the form,
    \\[
        p(x\_1,...,x\_n\|\\theta)=h\_n(t\_n,\\theta)g(x\_1,...,x\_n)=h\_{\\theta}(t\_n)g(x\_1,...,x\_n)
    \\]
    for some function $h\_n\\geq 0, g\\ge 0$.  
    - [**theorem**]  
    The sequence $t\_1,...,t\_n$ is sufficient for infinitely exchangable $X\_1,...,X\_n,...$ if and only if for any $n\\geq 1$, the density $p(x\_1,...,x\_n\|\\theta,t\_n)$ is independent of $\\theta$.  
    **proof.** For any $t\_n=t\_n(X\_1,...,X\_n)$,
    \\[
    \\begin{split}
        p(x\_1,...,x\_n\|\\theta)&=p(x\_1,...,x\_n,t\_n\|\\theta)\\\
        &=p(x\_1,...,x\_n\|t\_n,\\theta)\\cdot p(t\_n\|\\theta)\\\
    \\end{split}
    \\]
    If $p(x\_1,...,x_n\|\\theta,t\_n)$ is independent of $\\theta$, then $p(x\_1,...,x_n\|\\theta,t\_n)$ is $g$, $p(t\_n,\\theta)$ is $h\_n$. So $t\_n$ is a sufficient statistic.  
    If $t\_n$ is sufficient, then $p(x\_1,...,x\_n\|\\theta)=h\_n(t\_n,\\theta)g(x\_1,...,x\_n), h\_n\\geq 0,g\\ge 0$. Taking integral on both sides, we have,
    \\[
    \\int\_{t\_n(x\_1,...,x\_n)=t\_n} p(x\_1,...,x\_n\|\\theta)dx\_1,...,x\_n = \\int\_{t\_n(x\_1,...,x\_n)=t\_n} h\_n(t\_n,\\theta)g(x\_1,...,x\_n)dx\_1,...,x\_n
    \\]
    Note that $h\_n(t\_n,\\theta)$ in the right side is unrelated to the integral, $\\int g(x)dx$ can be seemed as a function of $t\_n$, denoted by $G(t\_n)$ and $\\int p(x\|\\theta)dx$ can be seemed as $p(t\_n\|\\theta)$. hence, we have,
    \\[
        p(t\_n\|\\theta)=h\_n(t\_n,\\theta)G(t\_n)
    \\]
    and,
    \\[
        h\_n(t\_n,\\theta)=\\frac{ p(t\_n\|\\theta)}{G(t\_n)}
    \\]
    So,
    \\[
        p(x\_1,...,x\_n\|\\theta)=\\frac{ p(t\_n\|\\theta)}{G(t\_n)} g(x\_1,...,x\_n)
    \\]
    and,
    \\[
        p(x\_1,...,x\_n\|t\_n,\\theta)=\\frac{p(x\_1,...,x\_n\|\\theta)}{p(t\_n\|\\theta)}=\\frac{g(x\_1,...,x\_n)}{G(t\_n)}
    \\]
    Thus we can see $p(x\_1,...,x\_n\|\\theta,t\_n)$ is independent with $\\theta$.


###Exponential Family###
- [**one-parameter**]  
    A pdf is said to belong to one-parameter exponential family if it is of the form 
    \\[
        p(x\|\\theta)=f(x)g(\\theta)\\exp(c\\cdot \\phi(\\theta)h(x))
    \\]
    where $g^{-1}(\\theta)=\\int f(x)\\exp(c\\cdot \\phi(\\theta)h(x))dx < \\infty$ is a regularization factor, denoted by $E\_f(f,g,h,\\phi,c,\\theta)$.

- [**sufficient statistic for $E\_f$**]  
    If $X\_1,...,X\_n\\in \\mathcal{X}$ is an exchangeable sequence such that given regular $E\_f$,
    \\[
        p(x\_1,...,x_n)=\\int\_{\\theta}\\prod\_{i=1}^n E\_f(x\_i\|f,g,h,\\phi,c)dF(\\theta)
    \\]
    for some $dF(\\theta)$. Then $t\_n=t\_n(x\_1,...,x\_n)=[n,h(x\_1)+...+h(x\_n)]$ is sufficient statistic.
    - [**example: bernoulli**]  
    \\[
    \\begin{split}
    p(x\|\\theta)&=\\theta^x (1-\\theta)^{1-x}\\\
    &=(1-\\theta)\\left(\\frac{\\theta}{1-\\theta}\\right)^x\\\
    &=(1-\\theta)\\cdot\\exp(x\\log\\frac{\\theta}{1-\\theta})
    \\end{split}
    \\]
    Then, we have, $f(x)=1,g(\\theta)=(1-\\theta),c=1,\\phi(\\theta)=\\log\\frac{\\theta}{1-\\theta},h(x)=x$.
    - [**poisson**]  
    \\[
        p(x\|\\theta)=\\frac{\\theta^x\\cdot e^{-\\theta}}{x!}=\\frac{1}{x!}\\exp(-\\theta)\\cdot\\exp(x\\log\\theta)
    \\]
    where, $f(x)=\\frac{1}{x!}, g(\\theta)=\\exp(-\\theta),c=1,h(x)=x,\\phi(\\theta)=\\log(\\theta)$.