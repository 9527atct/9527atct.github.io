---
layout: post
title: multiple kernel learing
date: 2016-04-23 15:58:05 +1000 
categories: MachineLearning
---

### Reproducing kernel Hibert Sapce (RKHS)

RKHS is a Hibert Space of functions in which point evaluation is a continuous linear functional. Roughly speaking, this means that if two function $f$ and $g$ in the RKHS are close in norm, i.e., $||f-g||$ is small, then $f$ and $g$ are also pointwise close, i.e., $|f(x)-g(x)|$ is small for all $x$. The reverse need not be true.

### Multiple kernel learning


Multiple kernel learning refers to a set of machine learning methods that use a predefined set of kernels and learn an optimal linear or non-linear combination of kernels as part of the algorithm. Reasons to use multiple kernel learning include the ability to select for an optimal kernel and parameters from a larger set of kernels, reducing bias due to kernel selection while allowing for more automated machine learning methods, and combining data from different sources (e.g. sound and images from a video) that have different notions of similarity and thus require different kernels. Instead of creating a new kernel, multiple kernel algorithms can be used to combine kernels already established for each individual data source.

+ Algorithms

The basic idea behind multiple kernel learning algorithms is to add an *extra parameter* to the minimization problem of the learning algorithm.

As an example, consider the case of supervised learning of a linear combination of a set of $n$ kernels $K$. We introduce a new kernel 
\\[
K'= \sum_{i=1}^n \beta_i K_i 
\\] 
where $ \beta $ is a vector of coefficients for each kernel. because the kernels are additive (due to properties of reproducing kernel Hilbert spaces), this new function is still a kernel. For a set of data $X$ with labels $Y$, the minimization problem can then be written as,
\\[
\min_{ \beta,c} E(Y,K'c) + R(K,c)
\\]
where $E$ is an error function and $R$ is a regularization term. $E$ is typically the square loss function or the hinge loss function, and $R$ is usually an $l_n$ norm or some combination of the norms. This optimization problem can then be solved by standard optimization methods. Adaptations of existing techniques such as the sequential minimal optimization have also been developed for multiple kernel SVM-based methods.
