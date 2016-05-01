---
layout: post
title: gaussian distribution
date: 2016-04-30 21:37:05 +1000 
categories: MachineLearning
comments: true
---

----------

### multivariate normal ###
multivariate gaussian or multivariate normal (MVN) is the most widely used joint probability density function for continuous variables. Multivariate Gaussian is the distribution with maximum entropy subject to having a specified mean and covariance. 

- pdf 
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

Suppose $x=(x_1,x_2)$ is jointly Gaussian,
\\[
\mu = \begin{pmatrix} \mu_1 \\\ \mu_2 \end{pmatrix} , \Sigma = \begin{pmatrix} \Sigma_{11} & \Sigma_{12} \\\ \Sigma_{21} & \Sigma_{22} \end{pmatrix}, \Lambda = \Sigma^{-1}
\\]

Then, we have the marginal distributions:
\\[
\begin{split}
p(x_1) &= N( \mu_1, \Sigma_{11} \\\
p(x_2) &= N( \mu_2, \Sigma_{22}
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

Suppose we have two variables, $x$ and $y$. Let $x \in R^{D_x}$ be a hidden variable, and $y \in R^{D_y}$ be a noisy observation of $x$. Let us assume we have the following prior and likelihood.
\\[
\begin{split}
p(x) = N(x| \mu_x, \Sigma_x) \\\
p(y|x) = N(y | Ax+b, \Sigma_y)
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

- posterior of $\mu$

