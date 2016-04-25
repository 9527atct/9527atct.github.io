---
layout: post
title: exponential family 
date: 2016-04-25 15:24:05 +1000 
categories: MachineLearning
---

----------

### Definition ###

A pdf $p(x| \theta)$, for $ \mathbf{x}=(x_1,...,x_m) \in \mathcal{X}^m$, and $ \theta \in \Theta  \subseteq R^d$, is said to be in the *exponential family* if it is of the form,
\\[
\begin{split}
p( \mathbf{x}| \theta) &= \frac{1}{Z( \theta)}h( \mathbf{x}) \exp [ \theta^T \phi( \mathbf{x})] \\\
&= h( \mathbf{x}) \exp [ \theta^T \phi( \mathbf{x}) - A( \theta)]
\end{split}
\\]
where,
\\[
\begin{split}
Z( \theta) &= \int_{ \mathcal{X}^m} h( \mathbf{x}) \exp [ \theta^T \phi( \mathbf{x})] dx \\\
A( \theta) &= \ln Z( \theta)
\end{split}
\\]

Here $\theta$ are called the *natural parameters*, $\phi( \mathbf{x}) \in R^d$ is called a vector of *sufficient statistics*, $Z( \theta)$ is called the *partition function*, $A( \theta)$ is called the *log partition function*, and $h( \mathbf{x})$ is the *scaling constant*, often 1. If $\phi( \mathbf{x})= \mathbf{x}$, we say it is a *natural exponential family*.

In general, exponential family is often written as,
\\[
p( \mathbf{x}| \theta) = h( \mathbf{x}) \exp [ \eta ( \theta)^T \phi ( \mathbf{x}) -A( \eta( \theta))]
\\]
where $ \eta$ is a function that maps the parameters $\theta$ to the natural parameters $ \eta = \eta ( \theta)$. if $dim( \theta) < dim( \eta ( \theta))$, it is called a curved exponential family, which means we have more sufficient statistics than parameters.

### example ###

The Bernoulli distribution can be written in exponential family form as follows:
\\[
Ber(x| \mu)= \mu^x(1- \mu)^{1-x}= \exp[ (x,1-x)( \ln \mu, \ln (1- \mu)^T]
\\]

where $\phi(x)=[x,1-x], \theta = [ \ln \mu, \ln (1- \mu)]$.

Another form,
\\[
Ber(x| \mu)= (1- \mu) \exp [x \ln \frac{ \mu}{1- \mu}]
\\]
where $\phi(x)=x, \theta = \ln \frac{ \mu}{1- \mu}$ 