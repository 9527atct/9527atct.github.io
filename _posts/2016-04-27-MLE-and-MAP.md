---
layout: post
title: MLE and MAP
date: 2016-04-25 15:24:05 +1000 
categories: MachineLearning
comments: true
---

----------

### conditions ###
- Given dataset $D=(x_1,...,x_n)$, $x_i \in R^d$
- Assume a joint distribution $p(D, \theta)$
- Goal: choose a good value of $\theta$ for $D$
- MAP: $ \theta_{MAP}= \arg \max_{ \theta} p( \theta | D)$
- MLE: $ \theta_{MLE}= \arg \max_{ \theta} p( D |     \theta)$

### samples ###
Suppose dataset $D=(x_1,...,x_n)$, $x_i \in R^d$, and $\theta \sim N( \mu,1)$. $x_1,...,x_n$ are conditional independent given $\theta$, and distribution is $N( \theta, \sigma^2).

Then, the MAP estimator is,
\\[
\theta_{map} = \arg\max_{ \theta} p( \theta |D) = \arg\max_{ \theta}( \ln p(D| \theta) + \ln p( \theta)) 
\\]

The derivative of log function is,
\\[
\frac{ \partial}{ \partial \theta}( \ln p(D| \theta)+ \ln p( \theta))= \frac{1}{ \sigma^2}( \sum_i^n x_i - n \theta) + ( \mu - \theta)
\\]

Then, we have,
\\[
\theta = \frac{ \sum_i^n x_i + \sigma^2 \mu}{n + \sigma^2}
\\]

So, we finally get the maximum a posterior of $\theta$,
\\[
\theta_{MAP}= \frac{n}{n+ \sigma^2} \bar{x} + \frac{ \sigma^2}{n+ \sigma^2} \mu
\\]

Obviously, the MAP estimator is a convex combination of $\bar{x}$ and $\mu$.