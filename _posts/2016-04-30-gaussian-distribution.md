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
    