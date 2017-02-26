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
### Hoeffding's Lemma  (from wikipedia)
Suppose $X$ is a real random variables with mean zero such that $p(x\\in[a,b])=1$. Then,
\\begin{equation}
E(e^{sX})\\leq \\exp\\left(\\frac{1}{8}s^2(b-a)^2\\right)
\\end{equation}

***
### Hoeffding's Inequality  (from wikipedia)  
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
By the way, here, we can using the cramer transform, that is,
\\[
\\psi\_X(s)=\\frac{1}{8}s^2\\sum\_{i=1}^n(b\_i-a\_i)^2
\\]
and the convex conjugate is
\\[
\\psi^*\_X(t)=\\frac{2t^2}{\\sum\_{i=1}^n(b\_i-a\_i)^2}
\\]

***
### Bennett's Inequality -- (from wikipedia)
- [**brief introduce**] In probability thoery, Bennett's Inequality provides an uppder bound on the probability that the sum of independent variables deviates from its expected value by more than any specified amount.
- [**theorem**]  
Let $X\_1,...,X\_n$ be independent random variables, and assume (for simplicity but without loss of generality) they all have zero expected value. Further assume $\|X\_j\|\\leq a$ almost surely for all $i$, and let,
\\[
\\sigma^2=\\frac{1}{n}\\sum\_{i=1}^n Var(X\_i)
\\]
Then for any $t\\geq 0$,
\\[
P\\left(\\sum\_{i=1}^n X\_i >t \\right)\\leq \\exp\\left( -\\frac{n\\sigma^2}{a^2}h\\left(\\frac{at}{n\\sigma^2}\\right) \\right)
\\]
where, $h(u)=(1+u)\\log(1+u)-u$.

***
### Bernstein's Inequality ###
Let $X\_1,...,X\_n$ be independent zero-mean variables. Suppose that $\|X\_i\|\\leq M$ almost surely, for all $i$. Then, for all positive $t$,
\\[
P\\left(\\sum\_{i=1}^n X\_i > t\\right)\\leq \\exp\\left(-\\frac{t^2}{2\\left(\\sum\_{j=1}^n E[X\_j^2] +\\frac{Mt}{3}\\right) } \\right)
\\]
- [**proof.**] Let $h(x)=(1+x)\\log(1+x)-x$ for $x\\geq 0$. And $h(x)\\geq \\frac{x^2}{2(1+\\frac{x}{3})}=g(x)$ (*can be proofed by using taylor's expansion*). So, from Bennett's inequality, it's easy to get,
\\[
\\begin{split}
P\\left(\\sum\_{i=1}^n X\_i >t\\right)&\\leq \\exp\\left( -\\frac{n\\sigma^2}{a^2}h\\left(\\frac{at}{n\\sigma^2}\\right)\\right)\\\
&\\leq \\exp\\left( -\\frac{n\\sigma^2}{a^2}g(\\frac{at}{n\\sigma^2})\\right)\\\
&=\\exp\\left(-\\frac{t^2}{2\\left(\\sum\_{j=1}^n E[X\_j^2]+\\frac{at}{3}\\right)}\\right)
\\end{split}
\\]


***
### Random Projection
Let $U=[u\_1,...,u\_p]^T\\in R^p$, $R\\in R^{p\\times d}, R^TR=I\_d$. Let $V=\\sqrt{\\frac{p}{d}}R^TU$. Then $E(\\mid\\mid V\\mid\\mid\_2^2)=\|\|U\|\|\_2^2$.

- [**lemma**]  
    Let $R$ be a random matrix of order $k\\times d$, i.e.,$R\_{ij}\\sim N(0,1)$, and $u$ be any fixed vector $\\in R^{d}$. Define $v=\\frac{1}{\\sqrt{k}}R\\cdot u$. Thus $v\\in R^k$ and $v\_i=\\frac{1}{\\sqrt{k}}\\sum\_i R\_{ij}u\_j$. Then,
    - $E[\|\| v \|\|\_2^2]=\|\| u\|\|\_2^2$
    - $P(\|\|\|v\|\|^2 -\|\|u\|\|^2 \\geq \|\| u\|\|^2\|)\\leq 2\\exp\\left(-(\\epsilon^2-\\epsilon^3)\\frac{k}{4} \\right)$  
    **proof1.** 
\\[
\\begin{split}
E(\|\|v\|\|\_2^2)&= E\\left( \\sum\_i v\_i^2\\right)\\\
&=\\sum\_i^k E(v\_i^2)\\\
&=\\sum\_i^k\\frac{1}{k}E\\left(\\left(\\sum\_i R\_{ij}u\_j\\right)^2\\right)\\\
&=\\sum\_{k=1}^k \\frac{1}{k}\\sum\_{1\\leq j\\leq d} u\_j^2\\\
&=\\sum\_{1\\leq j\\leq d} u\_j^2\\\
&=\|\|u\|\|\_2^2
\\end{split}
\\]

    **proof2**  
    Let $X=k\\cdot \\frac{\|\|v\|\|^2}{\|\|u\|\|^2}=\\frac{\\sum\_{j=1}^k (R\_{j} u)^2}{\|\| u\|\|^2}=\\sum\_{j=1}^k X\_j^2$, where $X\_j=\\frac{R\_ju}{\|\|u\|\|}$. Since $R\_j \\sim N(0,I\_p)$, so, $X\_i\\sim N(0,1)$.
\\[
\\begin{split}
P\\left(\\parallel v\\parallel^2 \\geq (1+\\epsilon)\\parallel u\\parallel^2\\right)&= P(X\\geq (1+\\epsilon)\\cdot k)\\\
&= P(e^{\\lambda X}\\geq e^{\\lambda(1+\\epsilon)k})\\\
&\\leq \\frac{E(e^{\\lambda X})}{e^{\\lambda(1+\\epsilon)k}}\\\
&=\\frac{\\prod\_{i=1}^d E\\left( e^{\\lambda X\_i^2}\\right)}{e^{\\lambda(1+\\epsilon)k}}\\\
&=\\left( \\frac{Ee^{\\lambda X\_i^2}}{e^{\\lambda(1+\\epsilon)}} \\right)^k
\\end{split}
\\]
Since, $Ee^{\\lambda X\_i^2}=\\int e^{\\lambda X\_i^2}\\phi(x\_i)dx\_i =\\frac{1}{\\sqrt{1-2\\lambda}} $, where $\\phi(x)$ is the p.d.f. of the standard normal distribution. Thus,
\\[
P(X\\geq (1+\\epsilon)\\cdot k) \\leq \\left( \\frac{e^{-2(1+\\epsilon)\\lambda}}{1-2\\lambda} \\right)^{k/2}
\\]
where $\\lambda\\in (0,1/2)$.

Let $\\lambda=\\frac{\\epsilon}{2(1+\\epsilon)}$, then 
\\[
P(X\\geq (1+\\epsilon)\\cdot k) \\leq \\left((1+\\epsilon)e^\\epsilon \\right)^{k/2}
\\]
And, $1+\\epsilon < e^{\\epsilon -\\frac{\\epsilon^2-\\epsilon^3}{2}}$. So,
\\[
P(X\\geq (1+\\epsilon)\\cdot k) \\leq e^\\left(-(\\epsilon^2-\\epsilon^3)k/4 \\right)
\\]

***
### John-Lidenstrauss Lemma
- [**brief introduction.**]  The lemma states that a small set of points in a high-dimensional can be embedded into a space of much lower dimension in such a way that distance between the points are nearly preserved. The map used for the embedding is at least Lipschitz, and can even be taken to be an orthogonal projection.
- [**lemma**]  Let $R:R^p\\rightarrow R^d$. Let $A$ be finite subset of $R^p$ with $\|A\|=n$. Assume that for some $\\nu \\geq 1$, $R\_{ij}\\in G(\\nu)$, and $R\_{ij}\\sim N(0,1)$. And let $\\epsilon,\\sigma\\in (0,1)$. If $d\\geq 100\\nu^2 \\epsilon^{-2}\\log\\left(\\frac{n}{\\sqrt{\\sigma}} \\right)$. There with probability at least $1-\\sigma$,
\\[
(1-\\epsilon)\\parallel X-Y\\parallel^2 \\leq \\parallel R^TX-R^TY\\parallel^2\\leq (1+\\epsilon)\\parallel X-Y\\parallel^2
\\]

- [**Lipshitz.**]  In mathematical analysis, **Lipschitz continuity**, named after Rudolf Lipschitz, is a strong form of uniform continuity for functions. Intuitively, a Lipschitz continuous function is limited in how fast it can change: there exists a definite real number such that, for every pair of points on the graph of this function, the absolute value of the slope of the line connecting them is not greater than this real number; this bound is called a *Lipschitz constant* of the function. For instance, every function that has bounded first derivatives is Lipschitz.
    + [**definition**]  
    Given two metric space $(X,d\_X)$ and $(Y,d\_Y)$, where $d\_X,d\_Y$ denotes the metric on the set $X,Y$ respectively. A function $f:X\\rightarrow Y$ is called **Lipschitz continuous** if there exists a real constant $C\\geq 0$ such that, for all $x\_1,x\_2$ in $X$,
    \\[
        d\_Y(f(x\_1,x\_2))\\leq K d\_X(x\_1,x\_2)
    \\]
    Any such $K$ is referred to as a **Lipschitz constant** for the function $f$. The smallest constant is sometimes called **the (best) Lipschitz constant**.
    + [**example**]  
        - $f(x)=\\sqrt{x^2+5}$ defined for all real numbers is Linpschitz continuous with constant $K=1$.
        - $f(x)=sin(x)$ is Lipschitz continuous because its derivative, the cosine function, is bounded above by 1 in absolute value.