---
layout: post
title: gaussian mixture model (GMM)
date: 2016-04-23 15:24:05 +1000 
categories: MachineLearning
comments: true
---

----------

### conditions ###
- suppose latent factor $z \in \{e_1,...,e_m\}, e_i=[0,...,i,...0]$.
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
p(z=e_k | x) = \frac{p(x|z=e_k)p(z=e_k)}{p(x)}=\frac{ \alpha_k N(x | \mu_k,C_k)}{ \sum_{k=1}^m  \alpha_k N(x | \mu_k,C_k)}
\\]

### EM for GMM ###
In this case, parameters are $\theta = ( \alpha, \{ \mu_k \}, \{ C_k \})$.

EM is then to solve the following equation, and get the best $ \theta $.
\\[
E_{ \theta_{0}(s_i(X,Z)|X=x) = E_{ \theta s_i(X,Z)
\\]

The first things to do is to get the $s_i(X,Z)|X=x $. we know that,
\\[
\begin{split}
p(x,z) &= \prod_{k=1}^m \alpha^{z_k} N(x| \mu_k, C_k)^{z_k} \\\
&= \prod_{k=1}^m e^{z_k \ln \alpha_k } \sqrt{ \frac{ \mid \Lambda_k \mid}{2 \pi}} ^{z_k} e^{ \frac{-z_k}{2}(x- \mu_k)^T \Lambda_k (x- \mu_k)} \\\
& \propto e^{ \sum z_k \ln \alpha_k + \frac{z_k}{2} \ln \mid \Lambda_k \mid - \frac{z_k}{2}(x^Tx-2 \mu_k^T \Labda_k x + \mu_k^T \mu_k)  }
\end{split}
\\]




### Expectation Maximization Algorithm ###
- Given $x=(x_1,...,x_n)$
- $(x,z) \sim p_{\theta}$ for some undnown $\theta \in \Theta$
- Goal: $\theta_{MLE} = \arg\max_{ \theta} p_{ \theta}(x)$
- Issue: $p_{ \theta}(x) = \sum_{z} p_{ \theta}(x,z)$ difficult to maximize.
- Alg: initialize $ \theta_0 \in \Theta $
  1. for t=0,1,2,...,(until convergence)
  2. E-step: $ Q( \theta, \theta_{t}) = E_{ \theta_t} ( \ln p_{ \theta}(x,z) \| X=x))$
  3. M-step: $ \theta_{t+1} = \arg\max_{ \theta} Q( \theta, \theta_t) $
  
- motivation for the EM 
Specialize exponential family: $p_{ \theta}(x,z)= \frac{1}{C( \theta)}h(x,z)e^{g( \theta)^Ts(x,z)}$

Nature form: 
\\[ 
p_{ \theta}(x,z)= \frac{1}{C( \theta)}h(x,z)e^{ \theta^T s(x,z)} = e^{ \theta^T s(x,z) - \ln C( \theta)} h(x,z)
\\]

The derivative of the target log distribution
\\[
\begin{split}
\frac{ \partial}{ \partial \theta_{i}} \ln p_{ \theta}(x) &= \frac{1}{p_{ \theta}(x)} \sum_z \frac{ \partial}{ \partial \theta_{i}} p_{ \theta}(x,z) \\\
&= \frac{1}{p_{ \theta}(x)} \sum_z (s_i(x,z)- \frac{ \partial}{ \partial \theta_{i} } \ln C( \theta)) p_{\theta}(x,z) \\\
&= \frac{1}{p_{ \theta}(x)} \sum_z (s_i(x,z)- E_{ \theta}(s_i(x,z)) p_{ \theta}(x,z) \\\
&= \sum_{z} s_i(x,z) p_{ \theta}(z | x) - E_{ \theta} s_i(x,z) \\\
&= E_{ \theta}(s_i(x,z) | X=x)  - E_{ \theta} s_i(x,z)
\end{split}
\\]

Then we have,
\\[
E_{ \theta}(s_i(x,z) | X=x)  = E_{ \theta} s_i(x,z)
\\]

- ISSUE: often can't solve analytically for $\theta$.
- Answer: Iterate.
- Alg: Let $ \theta_0 \in \theta$
  1. for t=1,2,3,...
  2. solve $E_{ \theta_{t-1}}(s_i(x,z) \| X=x)  = E_{ \theta_t} s_i(x,z)$ for $\theta_t$

Standard EM:
function of $Q$ is,
\\[ 
Q( \theta, \theta_{t}) = E_{ \theta_t} ( \ln p_{ \theta}(x,z) \| X=x))
\\]

and,
\\[
p_{ \theta}(x,z)= e^{ \theta^T s(x,z) - \ln C( \theta)} h(x,z)
\\] 

log function of likelihood, 
\\[
\ln p_{ \theta}(x,z)=  \theta^T s(x,z) - \ln C( \theta) + \ln h(x,z) 
\\]

$Q$ can be rewritten as,
\\[
Q( \theta, \theta_0)= E_{\theta_0}( \ln p_{ \theta}(X,Z) \| X=x)= \theta^TE_{ \theta_0}(s(X,Z) \| X=x) - \ln C( \theta) + const
\\]

The derivative of $Q$ is,
\\[
\frac{ \partial}{ \partial \theta_i} Q( \theta, \theta_0) = E_{ \theta_0}(s_i(X,Z)|X=x) - E_{ \theta} s_i(X,Z) =0
\\]

Then, $\theta$ is our EM estimator result.

