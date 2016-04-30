---
layout: post
title: gaussian distribution
date: 2016-04-30 21:37:05 +1000 
categories: MachineLearning
comments: true
---

----------

### multivariate normal ###
multivariate gaussian or multivariate normal (MVN) is the most widely used joint probability density function for continuous variables.

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

The following is to process the MLE for parameters $\mu$ and $\Sigma$. The likelihood function is,
\\[
\ln ( \theta)= \frac{-ND}{2} \ln 2 \pi + \frac{N}{2} \ln | \Lambda | - \frac{1}{2} \sum_{i=1}^N (x_i - \mu)^T \Lambda (x_i - \mu)
\\]
where $ \theta = ( \mu, \Sigma)$. 

Then, we let the derivative ,that is, $ \frac{ \partial}{ \partial \mu} \ln ( \theta)$ to be 0. Solving this equation, we could get the MLE vaule of $\mu$. Firstly, we calculate the $\frac{ \partial}{ \partial \mu} (x_i - \mu)^T \Sigma^{-1} (x_i - \mu)$,
\\[
\begin{split}
\frac{ \partial}{ \partial \mu} (x_i - \mu)^T \Sigma^{-1} (x_i - \mu) &= \frac{ \partial}{ \partial y_i} y_i^T \Sigma^{-1} y_i \frac{ \partial y_i }{ \partial \mu} \\\
&= -( \Sigma^{-1} + \Sigma^{-T}) y_i
end{split}
\\]
So, we have,
\\[
\frac{ \partial}{ \partial \mu} \ln ( \theta) = \frac{-1}{2} \sum_{i=1}^N -2 \Sigma^{-1} (x_i - \mu) = 0
\\]
Solving this equation, we finally get the MLE of the $\mu$ is,
\\[
\mu_{MLE} = \frac{1}{N} \sum_{i=1}^N x_i
\\]
    