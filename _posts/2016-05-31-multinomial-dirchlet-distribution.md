---
layout: postarticle
title: multinomial dirichlet distribution
date: 2016-05-24 12:09:05 +1000 
categories: Math
comments: true
---

### multinomial  ###
设某随机实验有$A_1,...,A_k$个结果，分别将它们出现的次数标记为随机变量$X_1,...,X_k$.它们的概率分布是$p_1,...,p_k$,那么在$n$次实验中，$A_1$出现$n_1$次，$A_k$出现$n_k$次的事件概率为
\\[
p(X_1=n_1,X_2=n_2,...,X_k=n_k)= \frac{ \Gamma( \sum_i n_i)}{ \Gamma(n_1)... \Gamma(n_k)} \prod_{i=1}^k p_i^{n_i}
\\]

### multinomial,binomial ,categorical ,bernolli###

假设有$k$个桶，$n$个球，每个桶中的球的个数为$x_i$,概率为$p_i$.那么掉入每个桶中的球的个数服从以下分布，
<table class="table">
<tr>
<td>分布</td><td>球的个数</td><td>桶数</td><td>掉入桶的概率</td>
</tr>
<tr>
<td>multinomial</td><td>$n$</td><td>$k$</td><td>$p_1,p_2,...,p_k$</td>
</tr>
<tr>
<td>binomial</td><td>$n$</td><td>2</td><td>$p$(另一个为$1-p$)</td>
</tr>
<tr>
<td>categorical</td><td>1</td><td>$k$</td><td>$p_1,p_2,...,p_k$</td>
</tr>
<tr>
<td>bernolli</td><td>1</td><td>2</td><td>$p$(另一个为$1-p$)</td>
</tr>
</table>