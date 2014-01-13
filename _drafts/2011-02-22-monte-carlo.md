---
title: Monte Carlo 之积分篇
layout: post
categories:
  - 学术
  - R
tags:
  - Importance Sampling
  - Monte Carlo
  - 蒙特卡罗
  - 积分
  - R
  - Hit or Miss
  - Sample Mean
---
可能是因为本人不太喜欢推导数学公式的缘故，因此在初次遇到蒙特卡洛方法的那一刻便深深的恋上了它……

喜欢Monte Carlo方法的原因还可能跟我喜欢用R做编程有关，很多复杂的问题，甚至数理方面难以求解的问题，利用Monte Carlo方法也可以轻松拿下！当然我们要借用计算机，让它帮我们计算海量的数据，倘若再往前推上30年，估计Monte Carlo几乎是一个没有利用价值的方法。

本文着重介绍3类Monte Carlo方法：Hit or Miss Monte Carlo Method, Sample-Mean Monte Carlo Method, Importance Sampling.

## 一、Hit or Miss Monte Carlo Method

这个方法非常的容易理解，我们用下图做下简单的说明：

![Hit and Miss](img)

我们欲求某函数在区间$[a, b]$上的积分值，首先我们要找一个常数$c$，使得它大于等于函数在$[a, b]$区间上的最大值（$c$取函数最大值时效率最高），然后利用$a$, $b$, $c$的值做一个矩形，这个矩形的面积为$(b-a)c$。


然后在矩形内随机打点，在函数下方（阴影部分）的点我们记为`Hit`,上方的点我们记作`Miss`。如果我们总共打了$N$个点，有$n$个点落在阴影部分，那么我们很容易得知，阴影部分的面积与矩形面积的比值即为$\frac{n}{N}$。

根据积分的几何意义，阴影部分的面积大小等于函数在$[a, b]$区间上的积分值，即$(a-b)\cdot c \frac{n}{N}$ 。

我们来看一个实例，用Hit or Miss 方法求$Pi$的值，由于思想比较简单，不做过多的解释，R代码如下：

{% highlight r%}
my.pi = function(n){
 x = runif(n)
 y = runif(n)
 4*sum(x^2 + y^2 < 1)/n
}
set.seed(123)
my.pi(100000)
{% endhighlight %}

结果为：

    [1] 3.14408
    
![pi](img)

这里我们打了十万个点，但结果却不是很令人满意，千分位上的数字已经不准确了。于是我们很自然的想到一个问题：我们要取多少点才能达到我们想要的精确度呢？

如图一所示，我们记事件$X$为点在矩形区域内的位置，第$i$个点落在阴影区域时记为$X_i=1$，否则为$X_i=0$ 。显然每一次打点都是一次Bernoulli实验，打$N$次点，$\sum_{i=1}^NX_N$就服从二项分布$B(N, p)$, 其中$p$为点落在阴影部分的概率。

我们用$I$表示函数在$[a, b]$区间上的积分值，$\hat{I}$表示估计值，则

$$
\begin{align}
\hat{I} & =c(b-a)\frac{\sum_{i=1}^NX_N}{N} \\
Var(\hat{I}) & =c^2(b-a)^2\frac{p(1-p)}{N}
\end{align}
$$

下面我们来求使得Hit or Miss方法的误差在误差限度$\epsilon$范围内的概率落在$1-\alpha$信赖区间里所需要的样本大小。

根据`Chebyshev`不等式，有

$$
\begin{align}
& P(|\hat{I}-I|\geq\epsilon) \leq\frac{E(|\hat{I}-I|^2)}{\epsilon^2} \\
\Rightarrow & P(|\hat{I}-I|<\epsilon) \geq 1-\frac{var(\hat{I})}{\epsilon^2}\approx 1-\alpha \\
\Rightarrow & \frac{var(\hat{I})}{\epsilon^2}\approx \alpha \\
\Rightarrow & c^2(b-a)^2\frac{p(1-p)}{N}\approx\epsilon^2\alpha \\
\Rightarrow & N\approx c^2(b-a)^2\frac{p(1-p)}{\epsilon^2\alpha}\leq\frac{c^2(b-a)^2}{4\epsilon^2\alpha}
\end{align}
$$

利用这个公式我们就可以求保持某种精确度下所需的样本数。拿上面求$Pi$的例子来说，我们如果希望结果的误差不超过0.001的概率为99%，那么需要的N值是多大呢？

显然，我们要使四分之一个圆的面积积分的误差不超过0.001/4=0.00025，即$\epsilon=0.00025$, $\alpha=0.01$，带入公式计算可得$N\geq\frac{1}{4\times0.01\times(0.001/4)^2}=400,000,000$
我们想精确到千分位就要打4亿个点，貌似这个方法的效率非常低，不给力啊！

## 二、Sample-Mean Monte Carlo Method

先给出Sample-Mean方法的算法：如果我们想求积分$\int_a^b g(x)dx$的值，则首先生成$n$个在$[a, b]$区间上服从均匀分布的随机数$x_1, \cdots, x_n$，那么$\frac{\sum_{i=1}^ng(x_i)}{n}(b-a)$便是我们要求的积分值。数理角度的证明很简单，就是简单的利用了期望的定义：（这里我们构造了[a,b]区间上的均匀分布，其密度函数为$\frac{1}{b-a}$）

$$
\begin{align}
& \int_a^b g(x)dx \\
= & (b-a)\int_a^b g(x)\frac{1}{b-a}dx \\
= & (b-a)\mathbb{E}_\mu(g(\mu)) \\
= & (b-a)\frac{\sum_{i=1}^n g(\mu_i)}{n}
\end{align}
$$

从几何角度来看，结论就变得非常直观：
$g(x)$是定义在$[a, b]$区间上的函数，那么$g(x)$在$[a, b]$区间上的平均值用积分形式可表示为：

$$f_{ave} = \frac{1}{b-a}\int_a^b g(x)dx$$

如果$x_1, \cdots, x_n$是$[a, b]$区间上服从均匀分布的随机数，那么$g(x)$在$[a, b]$区间上的平均值亦可以近似的用$g(x_1), \cdots, g(x_n)$的平均值表示,即

$$f_{ave} \approx \frac{\sum_{i=1}^n g(x_i)}{n}$$

于是 ：

$$
\begin{align}
f_{ave} &= \frac{1}{b-a}\int_a^bf(x)dx \approx \frac{\sum_{i=1}^ng(x_i)}{n} \\
& = \int_a^bg(x)dx \approx (b-a)\frac{\sum_{i=1}^ng(x_i)}{n}
\end{align}
$$

我们利用Sample-Mean方法来求一下$Pi$值：

{% highlight r%}
my.pi1 = function(n){
 x = runif(n)
 4*mean(sqrt(1 - x^2))
}
{% endhighlight%}

值得一提的是，Sample-Mean方法要比Hit or Miss方法的效率高：

{% highlight r%}
x = y = numeric()
for(i in 1:100){
x[i] = my.pi(1000)
y[i] = my.pi1(1000)
}
var(x); var(y)
{% endhighlight%}

    [1] 0.003233623
    [1] 0.000876325

可以看出，同样n=1000，Sample-Mean方法的方差比Hit or Miss方法的方差小的多。

## 三、Importance Sampling

![normal](img)

简单得说一下重点抽样的思想。如右图所示,这是正态分布的密度函数图像，我们欲求该函数在区间$[-6, 6]$上的积分值。如果我们利用前面介绍的两种方法来做的话，我们会发现，在函数的尾部$[-6,-3]\&[3,6]$区间上只有极少的点能落在阴影区域内，这就意味着我们浪费了很多时间打了一堆没用的点，效率很低。

为了提高效率，Importance Sampling采用构造一个与原函数图像相似并且容易生成随机数的密度函数$h(x)$，这样我们利用$h(x)$生成的随机数便可以大大的提高效率。

$$
\int_a^b f(x)dx = \int_a^b\frac{f(x)}{h(x)}h(x)=\mathbb{E}_h\frac{f(x)}{h(x)} \approx \frac{1}{n}\sum_{i=1}^{n}\frac{f(x_i)}{h(x_i)}
$$ 

我们援引Use R!系列丛书中的《Introducing Monte Carlo Methods with R》里面3.3节的一个例子来说明。

$Z~N(0, 1)$，求$P(Z>4.5)$

最容易想的方法是直接从标准正态分布上生成$N$个随机数，然后用比4.5大的值的数目除以$N$，代码也很简练

{% highlight r%}
sum(rnorm(10000) > 4.5)/10000
{% endhighlight%}
    
    [1] 0

但结果竟然是0，也就是说我们生成了10000个点，没有一个点是比4.5大的，我们看一下$pnorm(-4.5)$的值，为$3.397673e-06$，这意味着平均我们要打近三十万个点才会有一个点比4.5大，可见效率之低……

我们再来看一下用Importance Sampling方法怎么来做。考虑到求$P(Z>4.5)$既是求标准正态分布的密度函数$f(x)$在区间$[4.5, \infty]$上的积分，并且$f(x)$在该区间上是单调递减的函数，很容易想到构造一个指数分布函数。这里我们构造了$h(x) = e^{-(x-4.5)}$，根据前面所述的方法代码如下：

{% highlight r%}
n = 1000
x = rexp(n) + 4.5
weit = dnorm(x) / dexp(x - 4.5)
mean(weit)
{% endhighlight%}

    [1] 3.198016e-06

哇，我们这里$n$仅仅取了1000，就得到了与真实值如此接近的结果，可以称得上是相当给力了吧！

以后见了用数理方法难以计算的积分问题，就用Monte Carlo解决掉吧！

