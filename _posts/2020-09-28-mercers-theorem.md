---
layout:     post
title:      "Part 3: Mercer's theorem and the spectral perspective of RKHS"
subtitle:   "In this article, we provide another formulation of RKHS in terms of the spectrum of the Integral operator corresponding to a reproducing kernel, which is given by Mercer's Theorem and the property of Compact operators in separable Hilbert space."
date:       2020-09-28 16:40
author:     "edenx"
tags: 		  [kernel, fundamentals of RKHS]
category:   math
---

_**Disclaimer.** This post is served as a summarisation of my study notes on RKHS theory [1], and classes I took on relevant topics, containing theoratical details from [1, 2, 3] along with my interpretations directed by my personal interests on those topics. I am by no means an expert in functional analysis and spectral theory, so please feel free to point out any mistakes in the post.
<br/><br/>_

In this article, we assume that $\calX$ is a locally compact Hausdorff space equipped with a positive Borel measure $\mu$. Moreover, let $\calL^2(\mu)$ be the separable Hilbert space of real functions defined on $\calX$. We will mainly consider the spectral property of the integral operator for $k\in L^2(\calX\times\calX, \mu)$, which is defined as
<div>
$$
\begin{align}
  K(f)(x) = \int_{\calX} f(x)k(x,y)\;d\mu(x),\quad K: \calL^2(\calX) \to \calL^2(\calX),\label{Eq:HSIO}
\end{align}
$$
</div>
where $K$ is a Hilbert-Schmidt integral operator (abbreviated as integral operator in the following) as will be seen in Section 2. For completeness, we first present a brief introduction to the spectral theory of compact self-adjoint operator on Hilbert space. Then we show that the spectral theory is also applicable to the integral operator $K$ in our case. In the end, we will see how Mercer's theorem bridges spectral theory and RKHS, and finally its implication in ML.

<h2 class="section-heading">Spectral theorem in Hilbert space</h2>

The spectral theorem for finite dimensional Hermitian matrices (over $\R$) are of particular interest in Linear algebra, since its eigenvectors provide with an orthogonal basis, so that the linear map is diagonalisable. Compact operators in Hilbert space consisting of real functions may be viewed as an extension from the finite dimensional case for its spectral properties. We will see in this section, how we may obtain a CONS from a compact operator in $\calH$.

In the article, we use $\calH$ to denote separable Hilbert space if without specification; and we use 'linear operator' and 'linear map' interchangeably. The theory can be easily extended to spaces of complex-valued functions, but we here only present the results with real-valued functions for simplicity.

**Definition 4 (Compact operator).** _Let $\calH$ be a Hilbert space and $L(\calH)$ be the set of bounded operators on $\calH$, i.e. for any $T\in L(\calH),\; T:\calH\to\calH$, its induced operator norm is finite. Then, $T$ is compact if the image of each bounded set under $T$ is relatively compact (its closure is compact)._

**Definition 5 (Self-adjoint operator).** _A bounded operator $T$ as in Definition 4 is called self-adjoint if $A^{\ast} = A$, where $A^{\ast}$ is the adjoint of $A$._

Now, we are ready to present the spectral theorem for compact operators in separable Hilbert space $\calH$.

**Theorem 5 (Thm 6.27, M.Einsiedler 2017).** _Let $\calH$ be a separable Hilbert space, and $T$ a compact self-adjoint operator on $\calH$. Then there exists a sequence of real eigenvalues $\\{\lambda\_n\\}\_n$ with $\abs{\lambda\_n}\to 0$ as $n\to\infty$; and an orthonormal basis $\\{v\_n\\}\_n$ of eigenvectors with $A v\_n = \lambda\_n v\_n\; \forall n\geq 1$._

It follows directly that such $T$ is diagonalisable, and each non-zero eigenvalue has finite-multiplicity. In Section 2, we will see that an integral operator $K$ defined in \eqref{Eq:HSIO} is indeed compact.

<h2 class="section-heading">Mercer expansion of integral operator</h2>
We first show the $K$ is Hilbert-Schmidt (HS).

**Lemma 1.** _Operator $K$ defined in \eqref{Eq:HSIO} is Hilbert-Schmidt._
_Proof._
Recall that an operator $T$ on a separable Hilbert space is HS if for any Complete orthogonal system (CONS) $\\{\psi\_i\\}\_{i=1}^{\infty}$, we have the following
<div>
$$
  \norm{T}_{HS}^2 = \sum_{i=1}^{\infty}\norm{T\psi_i}^2 < \infty.
$$
</div>
Therefore, by Parseval's identity we have $k(x,\cdot) = \sum\_i \inner{k(x,\cdot), \psi\_i}\_{\calL^2} \psi\_i$, then
<div>
$$
  \begin{align*}
    \int \abs{k(x,y)}^2 \;dy
    &= \inner{k(x, \cdot), k(x, \cdot)}_{\calL^2}\\
    &= \sum_{i=1}^{\infty}\abs{\inner{k(x,\cdot), \psi_i}_{\calL^2}}^2 \\
    &=\sum_{i=1} \abs{\int k(x,y)\psi_i(y) \;dy}^2\\
    &=\sum_{i=1} \abs{K(\psi_i)(x)},
  \end{align*}
$$
</div>
then integrate w.r.t $x$ gives
<div>
$$
  \int\int \abs{k(x,y)}^2 \;dydx  = \sum_i \norm{K\psi_i}_{\calL^2}^2 = \norm{K}_{HS}^2.
$$
</div>
Since $k\in \calL^2(\calX\times\calX, \mu)$, the term on the RHS is bounded. Then we complete the proof.
<div style="text-align: right"> $\square$ </div>
**Remark.** _Interestingly, for any HS operator $T$ on separable $\calL^2(\calX, \mu)$, there is a square integrable function $k\_T\in \calL^2(\calX\times\calX, \mu)$ such that $T$ can be written in the form of \eqref{Eq:HSIO} [4]._

**Remark.** _We have seen in [Part 2](2020-09-24-hilbert-basis.md) that an RKHS can be characterised with any CONS of the separable Hilbert space $\calH$, however it is dependent on the choice for the basis. On the other hand, the norm of HS integral operator $K$ is specified irrespective of the CONS._
_Proof (informal)._
Consider any HS operator $T$ on $\calH$ with two sets of CONS $\\{\psi\_i\\}\_{i=1}^{\infty}$ and $\\{\varphi\_i\\}\_{i=1}^{\infty}$, then_
<div>
$$
\begin{align*}
  \norm{T}_{HS}
  &=\sum_{i=1}^{\infty}\norm{T\psi_i}_{\calH}^2
  = \sum_{i,j=1}^{\infty}\abs{\inner{\varphi_i, T\psi_i}_{\calH}}^2\\
  &= \sum_{i,j=1}^{\infty}
  \abs{\inner{T^{\ast}\varphi_j, \psi_i}_{\calH}}^2
  = \sum_{j=1}^{\infty} \norm{T^{\ast}\varphi_j}_{\calH}^2,
\end{align*}
$$
</div>
_where the second equality is due to $T\psi\_i = \sum\_{j=1}^{\infty} \inner{T\psi\_i, \varphi\_j}\_{\calH}\varphi\_j$._
<div style="text-align: right"> $\square$ </div>
Furthermore, the following Proposition gives that the HS-integral operator is compact and self-adjoint.

**Proposition 1 (Hilbert-Schmidt, M.Einsiedler 2017).** _Let $(\calX, \calB\_{\calX}, \mu)$, $(\calY, \calB\_{\calY}, \nu)$ be $\sigma$-finite measure spaces. Let $k\in \calL^2(\calX \times\calY, \mu\times\nu)$. Then the HS integral operator $T\_k:\calL^2(\calX, \mu)\to \calL^2(\calY, \nu)$ defined by_
<div>
$$
  T_k(f)(y) = \int_{\calX} f(x)k(x,y)\;d\mu(x)
$$
</div>
_for $\nu$-almost everywhere $y\in\calY$ defines a compact operator._

In addition, $T\_k$ in Proposition 1 is also continuous thus bounded [3], and it is self-adjoint as long as $k(x,y) = k(y,x)$ (which is automatically satisfied if $k$ is a real-valued PSD kernel). Clearly, Proposition 1 applies to our integral operator $K\in L^2(\calX\times\calX, \mu)$; with the assumption that $\calL^2$ is a separable Hilbert space, $K$ admits a set of non-zero eigenvalues $\\{\lambda\_j\\}\_j$ and eigenvectors $\\{\phi\_j\\}\_j$. Moreover, by the property of HS operator, we have that $K = \sum\_{i}\lambda\_i (\phi\_i \otimes \phi\_i)$, which can be seen as a generalisation to eigen-decomposition for Hermitian matrices [3].

Finally, Theorem 6 says that for positive definite quadratic form (condition 2 in Theorem 6), operator $K$ has positive eigenvalues. We present here a modification of Mercer's theorem in [1] to accommodate the setting given in the beginning, however, it can be shown to apply to a more general scenario.

**Theorem 6 (Mercer's theorem, S.Saitoh 2016).** _For $\mu$ and $\calX$ defined previously, assume $k$ satisfies the following assumptions:_
1. _$k(x,y) = k(y,x)\;\forall x,y\in\supp{\mu}$;_
2. $\int\int\_{\calX\times\calX} k(x,y)f(x)f(y)\;d\mu(y) \geq 0, \;\forall f\in\calL^2(\calX, \mu).$

_Then $K$ admits a set of positive eigenvalues and corresponding orthonomorl eigenfunctions, where $K = \sum\_{i}\lambda\_i (\phi\_i \otimes \phi\_i)$, where the convergence is absolute and uniform on $\supp{\mu\times\mu}$._

Since condition 2 is equivalent to the definition of positive definite quadratic form, Mercer's theorem is generally applicable to all reproducing kernels in [Part 1](2020-09-22-construction-of-RKHS.md).

<h2 class="section-heading">Construction of RKHS from a spectral perspective</h2>

Finally, as a consequence of Theorem 6, we present the explicit expression of RKHS using the eigen-decomposition of the HS integral operator (which clearly is a CONS according to Theorem 5).

**Theorem 7 (Thm 18, K.Fukumizu 2010).** _Under the same notation, we have a RKHS with $k$ s.t._
<div>
$$
  H_k = \{f\in\calL^2(\calX, \mu):
  f = \sum_i^{\infty} a_i \phi_i, \;
  \norm{f}_{H_k}^2 = \sum_i^{\infty} \frac{\abs{a_i}^2}{\lambda_i}<\infty\},
$$
</div>
_and the inner product of RKHS is of the form_
<div>
$$
  \inner{f, g}_{H_k} = \sum_i^{\infty} \frac{a_i b_i}{\lambda_i}
$$
</div>
_where $f = \sum\_i^{\infty} a\_i \phi\_i, \, g = \sum\_i^{\infty} b\_i \phi\_i$, and $a\_i, b\_i = 0$ for $\lambda\_i=0$._

Notably, it show that $k(x,x) = \sum\_i^{\infty}\lambda\_i \phi\_i(x)^2<\infty$ by Mercer's theorem, hence $k(x,\cdot) = \sum\_i^{\infty} \lambda\_i \phi\_i(x)\phi\_i(\cdot) \in H\_k$. Now, the reproducing property follows directly:
<div>
$$
  \inner{f, k(x,\cdot)}_{H_k} = \sum_i^{\infty} \frac{\lambda_i^2 \phi_i(x)}{\lambda_i} = f(x).
$$
</div>
Finally, we end the article with a remark on the implication of this expression of RKHS [4].

**Remark.** _We can observe that dividing each element of $\ell^2$ inner product by $\lambda\_i$ gives $\inner{\cdot, \cdot}\_{H\_k}$. This in effect imposes a smoothness condition on $H\_k$, in the sense that for $f = \sum\_i^{\infty} a\_i \phi\_i$ to be in $H\_k$, $a\_i$ must go to zero fast enough so that $\norm{f}\_{H\_k} = \sum\_i^{\infty} a\_i^2/\lambda\_i <\infty$._

<h2 class="section-heading">References</h2>

1. Saitoh, S and Sawano, Y. Theory of reproducing kernels and applications. Springer, 2016.
2. Einsiedler, M, and Ward, T. Functional analysis, spectral theory, and applications. Vol. 276. Springer, 2017.
3. Fukumizu, K. Kernel Method: Data Analysis with Positive Definite Kernels, [Lecture 5](http://stat.sys.i.kyoto-u.ac.jp/titech/class/fukumizu/Kernel_theory_5.pdf). Tokyo Institute of Technology, 2010.
4. Jordan, M. Stat241B: Advanced Topics in Learning & Decision Making, [Reproducing kernel Hilbert spaces I](https://people.eecs.berkeley.edu/~jordan/courses/281B-spring04/lectures/rkhs.pdf). University of California Berkeley, 2004.
