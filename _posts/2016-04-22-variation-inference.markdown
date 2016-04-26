---
layout: post
title: variational inference
date: 2016-04-22 12:58:05 +1000 
categories: MachineLearning
comments: true
---



----------

### Main Idea ###

The main idea behind variational methods is to pick a family of distributions over the latent variables with its own _variational parameter_
\\[
q(z_{1:m}| \alpha)
\\]
Then find the setting of the parameters that makes $q$ close to the posterior of interest.

Use $q$ with the fitted parameters as a proxy for the posterior, e.g., to form predictions about future data or to investigate the posterior distribution of the hidden variables.

### Using KL  to measure the closeness ###
- The KL divergence for variational inference is
\\[
KL(q || p)=\int q(Z) \ln \{ \frac{q(Z)}{p(Z|x)} \}=E_q [ \ln \frac{q(Z)}{p(Z|x)}]
\\]

### The Evidence Lower Bound (ELBO) ###

- We actually can't minimize the KL divergence exactly, but we can minimize a function that is equal to it up to a constant. This is the *evidence lower bound* (**ELBO**)

\\[
\begin{split}
\ln p(x) &= \ln \int_z p(x,z) \\\
&= \ln \int_z p(x,z) \frac{q(z)}{p(x,z)} \\\
&= \ln (E_q [ \frac{p(x,Z)}{q(z)} ]) \\\
&\geq E_q[ \ln p(x,Z)] - E_q[q(Z)]
\end{split}
\\]

The last inequality is the **ELBO**, , and applies the Jensen's inequality. We choose a family of variational distributions (i.e., a parameterization of a distribution of the latent variables, in another words, functional of distribution) such that the expectations are computable.

### Take KL, ELBO together ###

- First
\\[
p(z|x)= \frac{p(z,x)}{p(x)}
\\]

- Second

\\[
\begin{split}
KL(q(z)||p(z|x)) &= E_q[ \ln \frac{q(Z)}{p(Z|x)}] \\\
&= E_q[ \ln q(Z)] - E_q[ \ln p(Z|x)] \\\
&= E_q[ \ln q(Z)] - E_q[ \ln p(x,Z)] + \ln p(x) \\\
&= \ln p(x) - (E_q[ \ln p(x,Z)] - E_q[q(Z)])
\end{split}
\\]

Notice that $\ln p(x)$ does not depend on $q$. So, as a function of the variational distribution, minimizing the KL divergence is the same as maximizing the ELBO, marked as $\mathcal{L}(q)$ .

\\[
\ln p(x) = KL(q||p) + \mathcal{L}(q)
\\]

### Mean Field Variational Inference ###

In mean field variational inference, we assume that the variational family factorizes,
\\[
q(z_1,...,z_m)= \prod_{j=1}^m q(z_j)
\\]
Each variable is independent.

Then, Using coordinate ascent inference, ELBO can be written as,
\\[
\mathcal{L}(q)= \ln p(x_{1:n}) + \sum_{j=1}^m E[ \ln p(z_j | z_{1:(j-1)}, x_{1:n})] - E_j[ \ln q(z_j)]
\\]

Consider the ELBO as a function of $q(z_k)$,  employ the chain rule with the variable $z_k$ as the last variable inte list, Then,
\\[
\mathcal{L}(q)=E[ \ln p(z_k |z_{-k},x)] - E_j[ \ln q(z_k)] + const
\\]

Write this object as a function of $q(z_k)$,
\\[
\mathcal{L} = \int q(z_k)E_{-k}[ \ln p(z_k| z_{-k},x)] dz_{k} - \int q(z_k) \ln q(z_k) dz_k
\\]

The derivative w.r.t. $q(z_k)$ is 
\\[
\frac{ d \mathcal{L} }{ dq(z_k)}= E_{-k}[ \ln p(z_k|z_{-k},x) ]- \ln q(z_k) = 0
\\]

This leads to the coordinate ascent update for $q(z_k)$
\\[
q^*(z_k) \propto \exp{ E_{-k} [ \ln p(z_k | Z_{-k},x)] }
\\]

But the denominator of the posterior does not depend on $z_j$, so
\\[
q^*(z_k) \propto \exp{ E_{-k} [ \ln p(z_k , Z_{-k},x)] }
\\]

The *coordinate ascent algorithm* is to iteratively update each $q(z_k)$. The ELBO converges to a local minimum. Use the resulting $q$ is as a proxy for the true posterior.

### working with exponential family conditional ###

- Compute the log of the conditional

\\[
\ln p(z_j | z_{-j},x) = \ln h(z_j) + \eta (z_{-j},x)^T t(z_j) - a( \eta (z_{-j}, x))
\\]

- Compute the expectation with respect to $q(z_{-j})$

\\[
E[ \ln p(z_j | z_{-j},x)]= \ln h(z_j) + E[ \eta(z_{-j},x)]^Tt(z_j) - E[a( \eta (z_{-j}, x)) ]
\\]

- Noting that the last term does not depend on $q_j$, this means that

\\[
q^*(z_j) \propto h(z_j) \exp E[ \eta(z_{-j},x)]^Tt(z_j)
\\]
and the normalizing constant is $E[a( \eta (z_{-j}, x)) ]$



----------

### Reference ###
[Variational Bayesian methods](https://en.wikipedia.org/wiki/Variational_Bayesian_methods)

[Variational Inference](https://www.cs.princeton.edu/courses/archive/fall11/cos597C/lectures/variational-inference-i.pdf)