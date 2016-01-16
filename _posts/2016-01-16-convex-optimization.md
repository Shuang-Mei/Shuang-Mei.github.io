---
layout: post
title: "凸优化(Convex Optimization)"
description: "在machine learning 很多问题中，我们最终往往要求解某个函数的最优值。例如least-square, logistic regression, linear regression, svm等等，这类问题统称为优化问题。这篇blog主要介绍了凸集，凸函数及凸优化问题。"
category: 'basic learning'
---

在machine learning 很多问题中，我们最终往往要求解某个函数的最优值。用数学术语表示就是，给定一个函数 $f: R^{n} \rightarrow R$，我们需要求 $x \in R^{n}$使得$f(x)$ 取得最小（大）值。例如least-square, logistic regression, linear regression, svm等等，这类问题统称为优化问题。

在一般情况下，求解任意一个函数的全局最优值是很困难的。但是对于一种特定类型的函数——凸函数（convex function），我们可以很有效的求解其全局最优值。这里的“有效”是指在实际问题求解中，能在多项式复杂度的时间里求解。 人们将这类函数的最值问题称为*凸优化问题（Convex Optimal Problem）*。

这篇博文主要是对凸优化领域进行了一个简单的描述，参考Stanford taught “convex optimization review” by Stephen Boyd。

#1. 凸集

##1.0 凸集的定义
**定义:**一个集合$C$是凸集，当且仅当对任意$x,y \in C$,和$θ \in R$ 且$0\leq \theta \leq 1 $，都有

$$\theta x+(1-\theta)y \in C.$$

其几何意义在于，在集合$C$中任取两个点，连接两点的直线段上的任一点也在集合$C$中。下图是凸集和非凸集的例子：

##1.1 Examples

凸集的实例： 以下列举几个简单的凸集实例

**（1）所有$R^n\quad$** 很显然，对任意给定的$x,y∈R^n$ 都有 $\theta x+(1−\theta)y\in R^n$。 

**（2）非负卦限$\quad$**  $R^{n}_{+}$,很显然也符合定义。

**（3）范数球$\quad$**  $R^n$空间上的某个范数。
（例如欧几里得空间的模为$\parallel x \parallel_{2} =\sqrt{\sum_{i=1}^{n}x_i^2}$.），集合${x:\parallel x\parallel \leq 1}$也是一个凸集。假设$x,y \in R^n$，同时$\parallel x\parallel \leq 1,\parallel y\parallel \leq 1$，并且$0 \leq \theta \leq 1$，有

$$\parallel \theta x+(1-\theta)y)\parallel\leq \parallel \theta x\parallel+\parallel(1-\theta)y\parallel=\theta\parallel x\parallel+(1-\theta)\parallel y\parallel\leq 1$$

**（4）仿射子空间和多面体$\quad$**  给定一个矩阵$A \in R^{m \times n}$和一个向量$b \in R^m$，对应的仿射子空间被定义为${x \in:Ax=b}$。相应的多面体空间为{$x\in R^n:Ax \preceq b$}，"$\preceq$"表示对应的元素不等。

**（5）凸集的交集$\quad$**  假设$C_1,C_2,......C_k$都是凸集，它们的交集为

$$\cap_{i=1}^k C_i = \{x:x \in C_i \vee i=1,...,k\}$$

也是一个凸集，然而，凸集的并集却并不一定是凸集。

**（6）半正定矩阵$\quad$**  所有的半正定矩阵的集合称为"半正定锥"，被表示为$\mathbf{S}_{+}^{n}$，也是一个凸集。 回顾一下，矩阵$A \in R^{n\times n}$是一个对称的半正定矩阵当且仅当$A = A^T$，并且对于所有的$x\in R^n$，$x^TAx\geq 0$。

#2. 凸函数及凸函数判定方法

凸优化中的一个核心概念就是凸函数。

##2.1 定义
**凸函数定义：**一个函数$f:R^n\rightarrow R$是凸函数当且仅当其定义域$D(f)$是凸集，并且对于任意的$x,t\in D(f)$，$\theta \in R$并且$0\leq \theta\leq 1$都有

$$f(\theta x+(1-\theta)y \leq \theta f(x)+(1-\theta)f(y)).$$

也即是说，对于曲线上任意两点所连成的割线一定在函数曲线的上方，如下图所示：

**凸函数一阶条件：**假设函数$f:R^n\rightarrow R$是一阶可导的，那么$f$是凸函数当且仅当，对任意的$x,y\in D(f)$都有：

$$f(y)\geq f(x)+f'(x)(y-x)$$

其中，$f(x)+f'(x)(y-x)$是$f(y)$在$x$处的一阶泰勒展开。

**凸函数二阶条件：**假设函数$f:R^n\rightarrow R$是二阶可导的，那么$f$是凸函数当且仅当，对任意的$x\in D(f)$都有：
$$f''(x)\succeq 0$$
其中，当$f''(x)$是矩阵时，符号$\succeq$表示半正定，而非每个元素不等（在一维的情况下，相当于$\geq$，在二维情况下，不是表示对所有的$i$和$j$都有$X_{ij}\geq 0$，而是表示$X$为半正定矩阵）。

##2.2 Jensen不等式
我们先看看凸函数定义中的不等式：

$$f(\theta x+(1-\theta)y \leq \theta f(x)+(1-\theta)f(y)).$$

其中$0\leq \theta\leq 1$，类似的可以推广到多个点的情况：

$$f(\sum_{i=1}^k\theta_ix_i) \leq \sum_{i=1}k\theta_if(x_i).$$

其中，$\sum_{i=1}^k = 1$并且$\theta_i \geq 0$,$\forall i$。如果将上式$\theta$看成是概率密度，那么可以将上式改写为：

$$f(E(x)) \leq E(f(x))$$

这个不等式称为Jenson不等式。

##2.3 凸函数举例

1. **指数函数$\quad$**对于$f:R\rightarrow R$,$f(x)=e^{ax}$,$a\in R$。使用凸函数的二次判别，$f''(x)=a^2e^{ax}$，对于所有的$x$都是非负的。

1. **负对数函数$\quad$**对于$f:R\rightarrow R$,$f(x)=-log(x)$,定义域$D(f)={x:x >0}$。使用凸函数的二次判别，$f''(x)=1/x^2 >0$，对于所有的$x$都成立。

1. **仿射函数$\quad$**对于$f:R^n\rightarrow R$,$f(x)=b^Tx+c$,$b \in R^n,c\in R$。使用凸函数的二次判别，其Hessian矩阵为，$\bigtriangledown_x^2=0$，对于所有的$x$都成立。由于0矩阵既是半正定也是半负定矩阵，因此函数$f$既是凸函数也是凹函数。实际上，放射函数是仅有的一个既是凸函数也是凹函数的函数。

1. **二次函数$\quad$**对于$f:R^n\rightarrow R$,$f(x)=\frac{1}{2}x^TAx+b^Tx+c$,对于半正定矩阵$A \in S^n,b\in R^n,c\in R$。这个函数的Hessian矩阵为
 $$\bigtriangledown_x^2f(x)=A$$由于$A$矩阵是一个半正定矩阵，因此函数$f$是一个凸函数。函数$f(x)=||x||_2^2=x^Tx$是二次函数的一个特例，它是一个严格的凸函数。

1. **范数$\quad$**对于$f:R^n\rightarrow R$的某些范数，如一范数或者二范数。这些范数是凸函数，但是不能采用凸函数的一阶或者二阶判断来证明，因为它并不是在所有地方都是可导的（如一范数在$x=0$出不可导）。

1. **非负的凸函数加权和$\quad$**如果$f_x,f_2,...,f_k$都是凸函数，并且加权系数$w_1,w_2,...,w_k$都是非负的实数，那么

$$f(x)=\sum_{i=1}^k(w_if_i(x))$$

也是一个凸函数。



##3. 凸优化问题及举例
介绍了凸集合凸函数之后，现在就可以介绍凸优化问题了。

**凸优化问题的一般形式为**

$$min  \ \ f(x)$$

$$s.t\ \ g_i(x) \leq 0,  i=1,...,m$$

$$\ \ \ \      h_i(x) = 0,  i=1,...,m$$

其中，$f$和$g_i$都是凸函数，$h_i$是仿射函数，$x$是优化变量。

**凸优化问题的特例**

**LP问题**

Linear Programming,$f$和$g_i$都仿射函数，形式如下：

$$min\quad c^Tx+d$$

$$\qquad s.t\quad Gx\preceq h,  i=1,...,m$$

$$\ \ \ \ \qquad     Ax=b$$  

其中，$x\in R^n$是优化变量，$c\in R^n, d\in R, G\in R^{m\times n}, h\in R^m, A\in R^{p\times n},b \in R^p$是模型的参数，"$\preceq$"表示每个元素不等。

**QP问题**

Quadratic Programming, 不等式约束函数$g_i$仍然是仿射函数，目标函数$f$是一个凸二次函数，形式如下：

$$min\quad \frac{1}{2}x^TPx+c^Tx+d$$

$$\qquad s.t\quad Gx\preceq h,  i=1,...,m$$

$$\ \ \ \ \qquad     Ax=b$$  

其中，$x\in R^n$是优化变量，$c\in R^n, d\in R, G\in R^{m\times n}, h\in R^m, A\in R^{p\times n},b \in R^p$是模型的参数，$P\in S_{+}^n$是一个半正定矩阵。
(LP是QP问题的特例)

**QCQP问题**

Quadratic Constrained Quadratic Programming, 不等式约束函数$g_i$是一个凸二次函数，目标函数$f$也是一个凸二次函数，形式如下：

$$min\quad \frac{1}{2}x^TPx+c^Tx+d$$

$$\qquad s.t\quad \frac{1}{2}x^TQ_ix+r_i^Tx+s_i \leq 0,  i=1,...,m$$

$$\ \ \ \ \qquad     Ax=b$$  

其中，$x\in R^n$是优化变量，$c\in R^n, d\in R, G\in R^{m\times n}, h\in R^m, A\in R^{p\times n},b \in R^p$是模型的参数，$P\in S_{+}^n$是一个半正定矩阵。同时，$Q_i\in S_{+}^n, r_i \in R^n, s_i \in R$对于每一个$i=1,...,m$都满足。
(QP是QCQP问题的特例)

**SDP问题**

Semidefinite Programming, 这是一个比之前几个凸优化问题都难的优化问题，但是它在机器学习研究中非常普遍，其形式如下：

$$min\quad tr(CX)$$

$$\qquad s.t\quad tr(A_iX) = b_i,  i=1,...,p$$

$$\ \ \ \ \qquad     X\succeq 0$$  

其中，$X\in S^n$是优化变量。
(QCQP是SDP问题的特例)

**SOCP问题**

Second-order Cone Programming，二次锥规划问题，其形式如下：

$$min\quad f^Tx$$

$$\qquad s.t\quad \parallel A_ix+b_i\parallel_2 \leq c_i^Tx+d_i,  i=1,...,m$$

$$\ \ \ \ \qquad     Fx=g$$  

其中，$X\in S^n$是优化变量，$A_i \in R^{n_i\times n}, F\in R^{p\times n}$。不等式约束通常也被称为二次锥约束(SOC)。若$n_i = 0$，退化为LP问题，若$c_i = 0$，退化为QCQP问题。
(QCQP是SDP问题的特例)

参考文献：

[斯坦福凸优化教程](https://web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf)

[北京大学凸优化课程](http://bicmr.pku.edu.cn/~wenzw/courses/lieven-problems.pdf)
