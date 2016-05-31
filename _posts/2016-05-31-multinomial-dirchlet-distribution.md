---
layout: postarticle
title: multinomial dirichlet distribution
date: 2016-05-24 12:09:05 +1000 
categories: technology
comments: true
---

### multinomial  ###
设某随机实验有$A_1,...,A_k$个结果，分别将它们出现的次数标记为随机变量$X_1,...,X_k$.它们的概率分布是$p_1,...,p_k$,那么在$n$次实验中，$A_1$出现$n_1$次，$A_k$出现$n_k$次的事件概率为
\\[
p(X_1=n_1,X_2=n_2,...,X_k=n_k)= \frac{ \Gamma( \sum_i n_i)}{ \Gamma(n_1)... \Gamma(n_k)} \prod_{i=1}^k p_i^{n_i}
\\]