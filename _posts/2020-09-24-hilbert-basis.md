---
layout:     post
title:      "Part 2: Characterising RKHS with linear operators on Hilbert space"
subtitle:   "In this article, we will see how an RKHS can be constructed by a linear operator on a Hilbert space, which has an important example linking probability and RKHS of stationary kernels, i.e. Bochner's Theorem. For the second part, we will see any complete orthogonal system (CONS) in a separable Hilbert space will give rise to a characterisation of RKHS."
date:       2020-09-24 12:00
author:     "edenx"
tags: 		  [kernel, fundamentals of RKHS]
category:   math
---

_**Disclaimer.** This post is served as a summarisation of my study notes on RKHS theory [1], and classes I took on relevant topics, containing theoretical details from [1, 2] along with my interpretations directed by my personal interests on those topics. I am by no means an expert in functional analysis and spectral theory, so please feel free to point out any mistakes in the post.
<br/><br/>_

In this article, we will see the characterisation of RKHS as a image space of a linear operator associated with a feature map $\phi: \calX\to\calH$ on a (separable) Hilbert space $\calH$. The construction of the reproducing kernel from $\phi$ is obvious as shown in [Part 1](2020-09-22-construction-of-RKHS.md), however, what is more worthy of presenting is the direct construction of RKHS from a Hilbert space via the linear operator itself. We will show why this view is useful in practice via an import example, which is the Bochner's theorem. For Section 2, we will characterise RKHS with any CONS of the separable Hilbert space $\calH$.

In the article, we use $\calH$ to denote Hilbert space if without specification; and we use 'linear operator' and 'linear map' interchangeably. The theory can be easily extended to spaces of complex-valued functions, but we here only present the results with real-valued functions for simplicity.

<h2 class="section-heading">RKHS via linear mappings</h2>
Consider a feature map $\phi:\calX\to \calH$, then we define a linear operator $L:\calH\to \calF(\calX)$ from a Hilbert space $\calH$ on $\calX$ to the space of all real-valued functions on $\calX$, s.t.
<div>
$$
  L\mathbf{f} = \inner{\mathbf{f}, \phi(\cdot)}_{\calH}\; \forall \mathbf{f}\in \calH
$$
</div>
Moreover, we define the quadratic form
<div>
$$
  k(x,y) = \inner{\phi(x), \phi(y)}_{\calH},
$$
</div>
which is a positive definite function as in [Part 1](2020-09-22-construction-of-RKHS.md). Then we denote by $\calR(L)$ the image space of $L$, which is a linear function space. In $\calR(L)$, consider the norm
<div>
$$
  \norm{f}_{\calR(L)} \equiv \inf\{\norm{\mathbf{f}}_{\calH}: \mathbf{f}\in\calH, f = L\mathbf{f}\},
$$
</div>
Then we have the following theorem giving the construction of RKHS via $L$.

**Theorem 2 (Thm 2.36, S.Saitoh 2016).** _With the definitions above, we have the following properties for the image space $\calR(L)$:_
1. _$\calR(L)$ with the norm defined above is a Hilbert space;_
2. _The function $k$ defined previously is unique and satisfies reproducing property;_
3. _Assume $L$ is injective, then $L$ is an isometry from $(\calH, \inner{\cdot, \cdot}\_{\calH}$ to $(\calR(L), \inner{\cdot, \cdot}\_{\calR(L)})$ (_iff_ $\calH = \ker{L}^{\perp}$) _iff_ $\span\\{\phi(x):x\in\calX\\}$ is a dense subspace of $\calH$._

_Proof._
We first denote $\Pker:\calH \to \calR(L)$ as the orthogonal projection from $\calH$ to $\ker{L}^{\perp}$, where $\ker{L}$ is the null space of the linear mapping $L$ defined as
<div>
$$
    \ker{L} \equiv \{\mathbf{f}\in\calH: L\mathbf{f}=0\}
    = \cap_{x\in\calX}\{\mathbf{f}\in\calH:\inner{f, \phi(x)}_{\calH} = 0\}
$$
</div>
This implies that $\ker{L}$ is a closed subspace of $\calH$, therefore for some $\mathbf{h}\in\ker{L}$ and $f = L\mathbf{f}$,
<div>
$$
  \begin{align}
  \norm{f}_{\calR(L)}
  &=\norm{L\mathbf{f}}_{\calR(L)}
  = \norm{L\mathbf{f} - L\mathbf{h}}_{\calR(L)}
  = \inf_{\mathbf{h}\in\ker{L}}\norm{\mathbf{f}-\mathbf{h}}_{\calH}\\
  &=\norm{\Pker\mathbf{f}}_{\calH} \label{Eq:isometry}
  \end{align}
$$
</div>
which means $L\vert\_{\ker{L}^{\perp}}$ is an isometry between $(\ker{L}^{\perp}, \inner{\cdot, \cdot}\_{\calH})$ and $(\calR(L), \inner{\cdot, \cdot}\_{\calR(L)})$. Hence, the latter is a Hilbert space.

Now, we turn to the second property. Clearly, $k(x,\cdot) = L\phi(x) = \inner{\phi(\cdot), \phi(x)}\_{\calH} \in \calR(L)$; and for any $\mathbf{f}\_0\in\ker{L}$,
<div>
$$
  \inner{\mathbf{f}_0, \phi(x)}_{\calH} = 0 \;\forall x\in\calX
$$
</div>
hence ${\phi(x)}\_{x\in\calX}\subset \ker{L}^{\perp}$. For some $\mathbf{f}\in\calH\; s.t. \; f = L\mathbf{f}\in\calR(L)$, the reproducing property follows accordingly,
<div>
$$
  \begin{align*}
    \inner{f, k(x,\cdot)}_{\calR(L)}
    &= \inner{L\mathbf{f}, L\phi(x)}_{\calH}
    = \inner{\Pker \mathbf{f}, \Pker \phi(x)}_{\calH}\\
    &= \inner{\Pker\mathbf{f}, \phi(x)}_{\calH}
    = L\mathbf{f}(x) = f(x)
  \end{align*}
$$
</div>
where the second equality is due to Equation \eqref{Eq:isometry}, the third equality is by the definiton of $L$. And the uniqueness of $k$ can be easily verified by considering $k(x,\cdot)$.

Finally, we have seen from Equation \eqref{Eq:isometry}, $L\vert\_{\ker{L}^{\perp}}$ is an isometry between $(\ker{L}^{\perp}, \inner{\cdot, \cdot}\_{\calH})$ and $(\calR(L), \inner{\cdot, \cdot}\_{\calR(L)})$. Then $L$ is isomorphic iff $\calH=\ker{L}^{\perp}$. Now, if $\mathbf{f}\in\calH$ is perpendicular to all $\phi(x), x\in\calX$, then $\inner{f, \phi(x)}\_{\calH} = 0\;\forall x\in\calX$, with the injectivity of $L$, we must have $\mathbf{f}\equiv 0$. Therefore, $\\{\phi(x): x\in\calX\\}$ spans a dense subspace of $\calH$.

Moreover, we know $\\{\phi(x): x\in\calX\\}\subset \ker{L}^{\perp}$, hence $\calH = \ker{L}^{\perp}$.
<div style="text-align: right"> $\square$ </div>
Notably, the last statement of Theorem 1 says that $L$ is an isometry between $\calH$ and $\calR(L)$ iff $\\{\phi(x): x\in\calX\\}$ is complete in $\calH$. In this case, we can just say $L$ is isometric from $\calH$ to $\calH$. And we may denote such image space as $H_k$.

The most common function space that can be applied to the above formulation is $\calL^2$ space, which is also very important in Fourier analysis. In particular, we will see the following example connecting stationary kernels to the Fourier transform (which is linear and an isometry from $\calL^2$ to $\calL^2$) of non-negative Borel measures. This has many important applications, in particular for Gaussian Process, one reference I would pick for this is by Micheal Stein [3]; and of course the Random Fourier features (RFF) developed by the ML community for global approximation of Covariance function of a GP is also worth mentioning.

**Example (Bochner's theorem, S.Bochner 1933).**
For this example, we will not prove the theorem itself but provide with its consequences in representing a RKHS [1, 2]. Here we present the version in [4].

**Theorem 3 (H.Wendland 2004).** _A continuous function $h$ on $\calX=\R^d$ is positive definite iff there exists a finite non-negative Borel measure $\mu$ on $\R^d$ such that_
<div>
$$
  h(x) = \int_{\R^d} e^{-i\inner{x,\omega}\; d\mu(\omega)}.
$$
</div>

Now, assume $\nu(\omega)$ is the non-vanishing density w.r.t $\mu$ and assume $L^2(\R^d)$ with uniform measure, by Theorem 3, we have
<div>
$$
  k(x,x') = \int e^{-i\inner{x-x', \omega}} \nu(\omega)\;d\omega
  = \int e^{-i\inner{x, \omega}} \overline{e^{-i\inner{x', \omega}}} \nu(\omega)\;d\omega.
$$
</div>
Recall the $d$-dim Fourier transform is given by
<div>
$$
  \calF(f)(\omega)
  = (2\pi)^{-d/2} \int f(x) e^{-i\inner{x,w}}\;dx
$$
</div>
Then the Fourier transform of $k(x,x')$ is
<div>
$$
  \begin{align*}
    \calF(k(x,\cdot))(\omega)
    & = (2\pi)^{-d/2} \int\int(\nu(\omega')e^{-i\inner{x, \omega'}})
    e^{i\inner{x', \omega'}}\;d\omega' e^{-i\inner{x', \omega}} dx' \\
    &= (2\pi)^{-d/2}\nu(\omega)e^{-i\inner{x, \omega}}
  \end{align*}
$$
</div>
Substuting back the expression of $e^{-i\inner{x, \omega}}$ in terms of $\calF(k(x,\cdot))(\omega)$ into the kernel gives the following form of $k$
<div>
$$
  k(x,x')
  = (2\pi)^{-d/2}\int \frac{\calF(k(x,\cdot))(\omega) \overline{\calF(k(x',\cdot))(\omega)}}{\nu(\omega)}\;d\omega
$$
</div>
And clearly, the RKHS is given by
<div>
$$
  H_k = \{f\in \calL^2(\R^d):\int_{\R^d}\frac{\abs{F(f)}^2}{\nu(\omega)}\;d\omega < +\infty\}.
$$
</div>
This representation of $H\_k$ is also useful in defining/proving characteristic kernel, where informally, a characteristic kernel is a uniformly bounded PSD kernel that injectively maps a probability distribution $P$ to its mean element $\mu\_{P}$ (s.t. $\E\_{x\sim P}[f(x)] = \inner{\mu\_P, f}\_{H\_k}$). This is used in e.g. Maximum mean discrepancy for two samples test.

<h2 class="section-heading">Characterising RKHS via CONS of separable Hilbert space</h2>
Finally, we will see how a RKHS may be represented by any Complete orthogonal system (CONS) of separable Hilbert space.

Let $\calH$ be a separable Hilbert space with CONS $\\{V\_j\\}\_{j=1}^{\infty}$, which is countable. We denote the image space in Theorem 2 as $H\_k$ and assume the linear operator $L$ is as before, then define
<div>
$$
  v_j = LV_j = \inner{V_j, \phi(\cdot)}_{\calH} \in H_k.
$$
</div>
By Parseval's identity, we see that $\phi(x) = \sum\_{j=1}^{\infty} \inner{\phi(x), V\_j}\_{\calH}V\_j = \sum\_{j=1}^{\infty} v\_j(x)V\_j$ and
<div>
$$
  \sum_{j=1}^{\infty} \abs{v_j(x)}^2
  = \sum_{j=1}^{\infty} \abs{\inner{V_j, \phi(x)}_{\calH}}
  = \norm{\phi(x)}^2_{\calH}
$$
</div>
In addition, we can equivalently define the kernel $k$ as
<div>
$$
  \begin{align*}
    k(x, y) &= \inner{\phi(x), \phi(y)}_{\calH}
    = \sum_{j=1}^{\infty} \inner{\phi(x), V_j}\inner{\phi(y), V_j}\\
    &= \sum_{j=1}^{\infty} v_j(x)v_j(y)
  \end{align*},
$$
</div>
again by Parseval's identity.

With the above setup, we are now ready to give an alternative characterisation of RKHS [1],

**Theorem 4 (Thm 2.25, S.Saitoh 2016).** _Assume $L$ is injective and $\span\\{\phi(x): x\in\calX\\}$ is dense in $\calH$, then the RKHS in Theorem 1 can be formulated as_
<div>
$$  
  H_k = \left\{f\in\calH:
  f=\sum_{j=1}^{\infty}a_j v_j:
  \{a_j\}_{j=1}^{\infty} \in \ell^2(\N)
  \right\}
$$
</div>
_with norm_
<div>
$$
  \norm{f}_{H_k} =
  \norm{\sum_{j=1}^{\infty}a_jv_j}_{H_k} = \sqrt{\sum_{j=1}^{\infty} \abs{a_j}^2}
$$
</div>
From Theorem 4, it is clear that $\\{v\_j\\}\_{j=1}^{\infty}$ is dense in $H\_k$, moreover, as $L$ is injective, we have $\inner{v\_i, v\_j}\_{H\_k} = \inner{LV\_i, LV\_j}\_{H\_k} = \inner{V\_i, V\_j}\_{\calH} = 0$. Therefore $v\_i\perp v\_j$, _i.e._ $\\{v\_j\\}\_{j=1}^{\infty}$ is a CONS in the RKHS $H\_k$.

Furthermore, [1] shows $T\_{H\_k}(f) = \sum\_{j=1}^{\infty} \inner{f,v\_j}\_{H\_k}V\_j$ is an isometry from $H\_k$ to $\calH$, i.e. $\norm{f}\_{H\_k} = \norm{T\_{H\_k}(f)}\_{\calH}$ regardless of the injectivity of $L$. This gives a nice correspondence between the RKHS and the Hilbert space for general linear operator $L$, however, this does depend on the choice of CONS, and it is not useful in analysing the smoothing property of the RKHS. We will see why and how the norm of RKHS induces smoothing condition on the space in the next post on Mercer's theorem, and the spectral perspective of RKHS via Hilbert-Schmidt Integral operator (which is defined irrespective of the choice of CONS).

<h2 class="section-heading">References</h2>
1. Saitoh, S and Sawano, Y. Theory of reproducing kernels and applications. Springer, 2016.
2. Hofmann T, Schölkopf B, Smola AJ. Kernel methods in machine learning. The annals of statistics. 2008 Jun 1:1171-220.
3. Stein, M. Interpolation of spatial data: some theory for kriging. Springer Science & Business Media, 2012.
4. Wendland, H. Scattered data approximation. Vol.17. Cambridge university press, 2004.
