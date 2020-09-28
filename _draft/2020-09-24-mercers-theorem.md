---
layout:     post
title:      "Part 3: Mercer's theorem and the spectral perspective of RKHS"
subtitle:   "In this article, we provide another formulation of RKHS in terms of the spectrum of the Integral operator corresponding to the reproducing kernel, which is given by Mercer's Theorem and the property of Compact operators in Hilbert space."
date:       2020-09-24 22:00
author:     "edenx"
tags: 		[kernel]
category:   math
---

_**Disclaimer.** This post is served as a summarisation of my study notes on RKHS theory [1], and classes I took on relevant topics, containing theoratical details from [1, 2] along with my interpretations directed by my personal interests on those topics. I am by no means an expert in functional analysis and spetral theory, so please feel free to point out any mistakes in the post.
<br/><br/>_

In this article, we assume that $\calX$ is a locally compact Hausdorff space equipped with a positive Borel measure $\mu$. Moreover, let $\calL^2(\mu)$ be the seperable Hilbert space of real functions defined on $\calX$. We will mainly consider the spectral property of the integral operator for $k\in L^2(\calX\times\calX, \mu)$, which is defined as
$$
K(f)(x) = \int_{\calX} f(x)k(x,y)\;d\mu(x),\quad K: \calL^2(\calX) \to \calL^2(\calX)
$$
$K$ is a Hilbert-Schmidt integral operator (abbreviated as integral operator in the following) as will be seen in Section 2. For completeness, we first present a brief intro to the spectral theory of compact self-adjoint operator in Hilbert space. Then we show that the spectral theory is also applicable to the integral operator $K$ in our case. Finally, we will see how Mercer's theorem bridges spectral theory and RKHS, and finally its implication in ML.

<h2 class="section-heading">Spectral theorem in Hilbert space</h2>

## spectral theorem for compact operator in Hilbert space is a direct extension of spectral theory for square matrices (wiki)

**Definition 1 (Compact operator).**_Let $\calH$ be a Hilbert space and $L(\calH)$ be the set of bounded operators on $\calH$, i.e. for any $T\in L(\calH),\; T:\calH\to\calH$, its induced operator norm is finite. Then, $T$ is compact if the image of each bounded set under $T$ is relatively compact (its closure is compact)._

**Definition 2 (Self-adjoint operator).**_A bounded operator $T$ as in Definition 1 is called self-adjoint if $A^{\ast} = A$, where $A^{\ast$ is the adjoint of $A$._

<!-- Spectral theorem for compact self-adjoint in Hilbert space -->
**Theorem 1 (Thm 6.27, M.Einsiedler 2017).**_Let $\calH$ be a seperable Hilbert space, and $T$ a compact self-adjoint operator on $\calH$. Then there exists a sequence of real eigenvalues $\\{\lambda_n\\}_n$ with $\abs{\lambda_n}\to 0$ as $n\to\infty$; and an orthonormal basis $\\{v_n\\}_n$ of eigenvectors with $A v_n = \lambda_n v_n\; \forall n\geq 1$._

It follows directly that such $T$ is diagonalisable, and each non-zero eigenvalue has finite-multiplicity. 

<h2 class="section-heading">Mercer expansion of integral operator</h2>

We first show the integral operator $K$ defined in the beginning is indeed Hilbert-Schmidt. Recall that an operator $T$ on a seperable Hilbert space is HS if for any CONS $\\{\psi_i\\}_{i=1}^{\infty}$, 
$$
\norm{T}_{HS}^2 = \sum_{i=1}^{\infty}\norm{T\psi_i}^2 < \infty.
$$
Therefore, by Parseval's identity we have $k(x,\cdot) = \sum_i \inner{k(x,\cdot), \psi_i}_{\calL^2} \psi_i$, then
\begin{equation*}
\begin{align}
\int \abs{k(x,y)}^2 \;dy 
&= \inner{k(x, \cdot), k(x, \cdot)}_{\calL^2}\\
&= \sum_{i=1}^{\infty}\abs{\inner{k(x,\cdot), \psi_i}_{\calL^2}}^2 \\
&=\sum_{i=1} \abs{\int k(x,y)\psi_i(y) \;dy}^2\\
&=\sum_{i=1} \abs{K(\psi_i)(x)},
\end{align}
\end{equation*}
integrate w.r.t $x$ gives
$$
\int\int \abs{k(x,y)}^2 \;dydx  = \sum_i \norm{K\psi_i}_{\calL^2}^2 = \norm{K}_{HS}^2.
$$
Since $k\in \calL^2(\calX\times\calX, \mu)$, the term on the RHS is bounded. Then we complete the proof. Interestinhly, for any HS operator $T$ on seperable $\calL^2(\calX, \mu)$, there is a square integrable function $k_T\in \calL^2(\calX\times\calX, \mu)$ such that $T$ can be written in the form as $K$ [4]. Furthermore, we will see that the HS-integral operator is compact and self-adjoint.

**Proposition 1 (Hilbert-Schmidt, M.Einsiedler 2017).**_Let $(\calX, \calB_{\calX}, \mu)$, $(\calY, \calB_{\calY}, \nu)$ be $\sigma$-finite measure spaces. Let $k\in \calL^2(\calX \times\calY, \mu\times\nv)$. Then the Hilbert-Schmidt integral operator $K:\calL^2(\calX, \mu)\to \calL^2(\calY, \nu)$ defined by 
$$
K(f)(y) = \int_{\calX} f(x)k(x,y)\;d\mu(x)
$$
for $\nu$-almost everywhere $y\in\calY$ defines a compact operator._

In addition, $K$ in Proposition 1 is also continuous thus bounded [3], and it is self-adjoint as long as $k(x,y) = k(y,x)$. Clearly, Proposition 1 applies to our integral operator $K\in L^2(\calX\times\calX, \mu)$; with the assumption that $\calL^2$ is a seperable Hilbert space, $K$ admits a set of non-zero eigenvalues $\\{\lambda_j\\}_j$ and eigenvectors $\\{\phi_j\\}_j$. Moreover, by the property of Hilbert-Schmidt operator, we have that $K = \sum_{i}\lambda_i (\phi_i \otimes \phi_i)$, which can be seen as a generalisation to eigen-decomposition [4].

We will see that for positive definite quadratic form (condition 2 in Theorem 2), operator $K$ has positive eigenvalues. We present here a modification of Mercer's theorem in [1] to accommodate the setting given in the beginning, however, it can be shown to apply to a more general scenario.

**Theorem 2 (Mercer's theorem, S.Saitoh 2016).**_For $\mu$ and $\calX$ defined previously, assume $k$ satisfies the following assumptions:
1. $k(x,y) = k(y,x)\;\forall x,y\in\supp{\mu}$;
2. \int\int_{\calX\times\calX} k(x,y)f(x)f(y)\;d\mu(y) \geq 0, \;\forall f\in\calL^2(\calX, \mu).
Then $K$ admits a set of positive eigenvalues and corresponding orthonomorl eigenfunctions, where $K = \sum_{i}\lambda_i (\phi_i \otimes \phi_i)$, where the convergence is absolute and uniform on $\supp{\mu\times\mu}$._

Since condition 2 is equivalent to the definition of positive definite quadratic form, Mercer's theorem is generally applicable to all reproducing kernels in Part 1.

<h2 class="section-heading">Construction of RKHS from a spectral perspective</h2>

Finally, as a consequence of Theorem 2, we present the explicit expression of RKHS using the eigendecomposition of the integral operator (which clearly is a CONS). 

**Theorem 3 (Thm 18, K.Fukumizu 2010).**_Under the same notation, we have a RKHS with $k$ s.t.
**
H_k = \\{f\in\calL^2(\calX, \mu): 
f = \sum_i^{\infty} a_i \phi_i, \; 
\norm{f}_{H_k}^2 = \sum_i^{\infty} \frac{\abs{a_i}^2}{\lambda_i}<\infty\\},
**
and that the inner product of RKHS is of the form
$$
\inner{f, g}_{H_k} = \sum_i^{\infty} \frac{a_i b_i}{\lambda_i}
$$
where $f = \sum_i^{\infty} a_i \phi_i, \, g = \sum_i^{\infty} b_i \phi_i$, and $a_i, b_i = 0$ for $\lambda_i=0$._

Note that $k(x,x) = \sum_i^{\infty}\lambda_i \phi_i(x)^2<\infty$ by Mercer's theorem, so that $k(x,\cdot) = \sum_i^{\infty} \lambda_i \phi_i(x)\phi_i(\cdot) \in H_k$. The reproducing property follows directly:
$$
\inner{f, k(x,\cdot)}_{H_k} = \sum_i^{\infty} \frac{\lambda_i^2 \phi_i(x)}{\lambda_i} = f(x).
$$
We end with a remark on the implications of this expression of RKHS.
**Remark 1.**_ We can observe that dividing each element of $\ell^2$ inner product by $\lambda_i$ gives $\inner{\cdot, \cdot}_{H_k}$. This in effect imposes a smoothness condition on $H_k$, in the sense that for $f = \sum_i^{\infty} a_i \phi_i$ to be in $H_k$, $a_i$ must go to zero fast enough so that $\norm{f}_{H_k} = \sum_i^{\infty} a_i^2/\lambda_i <\infty$._

<h2 class="section-heading">References</h2>

1. Saburou Saitoh and Yoshihiro Sawano. Theory of reproducing kernels and applications. Springer, 2016.
2. Einsiedler, Manfred, and Thomas Ward. Functional analysis, spectral theory, and applications. Vol. 276. Springer, 2017.
3. Wikipedia contributors. "Hilbert–Schmidt integral operator." Wikipedia, The Free Encyclopedia. Wikipedia, The Free Encyclopedia, 19 Apr. 2020. Web. 25 Sep. 2020.
4. Fukumizu
5. M.Jordan