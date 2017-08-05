---
layout: postarticle
title: clusterpathRcpp code analysis
date: 2017-08-05 09:25:05 +1000
categories: technology
comments: true
---


### $\ell_1$ penalty clustering method    
$\ell_1$正则项的聚类效果。这一问题的的目标函数可以写成，
\\[
\sum\_{k=1}^p \left[ \frac{1}{2} \sum\_{i=1}^n (\alpha\_{ik}-X\_{ik})^2 +\lambda \sum\_{i<j} w\_{ij} \lvert \alpha\_{ik}-\alpha\_{jk} \rvert \right] = \sum\_{k=1}^p f\_1(\alpha^k,X^k)
\\] 
其中，$\alpha^k \in \mathbb{R}^n$是$\alpha$的第$k$列。 这样，关于矩阵$X$的最小化问题就等价于$p$个分隔开的最小化子问题，
\\[
\min\_{\alpha \in \mathbb{R}^{n\times p} f\_1(\alpha,X)=\sum\_{k=1}^p \min\_{\alpha^k \in \mathbb{R}^n} f\_1(\alpha^k,X^k)
\\]
对于每一个子问题，可以使用FLSA path algorithm来解决。
先看一下效果：
 
<img src="{{ BASE_PATH }}/photo/clusterpathRcpp/1Dl1.png"/>

### 1. STL 简介  

STL(Standard Template Library)是C++的一个标准模板库，现在作为C++的一部分嵌入到编译器，所以只要有C++编译器，那么都可以使用STL。该库集成了诸多常用的基本数据结构与算法，高度体现了可复用性。  

STL将代码抽象为三个主要的类别：container(容器)、algorithm(算法)、iterator(迭代器)。  

网上有一个比较通俗的说法。容器相当于是装东西的东西，如装水的杯子。算法相当于对容器内的东西进行一种操作，如往杯子里倒水。迭代器相当于操作杯子的水的载体，如向水杯里倒水时的水壶，汤勺等。  

### 1.1 容器  

容器主要用于存放数据。可以理解为一种数据结构。在实际应用中，根据所处理的数据类型，选择合适的容器。STL 中的容器有顺序容器和关联容器，容器适配器（congtainer adapters ：stack,queue ，priority queue ），位集（bit_set ）串包(string_package) 等等。 以下是一些常用的容器。  

顺序容器：  

- vector, 连续存储的无素
- list, 双线性列表，只能顺序访问
- deque, 双队列

关联容器：  

- set, 集合
- multiset, 允许有相同元素的集合
- stack, 栈，先进后出
- queue, 队列，先进先出
- map, 映射，由{键，值}对组成的集合
- multimap, 允许键对有相等的次序的映射

### 1.2 算法  

STL中算法大部分不作为某些特定容器类的成员函数，它们是泛型的。这就说明了算法可以适配大部分的容器。泛型算法有4类基本的类型。

- 变序型队列算法
- 非变序型 队列算法
- 排序算法
- 搜索及通用数值算法
特别说明：STL的算法并不只是针对STL容器所设计，对一般的容器也是适用的。

- 变序型算法  
这类算法会改变数据在容器内的位序。主要有，
	- copy(复制)
	- swap(交换)
	- replace(替代)
	- clear(清除)
	- remove(移动)
	- reverse(翻转)

其它具体的算法可以到查看C++ reference.

### 1.3 迭代器  
迭代器实际上是一种泛化指针。如果一个迭代器指向了容器中的某一成员，那么迭代器可以通过自增自减来遍历容器中的所员。迭代器是联系容器和算法的媒介，是算法操作容器的接口。STL定义了6种迭代器。

- 输入迭代器
- 输出迭代器
- 前向迭代器
- 双向迭代器
- 随机访问迭代器
- 流迭代器




