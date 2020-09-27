---
layout:     post
title:      "Part 1: Reproducing Kernels and Construction of RKHS"
subtitle:   "This is the first post of a three-part series on fundamentals of RKHS, which mainly serves as a way to reorganise my understandings of RKHS (in Functional analysis) and kernel methods (in Machine learning) and try to connect the properties of RKHS to its applications in ML."
date:       2020-09-22 10:00
author:     "edenx"
tags: 		[kernel]
category:   math
---

_**Disclaimer.** This post is served as a summarisation of my study notes on RKHS theory [1], and classes I took on relevant topics, containing theoretical details from [1, 2] along with my interpretations directed by my personal interests on those topics. I am by no means an expert in functional analysis and spectral theory, so please feel free to point out any mistakes in the post._
<br/><br/>

With the nice properties of Reproducing Kernel Hilbert Space (RKHS), many important results in ML are analysed theoretically with linear operators on these spaces. To dig into the details, we shall first look into fundamental properties of kernels and RKHS, and how it can be constructed from various perspectives.

To begin with, we give a concise introduction to the definitions and fundamental properties of reproducing kernels and RKHS, which many readers who know kernel methods are familiar with. The following two articles will be devoted to constructing a valid kernel (and its RKHS) from a Complete Orthogonal System (CONS) of a separable Hilbert Space moreover eigen-decomposition of a linear operator on $\calL^2$. 

In the article, we use $\calH$ to denote Hilbert space if without specification; and we use 'linear operator' and 'linear map' interchangeably. The theory can be easily extended to spaces of complex-valued functions, but we here only present the results with real-valued functions for simplicity.

<h2 class="section-heading">Basics and fundamental properties of RKHS</h2>

We will start with introducing the space of fucntions that generalises Euclidean space.

**Definition 1 (Hilbert Space).**_Let $\calH$ be a vector space with an inner product $\inner{\cdot, \cdot}_{\calH}$, and the associated norm $\norm{\cdot}_{\calH}$, where

$$
\norm{f}_{\calH} = \sqrt{\inner{f,f}_{\calH}},\; \forall f\in \calH
$$

Then the vector space $\calH$ is a Hilbert space if it is complete $w.r.t.$ the norm (with all Cauchy sequences converges in $\calH$)._

Then, the following definition gives a special space of functions with smoothness properties.

**Definition 2 (RKHS).**_ Let $\calX$ be a set and $\calH$ be a Hilbert space of functions defined on $\calH$. Then $\calH$ is a Reproducing Kernel Hilbert Space, if there exists a bilinear form $k: \calX \times \calX \to \mathbb{R}$ such that 

$$
\phi(x) = k(x,\cdot), \;\phi:\calX \to \calH \text{ is the feature map},
$$

and 

$$
\inner{f, k(x,\cdot)} = f(x),\; \forall f\in \calH,
$$

we call these the reproducing property of $k$.
Finally, we denote the RKHS $\calH$ with reproducing kernel $k$ interchangeably by $H_k = H_k(\calX)$._

In the following, we will see the correspondence of $k$ and $H_k$ is one-to-one. But first, one more definition is introduced to characterise the bilinear form $k$.

**Definition 2 (Positive Definite Quadratic Form).**_ A function $k: \calX \times \calX \to \mathbb{R}$ is called a positive definite quadratic form, or positive definite function, if for any function $h:\calX\to \mathbb{R}$ and for any finite subset $\calX' \subset \calX$, 

$$
\sum_{x_1, x_2 \in \calX'} h(x_1)h(x_2)k(x_1, x_2)\geq 0
$$

It is said to be strictly positive definite if $h\equiv 0$, i.e. function $h$ is the zero function.
-

Immediately from the definition, we can see any reproducing kernel is a positive definite function, or positive semi-definite (PSD) kernel. The opposite that any positive definite function induces a RKHS is more important and requires some derivations. 

**Theorem 1 (Aronszajn, 1950).**_Let $\calX$ be a metric space, and $k:\calX\times \calX \to \mathbb{R}$ be a positive definite function, there exists a unique Hilbert space $(H_k, \inner{\cdot, \cdot}_{H_k})$ of functions on $\calX$ satisfying the followings:
1. $\phi(x) = k(x,\cdot)\in \calH,\; \forall x\in \calX$;
2. Span$\{\phi(x): x\in \mathcal{X}\}$ is dense in $\calH$; and
3. $f(x) = \inner{\phi(x), f}_{\calH}\; \forall f\in\calH,\, x\in\calX$.
Therefore, $\calH$ is the unique RKHS with reproducing kernel $k$, thus denoted by $H_k$._

_Proof._ We here give a walk-through of the proof, for full details please refer to [2].

Consider 
$$H_{0,k} = \span\{\phi(x): x\in\calX\} = \{f=\sum_{i=1}^s \alpha_i\phi(x_i):x_i \in \calX, \alpha_i\in\R\; \forall i=1,\dots,s, \mathrm{ and } s\in\N\},$$ 

then we show the bilinear form $\inner{\cdot, \cdot}_{H_{0,k}}: H_{0,k} \times H_{0,k} \to \R$,

$$
\inner{f, g}_{H_{0,k}} 
= \inner{\sum_{i=1}^s\alpha_i\phi(x_i), \sum_{j=1}^r\beta_j\phi(y_j)}
= \sum_{i=1}^s\sum_{j=1}^r \alpha_i\beta_j k(x_i, y_j)
$$

is a well-defined inner product, which gives $H_{0,k}$ the structure of a pre-Hilbert space. Moreover, we can prove that $(H_{0,k}, \inner{\cdot, \cdot}_{H_{0,k}})$ satisfies all three conditions in the statement. Note that the definition of the inner product gives condition 3., where 

$$
\inner{f, \phi(x)}_{H_{0,k}} = \sum_{i=1}^s k(x_i, x) = f(x).
$$

The following step is to show the completion of $H_{0,k}$ (by adding the limit of every Cauchy sequence $\{f_n\}_{n\in\N}\subset H_{0,k}$) is a Hilbert space denoted by $H_k$, with bilinear form $\inner{\cdot, \cdot}_{H_k}, \;s.t.$ there exists sequences $\{f_n\}_{n\in\N}, \{g_n\}_{n\in\N} \subset H_{0,k}$

$$
\inner{f,g}_{H_k} = \lim_{n\to \infty} \inner{f_n, g_n}_{H_{0,k}}.
$$

To do this, we need to verify that the limit exists (i.e. to show the sequence of inner product $\{\inner{f_n, g_n}_{H_{0,k}}\}_{n\in\N}$ is a Cauchy sequence). Then, all three conditions follows directly from the definition of completion.

Lastly, the uniqueness of RKHS can be verified such that if $G_k$ is also a Hilbert space satisfying those three conditions, then $G_k = H_k$ and $\inner{\cdot, \cdot}_{G_k} = \inner{\cdot, \cdot}_{H_k}$. Notably, $H_{0,k}\subset G_k$ due to condition 2., and the equivalence of the inner product is directly given by 3. Now, since both $G_k$ and $H_k$ are completions of $H_{0,k}$, the uniqueness follows from the uniqueness of the completion procedure.

$\square$
{:.right}

A direct consequence of Theorem 1 is that given any feature map $\phi(\cdot):\calX\to\calH$, we can define a positive definite function $k(x, x') = \inner{\phi(x), \phi(x')}_{H_k}$ and a corresponding RKHS via procedure demonstrated in Theorem 1; on the other hand, for any RKHS with kernel $k$ (which is unique), we may define the feature map to be $\phi(x) = k(x, \cdot)$. For appropriate choices of feature map, the reproducing kernel $k$ is in closed form. This means that, for data $\{x_n\}_{n\in\N}\subset\calX$, $k(x, x')$ can be computed directly without the evaluation of $\phi(x), \phi(x')$ and the inner product between them. This is known as the kernel method in ML. This is really useful as many feature maps are of infinite dimensions.

Finally, we end this section with a remark:

**Remark 1.**_We can define a evaluation functional on $\calX$ that $k_x\; s.t. \; k_x(f) = f(x)$ for $f\in\calH$, which is a linear operator. Then we have that a Hilbert space is a RKHS iff $k_x$ is continuous $\forall x\in \calX$. In addition, this implies all the functions in RKHS are continuous._
Here, we only prove for the necessary condition, see [2] for full details. 
_Proof._
Since in this case $k_x$ is a continuous linear operator, by Riesz representation theorem, we can find $g_x\in\calH\; s.t.\; f(x) = k_x(f) = \inner{f, g_x}_{\calH},\; \forall f\in\calH$. 
Consider $k(x,y)$ as a function of $y$, then $k(x,y) = k_y(g_x) = \inner{g_x, g_y}_{\calH} = g_x(y)$, for $g_x\in\calH$ a function of $x$, corresponding to the $f$ in last paragraph; and $g_y\in\calH$ a function of $y$ given by Riesz.

$\square$
{:.right}

In fact, we will see in the following posts, an RKHS is characterised by a linear operator (associated to a feature map or a PSD kernel). Moreover, this view allows the smoothness property of RKHS to be analysed with spectral properties of the Integral operator of $k$, which gives connections to Harmonic analysis.


<h2 class="section-heading">References</h2>

1. Saburou Saitoh and Yoshihiro Sawano. Theory of reproducing kernels and applications. Springer, 2016.
2. Zaid Harchaoui, UW [STAT538 Lecture1 handout]({% link /docs/STAT538lec1.pdf %}). 2019.

