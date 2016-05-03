---
layout: post
title: gaussian mixture model (GMM)
date: 2016-04-23 15:24:05 +1000 
categories: MachineLearning
comments: true
---

----------

### conditions ###
------------------

- suppose latent factor $z \in \{e_1,...,e_m\}, e_i=[0,...,i,...0]$.
- $p(z=e_k)= \alpha_k$.
- Given $Z=e_k$, $x \sim N( \mu_k, C_k)$, where $ \mu_1,..., \mu_m \in R^d$, and , $C_1,...,C_m$ are $d \times d$ cov matrices.

### mixture distributions ###
-----------------------------

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
------------------

-  EM MLE

In this case, parameters are $\theta = ( \alpha, [ \mu_k ], [ C_k ])$.

EM is then to solve the following equation, and get the best $ \theta $. for each $j$
\\[
E_{ \theta_{0}}[s_j(X,Z)|X=x] = E_{ \theta}[ s_j(X,Z)]
\\]

The first things to do is to get the $s_i(X,Z)|X=x $. we know that,
\\[
\begin{split}
p(x,z) &= \prod_{k=1}^m \alpha^{z_k} N(x| \mu_k, C_k)^{z_k} \\\
&= \prod_{k=1}^m e^{z_k \ln \alpha_k } \sqrt{ \frac{ \mid \Lambda_k \mid}{2 \pi}} ^{z_k} e^{ \frac{-z_k}{2}(x- \mu_k)^T \Lambda_k (x- \mu_k)} \\\
& \propto \exp( \sum_{k=1}^m z_k \ln \alpha_k + \frac{z_k}{2} \ln \mid \Lambda_k \mid - \frac{z_k}{2}(x^T \Lambda_k x-2 \mu_k^T \Lambda_k x + \mu_k^T \Lambda_k \mu_k)  )  \\\
&= \exp (\sum z_k \beta_k -\frac{1}{2} \sum Tr(z_k xx^T \Lambda_k) + \sum z_kx^T \Lambda_k \mu_k)
\end{split}
\\]
where, $\beta_k = \ln \alpha_k + \frac{1}{2} \ln \mid \Lambda_k \mid - \frac{ 1}{2} \mu_k^T \Lambda_k \mu_k$. 

And, Sufficient statistic is $z, z_kxx^T [k=1,...m], z_kx [k=1,...,m]$

- Multiple  $x_i=(X_{i1},...,X_{id}), z_i=(Z_{i1},...,Z_{im})$
\\[
\begin{split}
p_{ \theta}(x_1,...,x_n,z_1,...,z_n) &= \prod_{i=1}^n p_{ \theta}(x_i,z_i) \\\
&= \exp ( \sum_k( \sum_i z_{ik} ) \beta_k -\frac{1}{2} \sum_k Tr(( \sum_i z_{ik}x_i x_i^T) \Lambda_k ) + \sum_k ( \sum_i z_{ik}x_i^T) \Lambda_k \mu_k   )
\end{split}
\\]

sufficient statistic is, $\sum_i z_{ik}, \sum_i z_{ik}x_i x_i^T, \sum_i z_{ik}x_i^T $.

the following character $x=(x_1,...,x_n), z=(z_1,...,z_n)$ is a sequence of observation value, so, either $x_i$ or $z_i$ is a vector.


1. $E_{ \theta_{0}}[ \sum_i z_{ik} \| X=x] = E_{ \theta} [ \sum_i z_{ik}]$. 
   the right part of equation is,
\\[
E_{ \theta} ( \sum_i z_{ik})= \sum_i E_{ \theta}[z_{ik}]= \sum_i \alpha_k = n \alpha_k
\\]
  the left,
\\[
E_{ \theta_{0}}( \sum_i z_{ik} \| X=x) = \sum_i E_{ \theta_0} [ z_{ik} | x_i] = \sum_i \gamma_{ik} = n_k
\\]
where $ \gamma_{ik} = \frac{ \alpha_k \times p(x_i \| \theta_0^k)} {  \sum_{l} \alpha_{l} \times p(x_i \| \theta_0^{l}) }$. 
  so, put it together, the parameter $\alpha_k$ estimator is,
\\[
\alpha_k = \frac{n_k}{n}
\\]

2. $E_{ \theta_0} [ \sum_i z_{ik}x_i | x] = E_{ \theta} [ \sum_i z_{ik} X_i]$. 
the left part of equation is,
\\[
\begin{split}
E_{ \theta_0} [ \sum_i z_{ik}x_i | x] &= \sum_i E_{ \theta_0} [ z_{ik}|x]x_i \\\
&= \sum_i \gamma_{ik}x_i
\end{split}
\\]
the right,
\\[
\begin{split}
E_{ \theta} [ \sum_i z_{ik} X_i] &= \sum_i E_{ \theta}[ E_{ \theta}[z_{ik}X_i|z_{ik}]] \\\
&= \sum_i p_{ \theta}(z_{ik}=1) \mu_k \\\
&= \sum_i \alpha_k \mu_k \\\ 
&= n \alpha_k \mu_k \\\
&= n_k \mu_k
\end{split}
\\]
put it together,
\\[
\mu_k = \frac{1}{n_k} \sum_i \gamma_{ik} x_i
\\]

3. $E_{ \theta_0}[ \sum_i z_{ik} x_i x_i^T \| X=x] = E_{ \theta}[ \sum_{i} z_{ik} x_i x_i^T]$. the left is,
\\[
E_{ \theta_0}[ \sum_i z_{ik} x_i x_i^T \| X=x] = \sum_{i} \gamma_ik x_i x_i^T
\\]
the right is,
\\[
\begin{split}
E_{ \theta}[ \sum_{i} z_{ik} x_i x_i^T] &= \sum_i E_{ \theta} [z_{ik} x_i x_i^T | z_{ik}] \\\
&= \sum_i p_{ \theta}(z_{ik}=1)(C_k + \mu_k \mu_k^T) \\\
&= n \alpha_k (z_{ik}=1)(C_k + \mu_k \mu_k^T) \\\
&= n_k (z_{ik}=1)(C_k + \mu_k \mu_k^T)
\end{split}
\\]
put together,
\\[
C_k = ( \frac{1}{n_k} \sum_i \gamma_{ik} x_i x_i^T) - \mu_k \mu_k^T
\\]


-  EM MAP estimation


In EM MAP estimation, the auxiliary function is,

\\[
Q( \theta, \theta^{old})= \left[ \sum_i \sum_k \gamma_{ik} \ln \pi_{ik} + \sum_i \sum_k \gamma_{ik} \ln p(x_i | \theta_k)  \right] + \ln p( \pi) + \sum_k \ln p( \theta_k)
\\]
where $ \ln p( \pi) + \sum_k \ln p( \theta_k)$ is added prior information.

-  E step: remains unchanged. <br/>

it is natural to use a Dirichlet prior, $\pi \sim Dir( \alpha)$, since this is conjugate to the categorical distribution. The MAP estimate is given by 

\\[
\pi_k = \frac{ \gamma_k + \alpha_k - 1}{N + \sum_k \alpha_k -K}
\\]

-  M step: consider a conjugate prior 

\\[
p( \mu_k, \Sigma_k)= NIW( \mu_k, \Sigma_k | m_0, \kappa_0, \nu_0, S_0)
\\]

Then, the MAP estimate is given by

\\[
\hat{ \mu}_k = \frac{ \gamma_k \bar{x}_k + \kappa_0 m_0}{ \gamma_k + \kappa_0} 
\\]

\\[
\hat{ \Sigma}_k = \frac{ S_0 + S_k + \frac{ \kappa_0 \gamma_k}{ \kappa_0 + \gamma_k} ( \bar{x}_k - m_0)( \bar{x}_k - m_0)^T}{ \nu_0 + \gamma_k + D + 2} 
\\]

\\[
\bar{x}_k = \frac{ \sum_i \gamma_{ik} x_i}{ \gamma_k} 
\\]

\\[
S_k = \sum_i \gamma_{ik}(x_i - \bar{x}_k)(x_i - \bar{x}_k)^T
\\]

3. Prior Hyperparameters




### Expectation Maximization Algorithm ###
------------------------------------------

- Given $x=(x_1,...,x_n)$
- $(x,z) \sim p_{\theta}$ for some undnown $\theta \in \Theta$
- Goal: $\theta_{MLE} = \arg\max_{ \theta} p_{ \theta}(x)$
- Issue: $p_{ \theta}(x) = \sum_{z} p_{ \theta}(x,z)$ difficult to maximize.
- Alg: initialize $ \theta_0 \in \Theta $
  1. for t=0,1,2,...,(until convergence)
  2. E-step: $ Q( \theta, \theta_{t}) = E_{ \theta_t} ( \ln p_{ \theta}(x,z) \| X=x))$
  3. M-step: 
     * for MLE: $ \theta_{t+1} = \arg\max_{ \theta} Q( \theta, \theta_t) $.
     * for MAP: $ \theta_{t+1} = \arg\max_{ \theta} Q( \theta, \theta_t) + \ln p( \theta) $.
  
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
\begin{split}
Q( \theta, \theta_0) &= E_{\theta_0}( \ln p_{ \theta}(X,Z) \| X=x)
&= \theta^TE_{ \theta_0}(s(X,Z) \| X=x) - \ln C( \theta) + const
\end{split}
\\]

The derivative of $Q$ is,
\\[
\frac{ \partial}{ \partial \theta_i} Q( \theta, \theta_0) = E_{ \theta_0}(s_i(X,Z)|X=x) - E_{ \theta} s_i(X,Z) =0
\\]

Then, $\theta$ is our EM estimator result.

