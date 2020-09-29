---
layout:     post
title:      "Part 1: Reproducing Kernels and Construction of RKHS"
subtitle:   "This is the first post of a three-part series on fundamentals of RKHS, which mainly serves as a way to reorganise my understandings of RKHS (in Functional analysis) and kernel methods (in Machine learning) and try to connect the properties of RKHS to its applications in ML."
thumbnail-img: ""
date:       2020-09-22 10:00
author:     "edenx"
tags: 		[kernel, fundamentals of RKHS]
category:   math
---

_**Disclaimer.** This post is served as a summarisation of my study notes on RKHS theory [1], and classes I took on relevant topics, containing theoretical details from [1, 2] along with my interpretations directed by my personal interests on those topics. I am by no means an expert in functional analysis and spectral theory, so please feel free to point out any mistakes in the post._
<br/><br/>

With the nice properties of Reproducing Kernel Hilbert Space (RKHS), many important results in ML are analysed theoretically with linear operators on these spaces. To dig into the details, we shall first look into fundamental properties of kernels and RKHS, and how it can be constructed from various perspectives.

To begin with, we give a concise introduction to the definitions and fundamental properties of reproducing kernels and RKHS, which many readers who know kernel methods are familiar with. The following two articles will be devoted to constructing a valid kernel (and its RKHS) from a Complete Orthogonal System (CONS) of a separable Hilbert Space moreover the eigen-decomposition of a linear operator on $\calL^2$.

In the article, we use $\calH$ to denote Hilbert space if without specification; and we use 'linear operator' and 'linear map' interchangeably. The theory can be easily extended to spaces of complex-valued functions, but we here only present the results with real-valued functions for simplicity.

<h2 class="section-heading">Basics and fundamental properties of RKHS</h2>

We will start with introducing the space of functions that generalises Euclidean space.

**Definition 1 (Hilbert Space).** _Let $\calH$ be a vector space with an inner product $\inner{\cdot, \cdot}\_{\calH}$, and the associated norm $\norm{\cdot}\_{\calH}$, where_
<div>
$$
	\norm{f}_{\calH} = \sqrt{\inner{f,f}_{\calH}},\; \forall f\in \calH
$$
</div>
_Then the vector space $\calH$ is a Hilbert space if it is complete $w.r.t.$ the norm (with all Cauchy sequences converges in $\calH$)._

Then, the following definition gives a special space of functions with smoothness properties.

**Definition 2 (RKHS).** _Let $\calX$ be a set and $\calH$ be a Hilbert space of functions defined on $\calH$. Then $\calH$ is a Reproducing Kernel Hilbert Space, if there exists a bilinear form $k: \calX \times \calX \to \R$ such that_
<div>
$$
	\phi(x) = k(x,\cdot), \;\phi:\calX \to \calH \;\text{is the feature map, and}
$$
</div>
<div>
$$
	\inner{f, k(x,\cdot)}_{\calH} = f(x),\; \forall f\in \calH,
$$
</div>
_we call these the reproducing property of $k$.
Finally, we denote the RKHS $\calH$ with reproducing kernel $k$ interchangeably by $H\_k = H\_k(\calX)$._

In the following, we will see the correspondence of $k$ and $H_k$ is one-to-one. But first, one more definition is introduced to characterise the bilinear form $k$.

**Definition 3 (Positive Definite Quadratic Form).** _A function $k: \calX \times \calX \to \R$ is called a **positive definite quadratic form**, or a **positive definite function**, if for any function $h:\calX\to \R$ and for any finite subset $\calX' \subset \calX$,_
<div>
$$
	\sum_{x_1, x_2 \in \calX'} h(x_1)h(x_2)k(x_1, x_2)\geq 0
$$
</div>
_It is said to be strictly positive definite if $h\equiv 0$, i.e. function $h$ is the zero function._

Immediately from the definition, we can see any reproducing kernel is a positive definite function, or what is often referred to as _**positive semi-definite (PSD) kernel**_. The opposite that any positive definite function induces a RKHS is more important and requires some derivations.

**Theorem 1 (Aronszajn, 1950).** _Let $\calX$ be a metric space, and $k:\calX\times \calX \to \mathbb{R}$ be a positive definite function, there exists a unique Hilbert space $(H\_k, \inner{\cdot, \cdot}\_{H\_k})$ of functions on $\calX$ satisfying the followings:_
1. _$\phi(x) = k(x,\cdot)\in \calH,\; \forall x\in \calX$;_
2. _$\span\\{\phi(x): x\in \mathcal{X}\\}$ is dense in $\calH$; and_
3. _$f(x) = \inner{\phi(x), f}\_{\calH}\; \forall f\in\calH,\, x\in\calX$._

_Therefore, $\calH$ is the unique RKHS with reproducing kernel $k$, thus denoted by $H\_k$._

_Proof._ We here give a walk-through of the proof, for full details please refer to [2].
Consider
<div>
$$
	H_{0,k} = \span\{\phi(x): x\in\calX\}
	= \{f=\sum_{i=1}^s \alpha_i\phi(x_i):x_i \in \calX, \alpha_i\in\R\; \forall i=1,\dots,s, \;\mathrm{and}\; s\in\N\},
$$
</div>
then we show the bilinear form $\inner{\cdot, \cdot}\_{H\_{0,k}}: H\_{0,k} \times H\_{0,k} \to \R$,
<div>
$$
	\inner{f, g}_{H_{0,k}}
	= \inner{\sum_{i=1}^s\alpha_i\phi(x_i), \sum_{j=1}^r\beta_j\phi(y_j)}_{\calH}
	= \sum_{i=1}^s\sum_{j=1}^r \alpha_i\beta_j k(x_i, y_j)
$$
</div>
is a well-defined inner product, which gives $H\_{0,k}$ the structure of a pre-Hilbert space. Moreover, we can prove that $(H\_{0,k}, \inner{\cdot, \cdot}\_{H\_{0,k}})$ satisfies all three conditions in the statement. Note that the definition of the inner product gives condition 3., where
<div>
$$
	\inner{f, \phi(x)}_{H_{0,k}} = \sum_{i=1}^s k(x_i, x) = f(x).
$$
</div>
The following step is to show the completion of $H_{0,k}$ (by adding the limit of every Cauchy sequence $\\{f\_n\\}\_{n\in\N}\subset H\_{0,k}$) is a Hilbert space denoted by $H\_k$, with bilinear form $\inner{\cdot, \cdot}\_{H\_k}, \;s.t.$ there exists sequences $\\{f\_n\\}\_{n\in\N}, \\{g\_n\\}\_{n\in\N} \subset H\_{0,k}$
<div>
$$
	\inner{f,g}_{H_k} = \lim_{n\to \infty} \inner{f_n, g_n}_{H_{0,k}}.
$$
</div>
To do this, we need to verify that the limit exists (i.e. to show the sequence of inner product $\\{\inner{f\_n, g\_n}\_{H\_{0,k}}\\}\_{n\in\N}$ is a Cauchy sequence). Then, all three conditions follows directly from the definition of completion.

Lastly, the uniqueness of RKHS can be verified such that if $G\_k$ is also a Hilbert space satisfying those three conditions, then $G\_k = H\_k$ and $\inner{\cdot, \cdot}\_{G\_k} = \inner{\cdot, \cdot}\_{H\_k}$. Notably, $H\_{0,k}\subset G\_k$ due to condition 2., and the equivalence of the inner product is directly given by 3. Now, since both $G\_k$ and $H\_k$ are completions of $H\_{0,k}$, the uniqueness of the RKHS follows from the uniqueness of the completion procedure.
<div style="text-align: right"> $\square$ </div>
A direct consequence of Theorem 1 is that given any feature map $\phi(\cdot):\calX\to\calH$, we can define a positive definite function $k(x, x') = \inner{\phi(x), \phi(x')}\_{H\_k}$ and a corresponding RKHS via procedure demonstrated in Theorem 1; on the other hand, for any RKHS with kernel $k$ (which is unique), we may define the feature map to be $\phi(x) = k(x, \cdot)$. For appropriate choices of feature map, the reproducing kernel $k$ is in closed form. This means that, for data $\\{x\_n\\}\_{n\in\N}\subset\calX$, $k(x, x')$ can be computed directly without the evaluation of $\phi(x), \phi(x')$ and the inner product between them. This is known as the kernel method in ML, which is really useful practically as many feature maps are of infinite dimensions (e.g. Gaussian).

Finally, we end with a remark:

**Remark.** _We can define a evaluation functional on $\calX$ that $k\_x\; s.t. \; k\_x(f) = f(x)$ for $f\in\calH$. Then we have that a Hilbert space is a RKHS iff linear operator $k\_x$ is continuous $\forall x\in \calX$. In addition, this implies all the functions in RKHS are continuous._
_Proof._
Here, we only prove for the necessary condition, see [2] for full details.

Since in this case $k\_x$ is a continuous linear operator, by Riesz representation theorem, we can find $g\_x\in\calH\; s.t.\; f(x) = k\_x(f) = \inner{f, g\_x}\_{\calH},\; \forall f\in\calH$.
Consider $k(x,y)$ as a function of $y$, then $k(x,y) = k\_y(g\_x) = \inner{g\_x, g\_y}\_{\calH} = g\_x(y)$, for $g\_x\in\calH$ a function of $x$, corresponding to the $f$ in last paragraph; and $g\_y\in\calH$ a function of $y$ given by Riesz.
<div style="text-align: right"> $\square$ </div>
This effectively shows that an RKHS is characterised (and can be constructed) by a continuous linear operator.
In fact, we will see in the following posts that apart from evaluation functional, there are linear operators mapping from $\calH$ to $H_k$ (associated with a feature map or a PSD kernel) that also do the job. Particularly, the linear operators associates nice properties of (separable) Hilbert spaces to the RKHS in terms of CONS and eigen-decomposition. Moreover, this view allows the smoothness property of RKHS to be analysed with spectral theorem of the Integral operator of $k$, which gives connections to Harmonic analysis. This also has important consequences in the use of RKHS in many fields.

<h2 class="section-heading">References</h2>

1. Saitoh, S and Sawano, Y. Theory of reproducing kernels and applications. Springer, 2016.
2. Harchaoui, Z. STAT 538 Statistical Learning: Modeling, Prediction, And Computing, [Lecture 2](docs/STAT538lec2.pdf). University of Washington, 2019.
