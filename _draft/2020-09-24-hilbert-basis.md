---
layout:     post
title:      "Part 2: Connection of RKHS to Hilbert space via CONS"
subtitle:   "With the nice properties of Reproducing Kernel Hilbert Space (RKHS), many important results in ML are analysed theoratically with linear operators on these spaces. To dig into the details, we shall first look into fundamental properties of kernels and RKHS, and how it can be constructed from various perspectives."
date:       2020-09-24 20:00
author:     "edenx"
tags: 		[kernel]
category:   math
---

_**Disclaimer.** This post is served as a summarisation of my study notes on RKHS theory [1], and classes I took on relevant topics, containing theoratical details from [1, 2] along with my interpretations directed by my personal interests on those topics. I am by no means an expert in functional analysis and spetral theory, so please feel free to point out any mistakes in the post.
<br/><br/>_

Consider a feature map $\phi:\calX\to \calH$, then we define a linear operator $L:\calH\to \calF{\calX}$ from a Hilbert space $\calH$ on $\calX$ to the space of all real-valued functions defined on $\calX$, s.t.
$$
L\bf = \inner{\bf, \phi(\cdot)}_{\calH}\; \forall \bf\in \calH
$$
Moreover, we define the quadratic form
$$
k(x,y) = \inner{\phi(x), \phi(y)}_{\calH},
$$
which is a positive definite function. Then we denote by $\calR(L)$ the image space of $L$, which is a linear function space. In $\calR(L)$, consider the norm
$$
\norm{f}_{\calR(L)} = \inf\{\norm{\bf}_{\calH}: \bf\in\calH, f = L\bf\},
$$

**Theorem 2 (Thm 2.36, S.Saitoh 2016).**_ With the definitions above, we have the following properties for the image space $\calR(L)$: 
1. $\calR(L)$ is a Hilbert space;
2. The function $k$ is unique and satisfies reproducing property;
3. Finally, the linear mapping $L$ is an isometry from $(\calH, \inner{\cdot, \cdot}_{\calH}$ to $(\calR(L), \inner{\cdot, \cdot}_{\calR(L)})$ (iff $\calH = \ker{L}^{\perp}$) iff $\Span\{\phi(x):x\in\calX\}$ is a dense subspace of $\calH$._

_Proof._


$\square$
{:.right}

<h2 class="section-heading">Linear mappings and CONS of seperable Hilbert space</h2>

Let $\calH$ be a seperable Hilbert space with a Complete orthogonal system (CONS) {V_j}_{j=1}^{\infty}, which is countable. We denote the image space in Theorem 2 as $H_k$ and assume the linear operator $L$ is as before, then define 
$$
v_j = LV_j = \inner{V_j, \phi(\cdot)}_{\calH} \in H_k.
$$
By Parseval's identity, we see that $\phi(x) = \sum_{j=1}^{\infty} \inner{\phi(x), V_j}_{\calH}V_j = \sum_{j=1}^{\infty} v_j(x)V_j$ and
$$
\sum_{j=1}^{\infty} \abs{v_j(x)}^2
= \sum_{j=1}^{\infty} \abs{\inner{V_j, \phi(x)}_{\calH}}
= \norm{\phi(x)}^2_{\calH} 
$$
In addition, we can equivalently define the kernel $k$ as
\begin{equation*}
\begin{align}
k(x, y) &= \inner{\phi(x), \phi(y)}_{\calH} \\
&= \sum_{j=1}^{\infty} \inner{\phi(x), V_j}\inner{\phi(y), V_j}\\
&= \sum_{j=1}^{\infty}
\end{align}
\end{equation*}
again by Parseval's identity.

With the above setup, we are now ready to give an alternative characterisation of RKHS,

**Theorem 3 (Thm 2.25, S.Saitoh 2016).**_Assume $L$ is injective and $\Span\{\phi(x): x\in\calX\}$ is dense in $\calH$, then the RKHS in Theorem 2 can be formulated as 
$$
H_k = \left\{f\in\calH:
f=\sum_{j=1}^{\infty}a_jv_j: \norm{f}_{H_k}^2=\{a_j\}_{j=1}^{\infty} \in \ell^2(\N)
\right\}
$$
with inner product
$$
\innerbig{\sum_{j=1}^{\infty}a_jv_j}_{H_k} = \sqrt{\sum_{j=1}^{\infty} \abs{a_j}^2}
$$_

From Theorem 3, it is clear that $\{v_j\}_{j=1}^{\infty}$ is dense in $H_k$, moreover, as $L$ is injective, we have $\inner{v_i, v_j}_{H_k} = \inner{LV_i, LV_j}_{H_k} = \inner{V_i, V_j}_{\calH} = 0$. Therefore $v_i\perp v_j$, i.e. $\{v_j\}_{j=1}^{\infty}$ is a complete orthogonal system in the RKHS $H_k$.

Furthermore, [1] shows $T_{H_k}(f) = \sum_{j=1}^{\infty} \inner{f,v_j}_{H_k}V_j$ is an isometry from $H_k$ to $\calH$, i.e. $\norm{f}_{H_k} = \norm{T_{H_k}(f)}_{\calH}$ regardless of the injectivity of $L$. This gives a nice correspondance between the RKHS and the Hilbert space, however, it is not useful in analysing the smoothing property of the RKHS, which is one of the reasons the kernel method became so popular in the first place. We will see why and how the norm of RKHS induces smoothing condition on the space in the next post on Mercer's theorem, and the spectral perspective of RKHS via Integral operator.


<h2 class="section-heading">References</h2>

1. Saburou Saitoh and Yoshihiro Sawano. Theory of reproducing kernels and applications. Springer, 2016.
2. Hofmann T, Schölkopf B, Smola AJ. Kernel methods in machine learning. The annals of statistics. 2008 Jun 1:1171-220.
