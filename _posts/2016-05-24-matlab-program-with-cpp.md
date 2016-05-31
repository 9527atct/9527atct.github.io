---
layout: postarticle
title: matlab work with cpp
date: 2016-05-24 12:09:05 +1000 
categories: technology
comments: true
---


### contents written by using c/cpp language ###



Both matlab and c are very popular program languages. In this article, we introduced a way to use these two technology together. 

- First create cpp source file "*.cpp", and include the header file "mex.h"; if you want to use the "mwSize" type, then also need to include "matrix.h".

```
#include "mex.h"
#include "matrix.h"
```

- Second, define your function details. for example,

```cpp
void arrayProduct(double x, double *y, double *z, mwSize  n)
{
mwSize  i;
for (i=0;i<n;i++){
    z[i] = x * y[i];
}
}
```
    
- Third, create the gateway function

```matlab
void mexFunction(int nlhs, mxArray *plhs[],int nrhs, const mxArray *prhs[])
{

double multiplier;
double *inMatrix;
mwSize ncols;
double *outMatrix;


if(nrhs != 2){
	mexErrMsgIdAndTxt("MyToolbox:arrayProduct:nrhs","Two inputs required.");
}
if(nlhs != 1) {
	mexErrMsgIdAndTxt("MyToolbox:arrayProduct:nlhs","One output required.");
}

if( !mxIsDouble(prhs[0]) || mxIsComplex(prhs[0]) || mxGetNumberOfElements(prhs[0]) != 1 ) {
	mexErrMsgIdAndTxt("MyToolbox:arrayProduct:notScalar","Input multiplier must be a scalar.");
}
if( !mxIsDouble(prhs[1]) || mxIsComplex(prhs[1])) {
	mexErrMsgIdAndTxt("MyToolbox:arrayProduct:notDouble","Input matrix must be type double.");
}
if(mxGetM(prhs[1]) != 1) {
	mexErrMsgIdAndTxt("MyToolbox:arrayProduct:notRowVector",  "Input must be a row vector.");
}



multiplier = mxGetScalar(prhs[0]);
inMatrix = mxGetPr(prhs[1]);
ncols = mxGetN(prhs[1]);

plhs[0] = mxCreateDoubleMatrix(1,ncols,mxREAL);
outMatrix = mxGetPr(plhs[0]);

arrayProduct(multiplier,inMatrix,outMatrix,ncols);
}
```


### compile ###


in the matlab enviroment, use command `mex -g xxx.c` to compile the c/cpp cource files. Here, the means of `-g` is to open the debug mode, when you want to debug the file.



### debug ###


In the windows operation system, we can use visual studio to debug the compiled files.

- firstly, open visuall c++, then click "tools"->"attach files" and choose the file that compiled with file suffix "xx.pdb".
- choose the breakpoint you want
- run files in matlab enviroment.
- done.