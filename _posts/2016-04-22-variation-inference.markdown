---
layout: post
title: variational inference
date: 2016-04-22 12:58:05 +1000 
categories: MachineLearning
---



----------

### Main Idea ###
The main idea behind variational methods is to pick a family of distributions over the latent variables with its own _variational parameter_
\\[
q(z_{1:m}| \alpha)
\\]
Then find the setting of the parameters that makes $q$ close to the posterior of interest.

Use $q$ with the fitted parameters as a proxy for the posterior, e.g., to form predictions about future data or to investigate the posterior distribution of the hidden variables.

### Using KL divergence to measure the closeness of two distributions ###
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

The last inequality is the **ELBO**, and applies the Jensen's inequality. We choose a family of variational distributions (i.e., a parameterization of a distribution of the latent variables, in another words, functional of distribution) such that the expectations are computable.

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

Notice that $\ln p(x)$ does not depend on $q$. So, as a function of the variational distribution, minimizing the KL divergence is the same as maximizing the ELBO.