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
    - [**from prof. zhihua Zhang's manuscript**]  
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
    - [**example 1**]  
    For a Bernoulli sequence $X\_1,...,X\_n$,
    \\[
    \\begin{split}
    p(x\_1,...,x\_n)&=\\int\_0^1 p(x\_1,...,x\_n\|\\theta)dF(\\theta)\\\
    &=\\int\_0^1 \\prod\_{i=1}^n B(x\|\\theta)dF(\\theta)\\\
    &=\\int\_0^1 \\theta^{S\_n}(1-\\theta)^{n-S\_n}dF(\\theta)
    \\end{split}
    \\]
    where, $S\_n=x\_1+...,+x\_n$. So,
    \\[
        p(x\_1,...+x\_n\|\\theta)=\\theta^{S\_n}(1-\\theta)^{n-S\_n}
    \\]
    Let $t\_n=[n,S\_n]$, then $p(x\_1,...,x_n\|\\theta)$ can be factorized into $h\_n=\\theta^{S\_n}(1-\\theta)^{n-S\_n}$ and $g=1$. So, $t\_n$ is the sufficient statistic of Bernoulli distribution.
    - [**example 2: Normal Distribution**]  
    \\[
    \\begin{split}
        p(x\_1,...,x\_n\|\\mu,\\lambda)&=\\prod\_{i=1}^n \\left(\\frac{\\lambda}{2\\pi}\\right)^{\\frac{1}{2}}\\exp\\left(-\\frac{\\lambda}{2}(x\_i -\\mu)^2 \\right)\\\
        &=\\left(\\frac{\\lambda}{2\\pi}\\right)^{\\frac{n}{2}}\\exp\\left(-\\frac{\\lambda}{2}\\sum\_{i=1}^n(x\_i -\\mu)^2 \\right)\\\
        &=\\left(\\frac{\\lambda}{2\\pi}\\right)^{\\frac{n}{2}}\\exp\\left(-\\frac{\\lambda}{2}[n(\\bar{x}-\\mu)^2+nS\_n^2]\\right)\\\
    \\end{split}
    \\]
    where $\\bar{x}=\\frac{1}{n}\\sum\_{i=1}^nx\_i, S\_n^2=\\frac{1}{n}\\sum\_{i=1}^n(x\_i-\\bar{x})^2$. So the sufficient statistic can be $[n,\\bar{x},S\_n^2]$. Note that the sufficient statistic is not unique.  


 

### One-Parameter Exponential Family ###
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

    - [**normal with unknown variance**]  
    \\[
    \\begin{split}
        p(x\|\\theta)&=N(x\|0,\\sigma^2)\\\
        &=\\left( \\frac{1}{2\\pi\\sigma^2}\\right)^{\\frac{1}{2}}\\exp\\left(-\\frac{x^2}{2\\sigma^2}\\right)\\\
        &=\\left( \\frac{1}{2\\pi}\\right)^{\\frac{1}{2}}\\theta^{-\\frac{1}{2}}\\exp\\left(-\\frac{x^2}{2\\theta}\\right)\\\
    \\end{split}
    \\]
    where, $f(x)=\\left( \\frac{1}{2\\pi}\\right)^{\\frac{1}{2}}, g(\\theta)=\\theta^{-\\frac{1}{2}},c=-1/2,h(x)=x^2,\\phi(\\theta)=\\theta^{-1}$.
    - [**uniform**]  
    \\[
        p(x\|\\theta)=U(x\|[0,\\theta])=\\frac{1}{\\theta}
    \\]
    So, $f(x)=1,g(\\theta)=\\theta^{-1},c=1,h(x)=\\phi(\\theta)=0$. Since $\\mathcal{X}$ is $[0,\\theta]$, so it is no regular.


###K-Parameter Exponential Family###
- [**k-parameters exponential family**]  
A pdf(pmf) $p(x\|\\theta), x\\in \\mathcal{X}$, which is labelled by $\\theta\\in\\Theta\\subseteq R$ is said to belong to *k-parameters exponential family* if it is of the form
\\[
p(x\|\\theta)=f(x)g(\\theta)\\exp\\left(\\sum_{j=1}^k c\_j\\cdot\\phi\_j(\\theta)h\_j(x) \\right)
\\]
Denoted by $E\_{f\_k}(x\|f,g,h,\\phi,c,\\theta)$.

- [**sufficient statistic for $E\_{f\_k}$**]  
If $X\_1,...,X\_n\\in \\mathcal{X}$ is an exchangeable sequence such that given regular $E\_{f\_k}(X\|f,g,h,\\phi,c,\\theta)$,
\\[
p(x\_1,...,x\_n\|\\theta)=\\prod\_{i=1}^n E\_{f\_k}(x\_i\|f,g,h,\\phi,c,\\theta)
\\]
Then $t\_n=t\_n(X\_1,...,X\_n)=[n,\\sum_{i=1}^n h\_1(X_i),...,\\sum_{i=1}^n h\_1(X_i)]$ is sufficient statistic of $X\_1,...,X\_n$.
    - [**example:normal**]  
    Let $\\theta=[\\mu,\\lambda]$,
    \\[
    \\begin{split}
        p(x\|\\theta)&=N(x\|\\mu,\\lambda)\\\
        &=\\left( \\frac{\\lambda}{2\\pi}\\right)^{\\frac{1}{2}}\\exp\\left(-\\frac{\\lambda}{2}(x-\\mu)^2 \\right)\\\
        &=\\left( \\frac{\\lambda}{2\\pi}\\right)^{\\frac{1}{2}}\\lambda^{\\frac{1}{2}}\\exp\\left( -\\frac{\\lambda}{2}\\mu^2\\right)\\exp\\left(\\lambda\\mu x-\\frac{1}{2}\\lambda x^2\\right)
    \\end{split}
    \\]
    So, $g(\\theta)=\\lambda^{\\frac{1}{2}}\\exp\\left( -\\frac{\\lambda}{2}\\mu^2\\right),c\_1=1,c\_2=-\\frac{1}{2},\\phi\_1(\\theta)=\\lambda\\mu,\\phi\_2(\\theta)=\\lambda,h\_1(x)=x,h\_2(x)=x^2$. Sufficient statistic: $t\_n=[n,x,x^2]$.

### Natural Exponential Family###
- [**definition from prof. zhang's manuscript**]  
The pdf of exponential family,
\\[
    p(y\|\\varphi)=a(y)\\exp(y^T \\varphi-b(\\varphi))
\\]
where $y=(y\_1,...,y\_k),\\varphi=(\\varphi\_1,...,\\varphi\_k)$. Comparing to the previous form, we can see $y\_i=h\_i(x_i),\\varphi\_i=c\_i\\phi(\\theta)$.
- [**wiki definition**]  
The pdf of exponential family can be rewritten into another form:
\\[
    f(x\|\\theta)=h(x)\\exp(\\eta(\\theta)^TT(x)-A(\\theta))
\\]

- [**properties from wiki**]
The mean vector and covariance matrix are
\\[
E[X]=\\triangledown_{\varphi}b(\\varphi);\\quad Cov[X]=\\triangledown\\triangledown^T b(\\varphi)
\\]where $\\triangledown$ is the gradient, and $\\triangledown\\triangledown^T$ is the Hessian matrix.  
**proof.** Since $\\int a(y)\\exp(y^T \\varphi-b(\\varphi))dy=1$, taking derivation on both sides.
\\[
\\begin{split}
&\\int a(y)\\exp(y^T \\varphi-b(\\varphi))\\cdot (y-\\triangledown\_\\varphi b(\\varphi))dy=0 \\\
\\Longrightarrow &\\int a(y)\\exp(y^T \\varphi-b(\\varphi))\\cdot y dy=\\int a(y)\\exp(y^T \\varphi-b(\\varphi))\\cdot \\triangledown\_\\varphi b(\\varphi)dy\\\
\\Longrightarrow &E[y]=\\triangledown\_\\varphi b(\\varphi)\\\
\\end{split}
\\]
And keep on taking derivation on both sides, we will obtain,
\\[
\\begin{split}
&E[y^2]-(\\triangledown\_\\varphi b(\\varphi))^2=\\triangledown\\triangledown^T b(\\varphi)\\\
\\Longrightarrow &E[y^2]-E^2[y]=\\triangledown\\triangledown^T b(\\varphi)\\\
\\Longrightarrow &D(y)=\\triangledown\\triangledown^T b(\\varphi)\\\
\\end{split}
\\]
- [**example: possion distribution**]  
\\[
e^{-\\lambda}\\frac{\\lambda^2}{x!}=\\frac{1}{x!}\\exp(x\\log\\lambda-\\lambda)=\\frac{1}{x!}\\exp(x\\varphi-e^{\\varphi})
\\]
So, $E[y]=\\triangledown\_\\varphi b(\\varphi)=\\triangledown\_\\varphi e^\\varphi=e^\\varphi=\\lambda$.

- [**theorem**]  
If $X=(X\_1,...,X\_n)$ is random variable from a regular exponential family distribution such that
\\[
p(x\|\\theta)=\\prod\_{i=1}^n f(x\_i)[g(\\theta)]^n\\exp\\left( \\sum\_{j=1}^kc\_j\\phi\_j(\\theta)\\sum\_{i=1}^nh\_j(x\_i) \\right)
\\]
Then the conjugate family for $\\theta$ has the form
\\[
    p(\\theta\|\\tau)=[K(\\tau)]^{-1}[g(\\theta)]^{\\tau\_0}\\exp\\left( \\sum\_{j=1}^kc\_j\\phi(\\theta)\\tau\_j\\right)
\\]
where $[K(\\tau)]=\\int\_\\theta[g(\\theta)]^\\tau \\exp\\left(\\sum\_{j=1}^k c\_j\\phi\_j(\\theta)\\tau\_j \\right)d\\theta <\\infty$.
    - [**explain from wiki**]  
    Assume that the probability of a single observation follows an exponential family, parameterized using its natural parameter:
    \\[
        p(x\|\\eta)=h(x)g(\\eta)\\exp(\\eta^TT(x))
    \\]
    Then, for data $X=(X\_1,...,X\_n)$, the likelihood is computed as follows:
    \\[
        p(X\|\\eta)=\\left(\\prod\_{i=1}^n h(x\_i)\\right)g(\\eta)^n \\exp\\left(\\eta^T\\sum\_{i=1}^n T(x\_i) \\right) 
    \\]
    Then, for the above conjugate prior:
    \\[
        p(\\eta\|\\chi,\\nu)=f(\\chi,\\nu)g(\\eta)^\\nu\\exp(\\eta^T \\chi)
    \\]
    We can then compute the posterior as follows:
    \\[
    \\begin{split}
    p(\\eta\|X,\\chi,\\nu)&\\propto p(X\|\\eta)p(\\eta\|\\chi,\\nu)\\\
    &=\\left(\\prod\_{i=1}^n h(x\_i)\\right)g(\\eta)^n \\exp\\left(\\eta^T\\sum\_{i=1}^n T(x\_i) \\right)f(\\chi,\\nu)g(\\eta)^\\nu\\exp(\\eta^T \\chi)\\\
    &\\propto g(\\eta)^n \\exp\\left(\\eta^T\\sum\_{i=1}^n T(x\_i) \\right) g(\\eta)^\\nu\\exp(\\eta^T \\chi)\\\
    &\\propto g(\\eta)^{n+\\nu}\\exp\\left(\\eta^T \\left(\\chi+\\sum\_{i=1}^nT(x\_i)\\right)\\right)
    \\end{split}
    \\]
    - [**example:bernoulli**]  
    \\[
    \\begin{split}
    p(x\|\\theta)&=\\prod\_{i=1}^n \\theta^{x\_i}(1-\\theta)^{(1-x\_i)}\\\
    &=(1-\\theta)^n \\exp\\left(\\log\\frac{\\theta}{1-\\theta}\\sum\_{i=1}^nx\_i \\right)
    \\end{split}
    \\]
    So, the conjugate prior can be,
    \\[
    \\begin{split}
    p(\\theta\|\\tau)&\\propto (1-\\theta)^{\\tau\_0} \\exp\\left(\\log\\frac{\\theta}{1-\\theta}\\tau\_1 \\right) \\\
    &\\propto (1-\\theta)^{\\tau\_0}\\left(\\frac{\\theta}{1-\\theta}\\right)^\\tau\_1\\\
    &\\propto \\theta^{\\tau\_1}(1-\\theta)^{\\tau\_0-\\tau\_1}
    \\end{split}
    \\]
    which is a beta distribution. 
    The update rule is,
    \\[
    \\begin{split}
    \\chi' &= \\chi + \\sum\_{i=1}^nT(x\_i)\\\
    \nu' &=\nu + n\\\
    \\end{split}
    \\]
    Then, the posterior has the form,
    \\[
    p(\\theta\|X,\\tau)\\propto \\theta^{\\sum\_{i=1}^n x\_i +\\tau\_1}(1-\\theta)^{n-\\sum\_{i=1}^n x\_i +\\tau\_0-\\tau\_1}
    \\]
    which is alos a beta distribution.