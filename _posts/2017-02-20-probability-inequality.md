---
layout: postarticle
title: probability inequality
date: 2017-02-12 14:11:05 +1000
categories: MachineLearning
comments: true
---
<h1></h1>
### Jensen Inequality ###
If $g$ is convex, then 
    \\[
        E[g(X)]\\geq g(E(X))
    \\]
    $f(x)=\\log(x)$ is not convex, but $f(x)=-\\log(x)$ is a convex function.

<h1></h1>
###Cauchy-Schwartz Inequality###
If $X$ and $Y$ have finite variances, then,
\\[
    E|XY|\\leq \\sqrt{E(X^2)E(Y^2)}
\\]

<h1></h1>
###Markov Inequality###
For all $t\\ge 0$,
\\[
\\begin{split}
Y1\\{Y\\geq t\\} &\\geq t1\\{y\\geq t\\}\\\
E(Y1\\{Y\\geq t\\}) &\\geq tE(1\\{Y\\geq t\\})\\\
P(\\{Y\\geq t\\})&\\leq E(Y1\\{Y\\geq t\\})/t
\\end{split}
\\]
If $Y>0$, then,
\\[
P(\\{ Y\\geq t\\})\\leq \\frac{E(Y)}{t   }
\\]
- Let $Y=\|Z-E(Z)\|$, then,
\\[
P(\|Z-E(Z)\|\\geq t)\\leq \\frac{E(\|Z-E(Z)\|)}{t}
\\]
- If $\\phi(x)$ is nondecrease,nonnegative,
\\[
P(\\{Y\\geq t\\})\\leq P(\\phi(Y)\\geq \\phi(t))=\\frac{E(\\phi(Y))}{\\phi(t)}
\\]
    - [**Chebyshev Inequality**] Let $\\phi(t)=t^2,Y=\|Z-E(Z)\|$,
    \\[
        P(\\{Z-E(Z)\\}\\geq t)\\leq \\frac{E(\|Z-E(Z)\|^2)}{t^2}=\\frac{Var(Z)}{t^2}
    \\]
    - [**more generally**]  Let $\\phi(t)=t^q$, then for some $q>0$, we have,
    \\[
        P(\\{ Z-E(Z)\\}\\geq t)\\leq \\frac{E(\|Z-E(Z)\|^q)}{t^q}
    \\]


<h1></h1>
###Cramer-Chernoff Method###
Let $Z$ be a real-valued random variable. For all $\\lambda\\geq 0$, we have,
\\[
P(\\{Z\\geq t\\})\\leq \\exp(-\\lambda t)\\cdot E(\\exp(\\lambda Z))
\\]
Then, **we want to minimize the upper bound**, that is, chose a best $\\lambda$ value.
So, we want to resolve,
\\[
\\inf\_{\\lambda\\geq 0} e^{-\\lambda t}E(e^{\\lambda Z}) \\equiv \\inf\_{\\lambda t \\geq 0} -\\lambda+\\log E(e^{\\lambda Z})
\\]
Define, $\\psi\_Z(\\lambda)=\\log E(e^{\\lambda Z})$. Let $\\psi\_Z^\*(\\lambda)=\\sup\_{\\lambda\\geq 0} \\lambda t-\\psi\_Z(\\lambda)$, which is called the cramer transform of $Z$. Then, we only need to compute 
\\[
\\psi\_Z^\*(t)=\\lambda^\*t-\\psi\_Z(\\lambda^\*)
\\]
where, $\\lambda^\*$ is the solution of $t-\\psi\_Z'(\\lambda)=0$. And, then we get the **upper bound** is,
\\[
P(\\{Z\\geq t\\})\\leq\\exp(-\\psi\_Z^\*(t))
\\]

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