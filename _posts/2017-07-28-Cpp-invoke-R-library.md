---
layout: postarticle
title: Cpp invoke R library
date: 2017-07-28 10:40:05 +1000
categories: technology
comments: true
---
  
  
### 1. C++调用R  
  
有时为了调试C++程序，必须在C++环境中模拟R的一些功能，如传输数据到算法，返回结果到R，以及调用R中已有的一些功能函数。这时需要使用到的第三方类库主要有RInside, Rcpp以及R提供的头文件。

  
### 1.1 类库准备  

### 1.1.1 R头文件  
若需要调用R所提供的功能以及与R交互，那么需要找到R所提供的接口文件“R.h, Rmath.h”，以及库文件"libR.so"。
```
$sudo find / -name "Rmath.h" | grep "usr/"
/usr/share/R/include/Rmath.h

$sudo find / -name "*R.so" | grep "usr/"
/usr/lib/R/lib/libR.so
```

  
### 1.1.2 RInside安装  
RInside的安装比较容易。这是一个R的C++扩展包，只需要在R的环境中使用一般的包安装流程就可以实现。现在给出ubuntu环境下的安装步骤，不加说明，默认操作系统为ubuntu。
```
$sudo R
>install.packages("RInside")
```
要想使用这个类库，得首先找到类库接口所提供的头文件如："RInside.h"。在操作系统中，打开shell，使用以下命令搜索文件所在位置。
```
$sudo find / -name "*RInside.h" | grep "usr/"
/usr/local/lib/R/site-library/RInside/include/RInside.h
```

以及库所在的路径，这些对后面C++编译环境特别重要。
```
$sudo find / -name "*RInside.so" | grep "usr/"
/usr/local/lib/R/site-library/RInside/lib/libRInside.so
/usr/local/lib/R/site-library/RInside/libs/RInside.so
```
  
### 1.1.3 Rcpp安装  
Rcpp的安装与RInside过程类似，在R环境中使用一般的包安装策略就可以实现。
```
$sudo R
>install.packages("Rcpp")

$sudo find / -name "Rcpp.h" | grep "usr/"
/usr/local/lib/R/site-library/Rcpp/include/Rcpp.h

$sudo find / -name "*Rcpp.so" | grep "usr/"
/usr/local/lib/R/site-library/Rcpp/libs/Rcpp.so

$cd /usr/local/lib/R/site-library/Rcpp/libs
$sudo cp Rcpp.so libRcpp.so
```
C++默认编译命令“-lRcpp"所寻找的链接库为”libRcpp.so"，所以需要对Rcpp.so 重命名。
  
### 1.2 环境搭建  
这里主要是在ubntu环境下，用Codeblocks来搭建实验环境。首先新建一个空白工程。然后在[project]->[build options]选择[Search directories]->[Compiler]->[Add]，并添加以下搜索路径：
```
/usr/share/R/include
/usr/local/lib/R/site-library/RInside/include
/usr/local/lib/R/site-library/Rcpp/include
```
以及[Linker]选项卡，添加以下类库搜索路径：
```
/usr/local/lib/R/site-library/RInside/lib/
/usr/local/lib/R/site-library/Rcpp/libs
```

[Linker settings]选项卡中[Link libraries]添加以下编译命令：
```
R
RInside
Rcpp
```

至此，所需要的环境已基本建立好了。下面以clusterpathRcpp类库为例来具体分析R与C++之间的交互。 clusterpathRcpp可以在http://R-Forge.R-project.org这里下载。
  
### 1.3 clusterpathRcpp源代码分析  
在clusterpathRcpp的类库目录src下把所有的C++文件加入到codeblocks当前工程，同时新建interface.cpp的头文件“interface.h"。因为cpp文件多次include的情况下，每次编译会出现重复定义的情况。
```C
#ifndef INTERFACE_H_INCLUDED
#define INTERFACE_H_INCLUDED

#include <Rcpp.h>
#include "l1.h"
#include "l2.h"

SEXP tree2list(Cluster *c);

RcppExport SEXP join_clusters_convert(SEXP xR);

SEXP res2list(Results *r);

RcppExport SEXP calcW_convert(SEXP x_R,SEXP gamma);

RcppExport SEXP join_clusters2_restart_convert
(SEXP x_R,SEXP w_R,
SEXP lambda,SEXP join_thresh,SEXP opt_thresh,SEXP lambda_factor,SEXP smooth,
SEXP maxit,SEXP linesearch_freq,SEXP linesearch_points,SEXP check_splits,
SEXP target_cluster,
SEXP verbose
);

#endif // INTERFACE_H_INCLUDED
```

接下来，就是最重要的测试部分，新建一个带main函数的cpp文件，

```C
#include <iostream>
#include "interface.h"

#include <Rcpp.h>
#include <RInside.h>

using namespace std;

int main(int argc, char* argv[])
{
//example 1: cpp code directly invoke R
RInside R(argc,argv);
R["txt"]="Hello world in R!\n"; //将字符串赋于R环境中的txt对象。
R.parseEvalQ("cat(txt)");       //R环境分析与执行“cat(txt)"命令
cout << "Hello world in C++!" << endl; //C++环境输出

//使用Rcpp类库提供的方法，将C++对象赋于R环境中的”vec1"对象。
R["vec1"]= Rcpp::NumericVector::create(1,2.3,4,5.7,8.0,9);
R.parseEvalQ("print(vec1)");    //R环境分析与执行,并将结果打印到console

std::string txt =
"z<-rnorm(n = 10,mean = 0,sd = 1)";

//把字符串中的内容发送到R环境，并将计算结果赋于C++对象 v
Rcpp::NumericVector v = R.parseEval(txt); 

for (int i=0; i< v.size(); i++) {           //显示c++对象v的内容
std::cout << "In C++ element " << i << " is " << v[i] << std::endl;
}


//example 2: 调试clusterpathRcpp类库, 
//具体的业务逻辑见clusterpathRcpp类库的R子目录中的函数定义
std::string txt2 =
"suppressMessages(library(clusterpathRcpp))";
R.parseEvalQ(txt2);
Rcpp::NumericVector dt((SEXP) R.parseEval("dt<-iris[,1]"));
R["res1"]=join_clusters_convert(dt);  //SEXP类型可以和R中的对象互转

std::string txt3=
"cat('\nres1='); print(res1)";
R.parseEvalQ(txt3);

return 0;
}
```

### 1.4 RInside, Rcpp, R代码分析    

### 1.4.1 代码分析1  
下面将系统的分析一下C++与R的交互代码。  
```C
int main(int argc, char* argv[]){
    RInside R(argc,argv); //实例化R交互对象。
    std::string txt4 =
        "suppressMessages(library(fPortfolio));"
        "lppData <- 100 * LPP2005.RET[, 1:6];"
        "ewSpec <- portfolioSpec();"
        "nAssets <- ncol(lppData);";
    R.parseEvalQ(txt4);

    const double dvec[6] = {0.1,0.1,0.1,0.1,0.3,0.3};
    const std::vector<double> w(dvec, &dvec[6]);
    R["weightsvec"] = w;
    std::string txt4 = "print(weightsvec);";
    R.parseEvalQ(txt4);
    txt4 = "setWeights(ewSpec)<-weightsvec";
    R.parseEvalQ(txt4);

    txt4 =
        "ewPf <- feasiblePortfolio(data=lppData, spec=ewSpec, constraints=\"LongOnly\");"
        "print(ewPf); "
        "vec <- getCovRiskBudgets(ewPf@portfolio);";
    Rcpp::NumericVector V( (SEXP)R.parseEval(txt4));
    Rcpp::CharacterVector names((SEXP)R.parseEval("names(vec)"));

    std::cout<<"\n\n And now from C++\n\n";
    for(int i=0; i<names.size();i++){
        std::cout<<std::setw(16)<<names[i]<<"\t"
                << std::setw(11)<<V[i]<<"\n";
    }
 }
```
    
通过上面的例子可以看出，R与C++的交互主要通过以下两种方式。  

- 发送命令至R   
	- 字符串  	
	- C++对象赋于R代理对象
```
	 std::string txt4= "print(weightsvec)"
	 R.parseEvalQ(txt4);
```
这是C++程序中，通过文本串的形式，将所要的操作发送至R执行环境。

	
```
	R["weightsvec"] = w;
```  
这里应该是先将C++对象传递给RInside对象，然后RInside对象再（wrap）传递给R代理对象。  

- 接收R执行结果   
```
Rcpp::NumericVector V( (SEXP)R.parseEval(txt4));
```
然后就可以在C++环境中，对Rcpp对象进行处理。
     
     
     
### 1.4.2 代码分析2（Rcpp中的as用法）  
```C
int main(int argc, char* argv[])
{
try{
        RInside R(argc, argv);
        std::string txt;
        txt = "m<-1.23";
        double d1 = Rcpp::as<double>(R.parseEval(txt));
        std::cout<< "d1:\t"<<d1<<std::endl;

        txt = "M <- 1.0*1:6";
        std::vector<double> d2 = Rcpp::as<std::vector<double> >(R.parseEval(txt));
        std::cout<<"d2[0]:\t" <<d2[0]<<"\nd2[1]:\t"<<d2[1]<<std::endl;


        std::string txt2 =
            "x <- rnorm(10,0,1)";
        std::vector<double> d3 = Rcpp::as<std::vector<double> >(R.parseEval(txt2));
        cout<<"begin to print the result that received from R\n";
        for(vector<double>::iterator iter=d3.begin(); iter<d3.end(); iter++){
            cout<<*iter<<"\t";
        }
        cout<<"\n";

        R["x"]=10;
        R["y"]=20;
        R.parseEval("z<-x+y");
        int sum = R["z"];
        std::cout<<"10+20="<<sum<<std::endl;

        sum=R.parseEval("x+y");   //直接隐式转换，把R对象转化为C++对象。
        std::cout<<"10+20="<<sum<<std::endl;

    }catch(std::exception ex){
        std::cerr<<"Exception caught:"<<ex.what()<<std::endl;
    }catch(...){
        std::cerr<<"Unknown exception caught"<<std::endl;
    }
```
- Rcpp类库提供的as函数可以把R环境得到的SEXP对象转化为C++对象（基本对象如int, double等以及stl对象如vector,map等）。另外，R["var_name"]可以直接存取R环境中的对象，也可以当作右值赋于一个C++对象，此时发生as的隐式转换。
     
### 1.4.3 C++函数输出到R环境  
```C
std::string hello( std::string who ){
    std::string result( "hello " ) ;
    result += who ;
    return result;
} 

int main(int argc, char *argv[]) {

    // create an embedded R instance
    RInside R(argc, argv);               

    // expose the "hello" function in the global environment
    R["hello"] = Rcpp::InternalFunction( &hello ) ;
   
    // call it and display the result
    std::string result = R.parseEvalNT("hello(\"world\")") ;
    std::cout << "hello( 'world') =  " << result << std::endl; 

    exit(0);
}
```
     
        
### 2. R扩展——Rcpp包开发  

R开发虽然很容易，但涉及到一些底层操作，如循环的时候，需要用C++的内存操作来加速。 此外， C/C++已有一些开发好的库，没必要用R重写，可以为R所调用。  


### 2.1 .C调用
这种方式使用C语言由R调用，主要有以下几个步骤：

* C语言编写的函数
* 编译
* 加载
* 调用
   
下面，给出一个简单的示例    

### 2.1.1 C语言写的函数    
```C
void double_me(int* x)
{
	*x = *x+*x;	
}
```  

### 2.1.2 编译  
```
$R CMD SHLIB doubler.c
```  


### 2.1.3 加载  
```
dyn.load("doubler.so")
```
  
### 2.1.4 调用  
```
.C("double", x=as.integer(4))
```  
这种方式虽然简单易懂，但R提供的语言接口过于复杂，容易出错，不好管理。


### 2.2 使用Rcpp包服务扩展R包  

Rcpp程序包为用R调用C++代码提供了便利。使用C++来扩展R包，Rcpp及RInside提供了无缝的衔接。

### 2.2.1 使用Rcpp构建扩展包框架    

在R环境中，可以可使用Rcpp包提供的函数(Rcpp.package.skeleton)得到扩展包的框架。
```
>libirary(Rcpp)
>Rcpp.package.skeleton( "Project_Name" )
```

在生成的R包 skeleton中， 可以找到rcpp\_hello\_world.cpp文件， 可以尝试添加几个函数， 修改成如下样式 （注意以下代码为C++文件,扩展名为cpp)

```
#include <Rcpp.h>
using namespace Rcpp;
using namespace std;
// 注意 #include <Rcpp.h> 是调用Rcpp的必要条件
RcppExport SEXP intVec1a(SEXP vec) {
   Rcpp::NumericVector prod_vec(vec);
   int prod = 1;
   for (int i=0; i<vec2.size(); i++) {
       prod *= vec2[i];
   }
   return (wrap(prod));
}

RcppExport SEXP square2(SEXP s)
{ 
 double s_c = Rcpp::as<double>(s);
 double squared = s_c*s_c;
 return (wrap(squared));
}

RcppExport SEXP expfun(SEXP x){
double x2 = Rcpp::as<double>(x);
double ans=1.0, term=1.0, eps=1e-16;
int n=0;
while (fabs(term)>eps){
   n++;
   term = term * x2 / n;
   ans = ans + term;
}
  return(wrap(ans));
}
```

### 2.2.2 编译与安装自定义包   
编译：将R的工作目录设定为当前包所在的目录，在R环境中输入，
```
>compileAttributes()
```
在windows console或linux bash环境下，输入，
```
$R CMD INSTALL Project_Name
```

### 2.2.3 调用  
进入R环境，
```
>library(Project_Name)
>.Call('square2', s= 520)
>.Call('prod_vec', vec= c(3, 4, 5))
>.Call('expfun', x=3)
```

### 2.2.4 卸载  
进入R环境，
```
>remove.packages("package name")
```

### 2.2.5 Wrap  
每次调用都需要调用.Call，不是很方便，可以用R函数包装一下。
```
expfunR <- function(xx){
   return( .Call('expfun', x= xx))
}

square2R <- function(ss){
   return( .Call('square2', s= ss))
}

intVecR <- function(x){
   return(.Call('prod_vec', vec= x))
}
```
