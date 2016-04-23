---
layout: post
title: Variational Inference
date: 2016-04-22 12:58:05 +1000 
categories: MachineLearning
---
***
### Main Idea ###
The main idea behind variational methods is to pick a family of distributions over the latent variables with its own _variational parameter_
\\[
q(z_{1:m}| \alpha)
\\]
Then find the setting of the parameters that makes $q$ close to the posterior of interest.

Use $q$ with the fitted parameters as a proxy for the posterior, e.g., to form predictions about future data or to investigate the posterior distribution of the hidden variables.

### Using KL divergence to measure the closeness of two distributions ###
- The KL divergence for variational inference is
\\[
KL(q || p)=\int q(Z) \ln \{ \frac{q(Z)}{p(Z|x)} \}=E_q [ \ln \frac{q(Z)}{p(Z|x)}]
\\]