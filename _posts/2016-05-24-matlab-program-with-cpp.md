---
layout: post
title: matlab program with cpp
date: 2016-05-24 12:09:05 +1000 
categories: technology
comments: true
---

----------
### matlab program with cpp ###

- first create cpp source file "*.cpp", and include the header file "mex.h"; if you want to use the "mwSize" type, then also need to include "matrix.h".
    `#include "mex.h"
    #include "matrix.h"`

- secondly, define your function details. for example,
    void arrayProduct(double x, double *y, double *z, mwSize  n)
    {
    mwSize  i;
    for (i=0;i<n;i++){
    z[i] = x* y[i];
    }
    }
    
- third,