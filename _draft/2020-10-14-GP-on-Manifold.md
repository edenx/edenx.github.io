---
layout:     post
title:      "Gaussian process on Manifold"
subtitle:   "In this post, we will extend the previous discussion on the connection between Elliptical operator and RKHS on Euclidean domain, to the stochastic PDE on compact Riemannian manifold. This turns out to be the natural way of defining general GP with a reproducing kernel that is derived from a PDE, however extendable to the cases where Spectral measure of the kernel is known. Examples for Matern class of kernels will be provided from Borovitskiy et al. 2020. "
date:       2020-10-14 20:00
author:     "edenx"
tags: 		[kernel, Lapalcian, PDE, GP]
category:   math
---
**A special thanks to Seth (!) who sent me this paper by Borovitskiy et al.[3], which is the main topic of discussion in this article.**

The motivation of reading on this topic, is closely connected to my interest in 'learning for structured data', in particular, learning functions for data supported on non-Euclidean domain, such as manifold and graphs. One of the reason being that a lot of practically important problems find data with some kind of underlying structure, which is probably more suitable to assume a locally Euclidean domain (smooth manifold); and of course graph structured data is also ubiquitous and of great interest in many fields of study. Besides, it's a relatively unexplored territory, which is exciting!

For someone with a spatial statistics background, it is kind of natural to find Gaussian Process (GP) as the first step in function learning on manifold, with its connection to SPDE and RKHS. Specifically, it is in fact a well motivated problem, with the pioneering work by Whittle on the discovery of Mat\'ern class of GP (which is used extensively in spatial statistics) being solutions to some SPDE driven by white noise [1]. It has resurfaced as the 'SPDE method' for krigging by Lindgren et al.[2] in the recent decades, and has been implemented in the INLA package, which is becoming increasingly popular in the applied studies with the element of spatial statistics, such as ecology, epidemiology, climate science etc. However, their implementation depends on solving SPDE with numerical methods (FEM), which is expensive, and sometimes difficult to make accurate approximation for certain hyperparameters.

The approach that Borovitskiy et al.[3] has taken to extend the SPDE method to compact Riemannian manifold without boundary, is by exploiting the spectral properties of Laplace-Beltrami operator, in a similar spirit that we have seen previously. In particular, they leverage the weight space view of GP [4] (or rather the eigen-decomposition of the kernel) to give a low-rank approximation of the covariance function/kernel. Additionally, it enables the exploitation of recent advancement in sparse GP by Hensman et al.[5] in the Riemannian manifold setting.

Our primary goal in this article is to construct an RKHS from an Elliptical SPDE driven by white noise on compact Riemannian manifold with no boundary. [Previously](2020-10-19-GP.md), we have seen the formal definition of regular generalised Gaussian field $\frakX$, and how its nuclear Integral operator $\calK$ identifies a RKHS for Gaussian random element $X$ such that $\frakX(f) = \inner{X, f}\_{\calH}$ on a separable Hilbert space $\calH$. Now, we first restrict our attention to $\calH = \calL^2(G)$ where $G\subset \R^d$, and the next thing to do is to construct a Gaussian white noise on such measurable space. Then we are fully ready to find the GP given by the solution to some SPDE on Euclidean domain. The generalisation to square integrable functions supported on compact Riemannian manifold (with no boundary) is straightforward, given the spectral properties of Laplace-Beltrami operator $\Delta\_{LB}$ as we will see later.

To motivate the following sections, we give two famous examples:

The Mat\'ern GPs [5] on $\calX = \R^d$ satisfies for $f:\calX\to\R$
<div>
$$
  \left(
    \frac{2\nu}{\kappa^2} - \Delta
    \right)^{\frac{\nu}{2} + \frac{d}{2}}f = \calW
$$
</div>
where we note the RHS is a (renormalised) Gaussian white noise, such that $\E[\calW(x)\calW(y)] = \delta\_y(x)$. Similarly, the solution $f:\calX\times \R^+\to \R$ to the following is also a GP with heat kernel as its covariance function (at any time point $t>0$),
<div>
$$
\left(
  \partder{}{t} - \Delta
  \right)f = \calW
$$
</div>
with some initial value function $f(\cdot, 0) = F(\cdot)$, where $\calW$ is a space time white noise, with $\E[\calW(t,x)\calW(s,y)] = \delta\_s(t)\delta\_y(x)$.

However, we will not muddle with time dependent random fields, and instead focus on the most basic Elliptical SPDE's, which can be viewed as variants of stochastic Helmholtz problems (such as the first example).

<!-- We will first give a brief introduction to GP with different perspectives, which is then followed by the general definition with the language of SPDE from [7]. We will draw intuitive analogy with what we have seen in the [previous post](2020-10-07-greens-function.md), and give example on the heat semigroup on Riemannian manifold. In the setting of compact Riemannian manifold without boundary (e.g. Torus, Sphere), it is actually quite similar to the Euclidean case, in the sense that the Laplace-Beltrami operator admits a Sturm-Liouville decomposition.

Certainly, this is not going to be a rigorous discussion of the SPDE on manifold, since there's a 500 pages book [10] just dedicated to the analysis of Heat kernel on manifold, and SPDE is not a subject that I am familiar with.  So instead, we will focus on building connections to what we have seen before, in an intuitive manner, with a focus on its applications. -->


<h2 class="section-heading">GP as solution to SPDE</h2>
In this section, we will look at the formal definition of Gaussian fields in the SPDE terminology [7]. But first, we review the spectral theory of Elliptical operators on compact Riemannian manifold.

<h3 class="section-heading">Spectral theory for Elliptical operator on compact Riemannian manifold</h3>

Let $(\calM, g)$ be a compact connected Riemannian manifold without boundary, where $g$ is the Riemannian metric that defines an inner product on the local tangent space $\calT_p\calM$ of the manifold $\calM$ at $p$. Let $\Delta_g$ denotes the Laplace-Beltrami operator defined on $\calL^2(\calM)$, which is the space of square integrable functions on $\calM$ w.r.t. Riemannian volume measure. Then the operator $-\Delta_g$ is self-adjoint and positive.

Under this setting, we will see that $-\Delta_g$ has spectral properties that are analogous to the Laplace operator under the setting of bounded domain in Euclidean space.

**Theorem 1 (Sturm-Liouville decomposition).**_Let $(\calM, g)$ be a compact Riemannian manifold without boundary, there exists an orthonormal basis $\\{\phi\_i\\}_{i\in\Z^+}$ of $\calL^2(\calM)$ such that $-\Delta\_g \phi_i = \lambda_i \phi_i$ with $0=\lambda_0 < \lambda_i \leq \dots\leq \lambda_i \to 0$ as $i\to \infty$. Moreover, $-\Delta_g$ admits the representation_
<div>
$$
  -\Delta_g f = \sum_{i=0}^{\infty} \lambda_i \inner{f, \phi_i}_{\calL^2}\phi_i
$$
</div>
_which converges unconditionally in $\calL^2(\calM)$._

This is analogous to the Dirichlet Laplace operator case, where the spectrum and eigenfunctions are given by the Resolvent operator defined by $(1+\Delta_g)^{-1}$, which is compact self-adjoint and positive. In addition, for any Borel function $\Phi:[0,+\infty)]\to\R$, the functional calculus allows for the decomposition of $\Phi(-\Delta_g)$ having the form
<div>
$$
  \Phi(-\Delta_g) = \sum_{i=0}^{\infty} \Phi(\lambda_i) \inner{f, \phi_i}_{\calL^2}\phi_i
$$
</div>

<h3 class="section-heading">GP as solution to SPDE</h3>


<h3 class="section-heading">Example: Heat semi-group on Riemannian manifold</h3>




<h2 class="section-heading">References</h2>

1. Whittle P. Stochastic-processes in several dimensions. Bulletin of the International Statistical Institute. 1963 Jan 1;40(2):974-94.
2. Lindgren F, Rue H, Lindström J. An explicit link between Gaussian fields and Gaussian Markov random fields: the stochastic partial differential equation approach. Journal of the Royal Statistical Society: Series B (Statistical Methodology). 2011 Sep;73(4):423-98.
3. Borovitskiy V, Terenin A, Mostowsky P, Deisenroth MP. Matern Gaussian processes on Riemannian manifolds. NeuRIPS 2020.
4. Rasmussen CE. Gaussian processes in machine learning. InSummer School on Machine Learning 2003 Feb 2 (pp. 63-71). Springer, Berlin, Heidelberg.
5. Hensman J, Durrande N, Solin A. Variational Fourier features for Gaussian processes. The Journal of Machine Learning Research. 2017 Jan 1;18(1):5537-88.
6. Dutordoir V, Durrande N, Hensman J. Sparse Gaussian Processes with Spherical Harmonic Features. ICML 2020.
7. Lototsky SV, Rozovsky BL. Stochastic partial differential equations. New York: Springer; 2017 Jul 6.
8. Bronstein MM, Bruna J, LeCun Y, Szlam A, Vandergheynst P. Geometric deep learning: going beyond euclidean data. IEEE Signal Processing Magazine. 2017 Jul 11;34(4):18-42.
10. Grigoryan A. Heat kernel and analysis on manifolds. American Mathematical Soc.; 2009.
