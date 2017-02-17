---
layout: postarticle
title: multinomial distribution
date: 2016-05-24 12:09:05 +1000 
categories: math
comments: true
---

### multinomial  ###
- [**brief introduce**]   
    设某随机实验有$A\_1,...,A\_k$个结果，分别将它们出现的次数标记为随机变量$X\_1,...,X\_k$.它们的概率分布是$p\_1,...,p\_k$,那么在$n$次实验中，$A\_1$出现$n\_1$次，$A\_k$出现$n\_k$次的事件概率为
\\[
p(X\_1=n\_1,X\_2=n\_2,...,X\_k=n\_k)= \frac{ \Gamma( \sum\_i n\_i)}{ \Gamma(n\_1)... \Gamma(n\_k)} \prod\_{i=1}^k p\_i^{n\_i}
\\]

    For the random variable result $n\_1$, it represents the frequency of the result $A\_1$ appeared in the experiment, also the same as the $n\_2,...,n\_k$. So the meaning of the $p(n\_1,...,n\_k)$ is the joint probability of that $A\_1$ occurred $n\_1$ times and $A\_2$ occurred $n\_2$ times etc.

+ [**properties**]  
    - $E(X\_i)=np\_i$
    - $var(X\_i)=np\_i(1-p\_i)$
    - $cov(X\_i,X\_j)=-np\_ip\_j$
+ [**marginal distribution**]   
    The marginal distribution of $X^{m}=(X_1,...,X_m)^T, (m\\le k)$ is the multinomial distribution,
\\[
M(x^{m}|(p\_1,...,p\_m))
\\]
+ [**conditional distribution**]   
    The conditional distribution of $X^{m}$ given the remaining $X\_i$'s is also multinomial,
\\[
p(x^{m}|x\_{m+1},...,x\_k) \\sim M\_{m-1}(x^{m}|p\_1',...,p\_m'),n-s)
\\]
    where $p\_i'=\\frac{p\_i}{\\sum\_{j=1}^mp\_j},(1\\leq i\\leq m)$ and $s=\\sum_{i=m+1}^k x\_i$.

    *proof.* prompt: using multinomial theorem.



### dirichlet distribution###
+ [**brief introduce**] If we treat the parameters $p\_1,...,p\_k$ as a random variable vector, with which obey a distribution. Then we could palce a conjugate prior distribution to it, and the distribution could be **dirichlet distribution**

+ [**pdf**]
\\[
p(p\_1,...,p\_k;\alpha\_1,...,\alpha\_k)=\frac{\Gamma(\sum\_{i=1}^k \alpha\_i)}{\prod\_{i=1}^k \Gamma(\alpha\_i)} \prod\_{i=1}^k p\_i^{\alpha\_i-1}
\\]
when $k=1$, the pdf is beta distribution.

+ [**properties**]  
    - $E(p\_i)=\\frac{\\alpha\_i} {\\sum\_{i=1}^k \\alpha\_i}$
    - $var(p\_i)=\\frac{E(p\_i)(1-E(p\_i))}{1+\\sum\_{j=1}^k \\alpha\_j}$
    - $cov(p\_i,p\_j)=\\frac{E(p\_i)E(p\_j)}{1+\\sum\_{j=1}^k \\alpha\_j}$

+ [**marginal**]
    The marginal distribution $P^{m}=(p\_1,...,p\_m)^T,(m\le k)$ is the dirichlet distribution,
\\[
Dir(P^{m}|(\\alpha\_1,...,\\alpha\_m),\\sum\_{i=m+1}^k \\alpha_i)
\\]

+ [**conditional**]
    The conditional distribution of $P^{m}$ given the $(p\_{m+1},...,p\_k)$ of $Y\_i=\\frac{p\_i}{1-\\sum\_{j=m+1}^k  p\_j}$ is also the dirichlet distribution,
\\[
Dir(Y^{m}|(\\alpha\_1,...,\\alpha\_m),\\sum\_{i=m+1}^k \\alpha_i)
\\]




### multinomial,binomial ,categorical ,bernoulli###

假设有$k$个桶，$n$个球，每个桶中的球的个数为$x\_i$,概率为$p\_i$.那么掉入每个桶中的球的个数服从以下分布，

<table class="table">
<tr>
<td>分布</td><td>球的个数</td><td>桶数</td><td>掉入桶的概率</td>
</tr>
<tr>
<td>multinomial</td><td>$n$</td><td>$k$</td><td>$p\_1,p\_2,...,p\_k$</td>
</tr>
<tr>
<td>binomial</td><td>$n$</td><td>2</td><td>$p$(另一个为$1-p$)</td>
</tr>
<tr>
<td>categorical</td><td>1</td><td>$k$</td><td>$p\_1,p\_2,...,p\_k$</td>
</tr>
<tr>
<td>bernolli</td><td>1</td><td>2</td><td>$p$(另一个为$1-p$)</td>
</tr>
</table>

