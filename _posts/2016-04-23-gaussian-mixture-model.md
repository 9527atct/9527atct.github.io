---
layout: post
title: gaussian mixture model (GMM)
date: 2016-04-23 15:24:05 +1000 
categories: MachineLearning
comments: true
---

----------

### conditions ###
- suppose latent factor $z \in \{e_1,...,e_m\}, e_i={0,...,i,0,...0}$.
- $p(z=e_k)= \alpha_k$.
- Given $Z=e_k$, $x \sim N( \mu_k, C_k)$, where $ \mu_1,..., \mu_m \in R^d$, and , $C_1,...,C_m$ are $d \times d$ cov matrices.

### mixture distributions ###
The mixture guassian marginal distribution
\\[
\begin{split}
p(x) &= \sum_z p(x|z)p(z) \\\
&= \sum_{k=1}^m p(z=e_k)p(x| z=e_k) \\\
&= \sum_{k=1}^m \alpha_k N(x| \mu_k, C_k)
\end{split}
\\]

And, the joint distribution is,
\\[
p(x,z)= \prod_{k=1}^m \alpha^{z_k} N(x| \mu_k, C_k)^{z_k}
\\]

the posterior distribution is,
\\[
p(z=e_k | x) = \frac{p(x|z=e_k)p(z=e_k}{p(x)}=\frac{ \alpha_k N(x | \mu_k,C_k)}{ \sum_{k=1}^m  \alpha_k N(x | \mu_k,C_k)}
\\]

### EM for GMM ###


### Expectation Maximization Algorithm ###
- Given $x=(x_1,...,x_n)
- $(x,z) \sim p_{\theta} for some undnown $\theta \in \Theta$
- Goal: $\theta_{MLE} = \arg\max_{ \theta} p_{ \theta}(x)$
- Issue: $p_{ \theta}(x) = \sum_{z} p_{ \theta}(x,z) difficult to maximize.
- Alg: initialize $ \theta_0 \in \Theta $
  1. for t=0,1,2,...,(until convergence)
  2. E-step: $Q( \theta, \theta_{t}) = E_{ \theta_t}( \ln p_{ \theta}(x,z)|X=x)
  3. M-step: $ \theta_{t+1} = \arg\max_{ \theta} Q( \theta, \theta_t) 