---
layout: postarticle
title: probability inequality
date: 2017-02-20 14:11:05 +1000
categories: MachineLearning
comments: true
---
***
### Jensen Inequality ###
If $g$ is convex, then 
\\begin{equation}
    E[g(X)]\\geq g(E(X))
\\end{equation}
$f(x)=\\log(x)$ is not convex, but $f(x)=-\\log(x)$ is a convex function.  
  
      
***
### Cauchy-Schwartz Inequality ###
            
If $X$ and $Y$ have finite variances, then,
\\begin{equation}
    E|XY|\\leq \\sqrt{E(X^2)E(Y^2)}
\\end{equation}

***      
### Markov Inequality   
     
For all $t\\ge 0$,
\\[
\\begin{split}
Y1\\{Y\\geq t\\} &\\geq t1\\{y\\geq t\\}\\\
E(Y1\\{Y\\geq t\\}) &\\geq tE(1\\{Y\\geq t\\})\\\
P(\\{Y\\geq t\\})&\\leq E(Y1\\{Y\\geq t\\})/t
\\end{split}
\\]
If $Y>0$, then,
\\begin{equation}
P(\\{ Y\\geq t\\})\\leq \\frac{E(Y)}{t   }
\\end{equation}
- Let $Y=\|Z-E(Z)\|$, then,
\\begin{equation}
P(\|Z-E(Z)\|\\geq t)\\leq \\frac{E(\|Z-E(Z)\|)}{t}
\\end{equation}
- If $\\phi(x)$ is nondecrease,nonnegative,
\\begin{equation}
P(\\{Y\\geq t\\})\\leq P(\\phi(Y)\\geq \\phi(t))=\\frac{E(\\phi(Y))}{\\phi(t)}
\\end{equation}
    - [**Chebyshev Inequality**] Let $\\phi(t)=t^2,Y=\|Z-E(Z)\|$,

\\begin{equation}
P(\\{Z-E(Z)\\}\\geq t)\\leq \\frac{E(\|Z-E(Z)\|^2)}{t^2}=\\frac{Var(Z)}{t^2}
\\end{equation}
    - [**more generally**]  Let $\\phi(t)=t^q$, then for some $q>0$, we have,
}
\\begin{equation}
P(\\{ Z-E(Z)\\}\\geq t)\\leq \\frac{E(\|Z-E(Z)\|^q)}{t^q}
\\end{equation}


***
### Cramer-Chernoff Method      

Let $Z$ be a real-valued random variable. For all $\\lambda\\geq 0$, we have,
\\[
P(\\{Z\\geq t\\})\\leq \\exp(-\\lambda t)\\cdot E(\\exp(\\lambda Z))
\\]
Then, **we want to minimize the upper bound**, that is, chose a best $\\lambda$ value.
So, we want to resolve,
\\[
\\inf\_{\\lambda\\geq 0} e^{-\\lambda t}E(e^{\\lambda Z}) \\equiv \\inf\_{\\lambda t \\geq 0} -\\lambda+\\log E(e^{\\lambda Z})
\\]
Define, $\\psi\_Z(\\lambda)=\\log E(e^{\\lambda Z})$. Let $\\psi\_Z^\*(\\lambda)=\\sup\_{\\lambda\\geq 0} \\lambda t-\\psi\_Z(\\lambda)$, which is called the **cramer transform** of $Z$. Then, we only need to compute 
\\[
\\psi\_Z^\*(t)=\\lambda^\*t-\\psi\_Z(\\lambda^\*)
\\]
where, $\\lambda^\*$ is the solution of $t-\\psi\_Z'(\\lambda)=0$. And, then we get the **upper bound** is,
\\begin{equation}
P(\\{Z\\geq t\\})\\leq\\exp(-\\psi\_Z^\*(t))
\\end{equation}

- [**example**]  Let $Z\\sim N(0,\\sigma^2)$, then we have,
\\[
\\begin{split}
\\psi\_Z(\\lambda) &=\\log\\int e^{\\lambda z}\\frac{1}{\\sqrt{2\\pi}\\sigma}\\exp\\left(-\\frac{z^2}{2\\sigma^2}\\right)dz \\\
&=\\log\\int \\frac{1}{\\sqrt{2\\pi}\\sigma}\\exp\\left(-\\frac{z^2-2\\lambda\\sigma^2 z}{2\\sigma^2}\\right) dz\\\
&=\\log\\int \\frac{1}{\\sqrt{2\\pi}\\sigma}\\exp\\left(-\\frac{(z^2-\\lambda\\sigma^2)^2}{2\\sigma^2}\\right) \\exp\\left(-\\frac{\\lambda^2\\sigma^4}{2\\sigma^2}\\right)dz\\\
&=\\frac{\\lambda^2\\sigma^2}{2}
\\end{split}
\\]
And,
\\[
t-\\psi\_Z'(\\lambda)=\\lambda \\sigma^2=0
\\]
Then, we get $\\lambda^\*=\\frac{t}{\\sigma^2}$, and, $\\psi\_Z^\*(\\lambda^\*)=\\sup\_{\\lambda\\geq 0}\\{\\lambda\* t-\\psi\_Z(\\lambda^\*)\\}=t\\cdot \\frac{t}{\\sigma^2}-\\frac{t^2}{\\sigma^4}\\frac{\\sigma^2}{2}=\\frac{t^2}{2\\sigma^2}$.  
Finally, the upper bound is,
\\[
P(\\{Z\\geq t\\})\\leq \\exp\left(-\\psi\_Z^\*(\\lambda)\\right)=\\exp\\left(-\\frac{t^2}{2\\sigma^2}\\right)
\\]

***
### Hoeffding's Lemma  
Suppose $X$ is a real random variables with mean zero such that $p(x\\in[a,b])=1$. Then,
\\begin{equation}
E(e^{sX})\\leq \\exp(\\frac{1}{8}s^2(b-a)^2)
\\end{equation}

***
### Hoeffding's Inequality    
- [**brief introduce.**] In probability theory, Hoeffding's inequality provides an upper bound on the probability that the sum of random variables deviates from its expected value.  

Let $X\_1,...,X\_n$ be independent random variables bounded by the interval $[0,1]: 0\\leq X\_i\\leq 1$. We define the empirical mean of these variables by 
\\[
\\bar{X}=\\frac{1}{n}(X\_1+...+X\_n)
\\] 
One of the inequalities in **theorem 1** of Hoeffding:
\\begin{equation}
P(\\bar{X}-E[\\bar{X}]\\geq t)\\leq e^{-2nt^2}
\\end{equation}
**theorem 2** of Hoeffding is a generalization of the above inequality when it is known that $X\_i$ are strictly bounded by the interval $[a\_i,b\_i]$,
\\begin{equation}
P(\\bar{X}-E(\\bar{X})\\geq t)\\leq \\exp\\left( -\\frac{2n^2t^2}{\\sum\_{i=1}^n(b\_i-a\_i)^2}\\right)
\\end{equation}
which are valid for positive values of $t$.  
The inequalities can be also stated in terms of the sum
\\[
S\_n=X\_1+...+X\_n
\\]
of the random variables:
\\begin{equation}
P(S\_n-E(S\_n)\\geq t)\\leq \\exp\\left(-\\frac{2t^2}{\\sum\_{i=1}^n(b\_i-a\_i)^2}\\right)
\\end{equation}
- [**proof.**] Using the Hoeffding's Lemma, we can prove hoeffding inequality. Suppose $X\_1,...,X\_n$ are $n$ independent random variables such that,
\\[
P(x\_i\\in[a\_i,b\_i])=1, 1\\leq i \\leq n
\\]
Let $S\_n=X\_1+...+X\_n$. Then for $s,t\\geq 0$, Markov inequality and the independent of $X\_i$ implies:
\\[
\\begin{split}
P(S\_n-E(S\_n)\\geq t) &= P(e^{s(S\_n-E(S\_n))})\\geq e^{st})\\\
&\\leq e^{-st}E(e^{s(S\_n-E(S\_n))})\\\
&=e^{-st}\\prod\_{i=1}^n E\\left( e^{s(x\_i-E(x\_i)} \\right)\\\
&\\leq e^{-st}\\prod\_{i=1}^n e^{\\frac{s^2(b\_i-a\_i)^2}{8}}\\\
&=\\exp\\left( -st +\\frac{1}{8}s^2\\sum\_{i=1}^n(b\_i-a\_i)^2\\right)
\\end{split}
\\]
To get the best possible upper bound, we find the minimum of the right hand side of the last inequality as a function of $s$. Thus, we get,
\\[
P(S\_n-E(S\_n)\\geq t)\\leq \\exp\\left(-\\frac{2t^2}{\\sum\_{i=1}^n(b\_i-a\_i)^2}\\right)
\\]
Here, we can using the cramer transform, that is,
\\[
\\psi\_X(s)=\\frac{1}{8}s^2\\sum\_{i=1}^n(b\_i-a\_i)^2
\\]
and the convex conjugate is
\\[
\\psi^*\_X(t)=\\frac{2t^2}{\\sum\_{i=1}^n(b\_i-a\_i)^2}
\\]
