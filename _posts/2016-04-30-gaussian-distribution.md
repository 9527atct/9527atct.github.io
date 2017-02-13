---
layout: post
title: gaussian distribution
date: 2016-04-30 21:09:05 +1000 
categories: MachineLearning
comments: true
---

----------

### Multivariate Normal Distribution###
- [**brief introduce**] multivariate gaussian or multivariate normal (MVN) is the most widely used joint probability density function for continuous variables. Multivariate Gaussian is the distribution with maximum entropy subject to having a specified mean and covariance. 

- [**pdf**]
\\[
N(x| \mu, \Sigma)= \frac{1}{(2 \pi)^{ \frac{D}{2}} | \Sigma|^{ \frac{1}{2}}} \exp [ - \frac{1}{2} (x- \mu)^T \Sigma^{-1}(x- \mu) ]
\\]
where,
\\[
\begin{split}
(x- \mu)^T \Sigma^{-1}(x- \mu) &= (x- \mu)^T( \sum_{i=1}^D \frac{1}{ \lambda_i} u_i u_i^T )(x - \mu) \\\
&= \sum_{i=1}^D \frac{1}{ \lambda_i } (x- \mu)^T u_i u_i^T (x- \mu) \\\
&= \sum_{i=1}^D \frac{y_i^2}{ \lambda_i }
\end{split}
\\]
where, $y_i = u_i^T(x- \mu)$.

### Matrix Normal Distribution ###
- [**brief introduce**] In statistics, the matrix normal distribution is a probability distribution that is a generalization of the multivariate normal distribution to matrix-valued random variable. Also the matrix normal distribution is special case of the multivariate normal distribution.
- [**definition**] The probability density function for the random matrix $X\_{np} $ that follows the matrix normal distribution $MN\_{np}(M,U,V)$ has the form,
\\[
p(X|M,U,V)=\\frac{ exp(-\\frac{1}{2} tr(V^{-1}(X-M)^T U^{-1}(X-M) )) }{ (2\\pi)^{np/2}|V|^{n/2}|U|^{p/2}  }
\\]
Here, $V\_{p\\times p}$ can be treated as **covariance matrix**, and $U\_{n\\times n}$ as the **kernel matrix** of data.

    **proof**: 
\\[
\\begin{split}
&-\\frac{1}{2} tr(V^{-1}(X-M)^T U^{-1}(X-M)) \\\
&=-\\frac{1}{2} vec(X-M)^T vec(U^{-1}(X-M)V^{-1})\\\
&=-\\frac{1}{2} vec(X-M)^T (V^{-1} \\otimes U^{-1}) vec( X-M) \\\
&=-\\frac{1}{2} vec(X-M)^T (V \\otimes U)^{-1}  vec( X-M) \\\
&=-\\frac{1}{2} vec(X-M)^T (\\Sigma)^{-1}  vec( X-M) \\\
\\end{split}
\\]
and for determinant,
\\[
|V|^{n/2}|U|^{p/2}=|V\\otimes U|=|\\Sigma|
\\]
so, we can conclude that,
\\[
vec(X) \\sim N\_{np}(vec(M),V\\otimes U)
\\]
notice that, both $V$ and $U$ are symmetric matrices.



### MLE for $\mu, \Sigma$ ###
> \\[ \mu_{MLE} = \frac{1}{N} \sum_{i=1}^N x_i = \bar{x} \\]
> \\[ \Sigma_{MLE} = \frac{1}{N} \sum_{i=1}^N (x_i - \bar{x})(x_i - \bar{x})^T = \frac{1}{N}( \sum_{i=1}^N x_i x_i^T) - \bar{x} \bar{x}^T \\]

- $\mu_{MLE}$

The goal of the following steps is to process the MLE for parameters $\mu$ and $\Sigma$. We know that The likelihood function of joint distribution is,
\\[
\ln ( \theta)= \frac{-ND}{2} \ln 2 \pi + \frac{N}{2} \ln | \Lambda | - \frac{1}{2} \sum_{i=1}^N (x_i - \mu)^T \Lambda (x_i - \mu)
\\]
where $ \theta = ( \mu, \Sigma)$. 

Then, we let the derivative ,that is, $ \frac{ \partial}{ \partial \mu} \ln ( \theta)$ to be 0. Solving this equation, we could get the MLE vaule of $\mu$. Firstly, we calculate the $\frac{ \partial}{ \partial \mu} (x_i - \mu)^T \Sigma^{-1} (x_i - \mu)$, and apply the rule $ \frac{ \partial a^TAa}{ \partial a}=(A+A^T)a $,
\\[
\begin{split}
\frac{ \partial}{ \partial \mu} (x_i - \mu)^T \Sigma^{-1} (x_i - \mu) &= \frac{ \partial}{ \partial y_i} y_i^T \Sigma^{-1} y_i \frac{ \partial y_i }{ \partial \mu} \\\
&= -( \Sigma^{-1} + \Sigma^{-T}) y_i
\end{split}
\\]
 we have,
\\[
\frac{ \partial}{ \partial \mu} \ln ( \theta) = \frac{-1}{2} \sum_{i=1}^N -2 \Sigma^{-1} (x_i - \mu) = 0
\\]
Solving this equation, we finally get the MLE for the parameter $\mu$ is,
\\[
\mu_{MLE} = \frac{1}{N} \sum_{i=1}^N x_i
\\]
    
- $\Sigma_{MLE}$

\\[
\begin{split}
\ln l( \theta) &= \frac{-ND}{2} \ln 2 \pi + \frac{N}{2} \ln | \Lambda | - \frac{1}{2} \sum_{i=1}^N Tr[ (x_i - \mu)^T \Lambda (x_i - \mu)] \\\
&= \frac{-ND}{2} \ln 2 \pi + \frac{N}{2} \ln | \Lambda | - \frac{1}{2} \sum_{i=1}^N Tr[ (x_i - \mu)(x_i - \mu)^T \Lambda ] \\\
&= \frac{-ND}{2} \ln 2 \pi + \frac{N}{2} \ln | \Lambda | - \frac{1}{2} Tr[ S_{\mu} \Lambda ]
\end{split}
\\]
where, $S_{\mu}= \sum_{i=1}^{N} (x_i - \mu)(x_i - \mu)^T$. Using the rule $\frac{\partial \ln (A)}{ \partial A}=A^{-T}$ and $ \frac{ \partial Tr(BA)}{ \partial A}=B^T$ the derivate of the function of $\Lambda$ is
\\[
\frac{ \partial \ln l( \theta)}{ \partial \Lambda} = \frac{N}{2} \Lambda^{-T} - \frac{1}{2} S_{\mu}^T = 0
\\]
Finally, we get the MLE of $\Sigma$, that is,
\\[
\Sigma_{MLE} = \frac{1}{N} S_{\mu}^T
\\]

### Jointly Gaussian ###
------------------------

Suppose $x=(x_1,x_2)$ is jointly Gaussian,
\\[
\mu = \begin{pmatrix} \mu_1 \\\ \mu_2 \end{pmatrix} , \Sigma = \begin{pmatrix} \Sigma_{11} & \Sigma_{12} \\\ \Sigma_{21} & \Sigma_{22} \end{pmatrix}, \Lambda = \Sigma^{-1}
\\]

Then, we have the marginal distributions:
\\[
\begin{split}
p(x_1) &= N( \mu_1, \Sigma_{11}) \\\
p(x_2) &= N( \mu_2, \Sigma_{22})
\end{split}
\\]

and the posterior conditional is given by
\\[
\begin{split}
p(x_1 | x_2) &= N(x_1 | \mu_{1|2}, \Sigma_{1|2}) \\\
\mu_{1|2}&= \mu_1 + \Sigma_{12} \Sigma_{22}^{-1}(x_2 - \mu_2) \\\
&= \mu_1 - \Lambda_{11}^{-1} \Lambda_{12}(x_2 - \mu_2) \\\
&= \Sigma_{1|2}( \Lambda_{11} \mu_1 - \Lambda_{12}(x_2 - \mu_2)) \\\
\Sigma_{1|2} &= \Sigma_{11} - \Sigma_{12} \Sigma_{22}^{-1} \Sigma_{21} = \Lambda_{11}^{-1}
\end{split}
\\]

### Linear Gaussian ###
-----------------------

Suppose we have two variables, $x$ and $y$. Let $x \in R^{D_x}$ be a hidden variable, and $y \in R^{D_y}$ be a noisy observation of $x$. Let us assume we have the following prior and likelihood.
\\[
\begin{split}
p(x) &= N(x| \mu_x, \Sigma_x) \\\
p(y|x) &= N(y | Ax+b, \Sigma_y)
\end{split}
\\]
where $A$ is a matrix of size $D_y \times D_x$. This is an example of a linear Gaussian system.

Then, the posterior $p(x|y)$ is given by the following:
\\[
\begin{split}
p(x|y) &= N(x | \mu_{x|y}, \Sigma_{x|y}) \\\
\Sigma_{x|y} &= \Sigma_x^{-1} + A^T \Sigma_y^{-1} A \\\
\mu_{x|y} &= \Sigma_{x|y}[A^T \Sigma_y^{-1}(y-b)+ \Sigma_x^{-1} \mu_x]
\end{split}
\\]
In addition, the normalization constant $p(y)$ is given by 
\\[
p(y) = N(y| A \mu_x +b , \Sigma_y + A \Sigma_x A^T)
\\]

### Wishart distribution ###
----------------------------

The Wishart distribution is the generalization of Gamma distribution to positive definite matrices.

- pdf

\\[
Wi( \Lambda | S, \nu) = \frac{1}{Z_{Wi}} | \Lambda |^{( \nu - D -1 / 2)} \exp (- \frac{1}{2} tr ( \Lambda S^{-1}))
\\]
Here $\nu$ is called the "degrees of freedom" and $S$ is the "scale matrix".
\\[
Z_{Wi} = 2^{ \nu D /2} \Gamma_{D}( \nu /2) | S |^{ \nu /2}
\\]
where $ \Gamma_{D}(a)$ is the multivariate gamma function:
\\[
\Gamma_{D}(x)= \pi^{D(D-1)/4} \prod_{i=1}^D \Gamma(x+(1-i)/2)
\\]
Hence $\Gamma_1(a) = \Gamma(a)$ and
\\[
\Gamma_{D}( \nu_0 /2)= \prod_{i=1}^D \Gamma( \frac{ \nu_0 + 1 - i}{2})
\\]
The normalization constant only exists (and hence the pdf is only well defined) if $ \nu > D-1$.

- connection between the Wishart and the Gaussian

Let $x_i \sim \mathcal{N}(0, \Sigma)$. Then the scatter matrix $S= \sum_{i=1}^N x_ix_i^T$ has a Wishart distribution: $S \sim Wi( \Sigma,1)$. Hence $E[S]= N \Sigma$.

- mean,mode

mean:
\\[
mean = \nu S
\\]
mode:
\\[
mode = (\nu -D -1)S
\\]

- if $D=1$, the Wishart reduces to the Gamma distribution:
\\[
Wi( \lambda | s^{-1}, \nu) = Ga( \lambda | \nu /2 ,s/2)
\\]

### Inverse Wishart distribution ###
------------------------------------

If $\lambda \sim Ga(a,b)$, then $\frac{1}{\lambda} \sim IG(a,b)$. similarly, if $\Sigma^{-1} \sim Wi(S, \nu)$ then $\Sigma \sim IW(S^{-1}, \nu + D + 1)$, where IW is the inverse Wishart, the multidimensional generalization of the inverse Gamma.

- pdf
\\[
IW( \Sigma | S, \nu) = \frac{1}{Z_{IW}} | \Sigma |^{-( \nu + D + 1) /2} \exp[ - \frac{1}{2} tr( S^{-1} \Sigma^{-1}]
\\]
where 
\\[
Z_{IW} = |S|^{- \nu /2} 2^{ \nu d/2} \Gamma_{D}( \nu /2)
\\]

- mean
\\[
mean= \frac{S^{-1}}{ \nu -D -1}
\\]

- mode
\\[
\frac{S^{-1}}{ \nu + D + 1}
\\]

- if $D=1$, this reduces to the inverse Gamma:
\\[
IW( \sigma^2 | S^{-1}, \nu)= IG( \sigma^2 | \nu /2 ,S/2)
\\]

### MAP estimation ###
----------------------

- **posterior of $\mu$**

The likelihood has the form $ p( \mathcal{D}| \mu)= \mathcal{N}( \bar{x}| \mu, \frac{1}{N} \Sigma)$. According to linear Gaussian theory, we can treat the $\mathcal{D}$ as the observation of the hidden variable $\mu$. Now, we give a prior to $\mu$, that is, $p( \mu) = \mathcal{N}( \mu | m_o, v_0)$. Then, we can derive a Gaussian posterior for $\mu$ ,
\\[
\begin{split}
p( \mu | \mathcal{D}, \Sigma) &= \mathcal{N}( \mu | m_N,V_N) \\\
m_N &= V_N( \Sigma^{-1}(N \bar{x}) + V_0^{-1}m_0) \\\
V_N^{-1} &= V_0^{-1} + N \Sigma^{-1}
\end{split}
\\]

- **posterior distribution of $\Sigma$**  
The likelihood,
\\[
p( \mathcal{D}| \mu, \Sigma) \propto | \Sigma |^{-N/2} \exp [ \frac{-1}{2} tr(S_{ \mu} \Sigma^{-1} ]
\\]
The corresponding conjugate prior is known as the inverse Wishart distribution,
\\[
IW( \Sigma | S_0^{-1}, \nu_0) \propto | \Sigma |^{-( \nu_0 + D + 1) /2} \exp [ \frac{-1}{2}tr(S_0 \Sigma^{-1}) ]
\\]
Here $ \nu_0 > D-1$ is the degrees of freedom, $S_0$ is a symmetric pd matrix. We see that $S_0^{-1}$ plays the role of the prior scatter matrix, and $  \nu_0 + D + 1$ controls the strength of the prior, and hence plays a role analogous to the sample size $N$.
Multiplying the likelihood and prior we find that the posterior is also inverse Wishart:
\\[
\begin{split}
p( \Sigma| \mathcal{D}, \mu) & \propto | \Sigma |^{N/2}  \exp [ \frac{-1}{2} tr(S_{ \mu} \Sigma^{-1}) ]  | \Sigma |^{-( \nu_0 + D + 1) /2} \exp [ \frac{-1}{2}tr(S_0 \Sigma^{-1}) ] \\\
&= | \Sigma|^{ \frac{N+( \nu_0 + D + 1}{2}} \exp [- \frac{1}{2} tr[ \Sigma^{-1} (S_{ \mu} + S_0)]] \\\
&= IW( \Sigma | S_N, \nu_N)
\end{split}
\\]
Here, $\nu_N = \nu_0 + N$, $S_N^{-1} = S_0 + S_{ \mu}$. <br/>

MAP estimation for $ \Sigma$

\\[
\hat{ \Sigma} = \frac{ S_N }{ \nu_N + D + 1} = \frac{S_0 + S_{ \mu}}{N_0 + N}
\\]

if  we use an improper uniform prior, corresponding to $N_0 =0 $ and $S_0 = 0$, we recover the MLE.
Let $\mu = \bar{x}$, so, $S_{ \mu} = S_{ \hat{x}}$. Then the posterior can be rewritten as

\\[
\begin{split}
\hat{ \Sigma} &= \frac{S_0 + S_{ \bar{x}}}{N_0 + N} \\\
&= \frac{N_0 S_0}{(N_0 + N)N_0  }+ \frac{NS}{(N_0+N)N} \\\
&= \lambda \Sigma_0 + (1- \lambda) \hat{ \Sigma}_{mle}
\end{split}
\\]

where $\lambda = \frac{N_0}{N_0 + N}$.


  
- **Posterior distribution of $\mu$ and $\Sigma$**
	1. **likelihood**:
\\[
\begin{split}
p( \mathcal{D} | \mu, \Sigma)=(2 \pi)^{-ND/2} | \Sigma |^{-N/2} \exp \left( - \frac{1}{2} \sum_{i=1}^N (x_i - \mu)^T \Sigma^{-1} (x_i - \mu) \right)
\end{split}
\\]
We know that,
\\[
\sum_{i=1}^N (x_i - \mu)^T \Sigma^{-1} (x_i - \mu) = tr( \Sigma^{-1} S_{ \bar{x}}) + N( \bar{x} - \mu)^T \Sigma^{-1} ( \bar{x} - \mu)
\\]
Hence we can rewritte the likelihood as follows:
\\[
p( \mathcal{D} | \mu, \Sigma)=(2 \pi)^{-ND/2} | \Sigma |^{-N/2}\exp \left( - \frac{N}{2} \sum_{i=1}^N (x_i - \bar{x})^T \Sigma^{-1} (x_i - \bar{x}) \right) \exp \left( - \frac{N}{2} tr( \Sigma^{-1} S_{ \bar{x}}) \right)
\\]

	2. **Prior: Normal-inverse-wishart, NIW**
\\[
p( \mu ,\Sigma) = p( \Sigma) p( \mu | \Sigma)
\\]
\\[
NIW( \mu , \Sigma | m_0, \kappa_0, \nu_0, S_0) \sim N( \mu | m_0, \frac{1}{ \kappa_0} \Sigma) \times IW( \Sigma |S_0, \nu_0)
\\]
where, $m_0$ is our prior mean for $\mu$, and $\kappa_0$ is how strongly we believe this prior; and $S_0$ is our prior mean for $\Sigma$, and $\nu_0$ is how strongly we believe this prior.
	
	3. **Posterior**
\\[
\begin{split}
p( \mu, \Sigma | \mathcal{D}) &= NIW( \mu, \Sigma | m_N, \kappa_N, \nu_N, S_N) \\\
m_N &= \frac{ \kappa_0 m_0 + N \bar{x}}{ \kappa_{N}} = \frac{ \kappa_0}{ \kappa_0 + N}m_0 + \frac{N}{ \kappa_0 + N} \bar{x} \\\
\kappa_N &= \kappa_0 + N\\\
\nu_N &= \nu_0 + N \\\
S_N &= S_0 + S_{ \bar{x}} + \frac{ \kappa_0 N}{ \kappa_0 + N}( \bar{x} - m_0)( \bar{x} - m_0)^T \\\
&= S_0 + S + \kappa_0m_0m_0^T - \kappa_Nm_Nm_N^T
\end{split}
\\]
where $S= \sum_{i=1}^N x_ix_i^T$. Result analysis: the posterior mean is a convex combination of the prior mean and the MLE, with "strength" $\kappa_0 + N$; and the posterior scatter matrix $S_N$ is the prior scatter matrix $S_0$ plus the empirical scatter matrix $S_{ \bar{x}}$ plus an extra term due to the uncertainty in the mean.

   4. **MAP for $ \mu, \Sigma$**
        - **4.1 $ \hat{ \Sigma} $**
\\[
p( \Sigma | \mathcal{D}) = \int p( \mu, \Sigma | \mathcal{D}) d \mu = IW( \Sigma | S_N, \nu_N)
\\]
Then, $ \hat{ \Sigma}_{map} = \frac{S_N}{ \nu_N + D + 1}$ . 
        - **4.2 $ \hat{ \mu}$**
\\[
p( \mu | \mathcal{D} = \int p( \mu, \Sigma | \mathcal{D}) d \Sigma = \mathcal{T}( \mu | m_N, \frac{S_N}{ \kappa_N ( \nu_N -D + 1)} S_N, \nu_N -D +1)
\\]
Then, $ \hat{ \mu}_{map} = m_N$.
        - **4.3 Posterior predictive**s
\\[
\begin{split}
p(x| \mathcal{D})= p(x| \mu, \Sigma)p( \mu, \Sigma| \mathcal{D}) &= \iint \mathcal{N}(x| \mu, \Sigma) NIW( \mu , \Sigma | m_N, \kappa_N, \nu_N, S_N) d \mu d \Sigma \\\
&= \mathcal{T}(x|m_N, \frac{ \kappa_N + 1}{ \kappa_N( \nu_N -D +1)}S_N, \nu_N -D + 1)
\end{split}
\\]
   
   
   
   