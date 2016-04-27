---
layout: post
title: exponential family 
date: 2016-04-25 15:24:05 +1000 
categories: MachineLearning
comments: true
---

----------

### Definition ###

A pdf $p(x| \theta)$, for $ \mathbf{x}=(x_1,...,x_m) \in \mathcal{X}^m$, and $ \theta \in \Theta  \subseteq R^d$, is said to be in the *exponential family* if it is of the form,
\\[
\begin{split}
p( \mathbf{x}| \theta) &= \frac{1}{Z( \theta)}h( \mathbf{x}) \exp [ \theta^T s( \mathbf{x})] \\\
&= h( \mathbf{x}) \exp [ \theta^T s( \mathbf{x}) - A( \theta)]
\end{split}
\\]
where,
\\[
\begin{split}
Z( \theta) &= \int_{ \mathcal{X}^m} h( \mathbf{x}) \exp [ \theta^T s( \mathbf{x})] dx \\\
A( \theta) &= \ln Z( \theta)
\end{split}
\\]

Here $\theta$ are called the *natural parameters*, $s( \mathbf{x}) \in R^d$ is called a vector of *sufficient statistics*, $Z( \theta)$ is called the *partition function*, $A( \theta)$ is called the *log partition function*, and $h( \mathbf{x})$ is the *scaling constant*, often 1. If $s( \mathbf{x})= \mathbf{x}$, we say it is a *natural exponential family*.

In general, exponential family is often written as,
\\[
p( \mathbf{x}| \theta) = h( \mathbf{x}) \exp [ \eta ( \theta)^T s ( \mathbf{x}) -A( \eta( \theta))]
\\]
where $ \eta$ is a function that maps the parameters $\theta$ to the natural parameters $ \eta = \eta ( \theta)$. if $dim( \theta) < dim( \eta ( \theta))$, it is called a curved exponential family, which means we have more sufficient statistics than parameters.

### example ###

The Bernoulli distribution can be written in exponential family form as follows:
\\[
Ber(x| \mu)= \mu^x(1- \mu)^{1-x}= \exp[ (x,1-x)( \ln \mu, \ln (1- \mu)^T]
\\]

where $s(x)=[x,1-x], \theta = [ \ln \mu, \ln (1- \mu)]$.

Another form,
\\[
Ber(x| \mu)= (1- \mu) \exp [x \ln \frac{ \mu}{1- \mu}]
\\]
where $s(x)=x, \theta = \ln \frac{ \mu}{1- \mu}$ 

### MLE for an exponential family ###
Given $D = (x_1,...,x_n)$, $x_i \in R^d , \theta \in R^k , x_1,...,x_n \sim p(x|  \theta) $, Then, MLE is,
\\[
\theta_{MLE} = \arg \max _{ \theta } p(D| \theta) 
\\]

That is,
\\[
\begin{split}
p(D| \theta)&= \prod_{i=1}^n p(x_i | \theta) \\\
&= \prod_{i=1}^n e^{ \theta^T s(x_i)}h(x_i) \frac{1}{Z( \theta)} \\\
&= z( \theta)^{-n} e^{ \theta^T \sum_{i=1}^n s(x_i)} \prod_{i=1}^n h(x_i) \\\
&= z( \theta)^{-n} e^{ \theta^T s(D) } \prod_{i=1}^n h(x_i)
\end{split}
\\]

log function of the MLE
\\[
\ln p(D| \theta)= -n \ln Z( \theta) + \theta^T S(D) + \sum_{i=1}^n \ln h(x_i)
\\]
where $S=(s_1,...,s_k}$,  $\theta^T S(D)= \sum_{j=1}^k \theta_j s_j(D)$, $s_j(D)= \sum_{i=1}^n s_j(x_i)$.


The function derivative is,
\\[
\frac{ \partial}{ \partial \theta_j} \ln p(D| \theta) = -n \frac{ \partial}{ \partial \theta_j} \ln Z( \theta) +s_j(D)
\\]  

and, $\frac{ \partial}{ \partial \theta_j} \ln Z( \theta)$,
\\[
\begin{split}
\frac{ \partial}{ \partial \theta_j} \ln Z( \theta) &= \frac{1}{Z( \theta)} \frac{ \partial}{ \partial \theta_j} Z( \theta) \\\
&= \frac{1}{Z( \theta)} \int s_j(x)e^{ \theta^T s(x)} h(x) dx \\\
&= \int s_j(x) p_{ \theta}(x) dx \\\
&= E_{ \theta}[ s_j(X) ]
\end{split}
\\]
