---
layout:     post
title:      "Green's function, RKHS and Regularisation"
subtitle:   "With the spectral perspective of RKHS introduced previously, we now look at a special and important category of reproducing kernels, which is the Green's functions to positive systems of differential equations. We will have examples on the eigenvalue problem for Dirichlet Laplace operator; and also on the Heat equation in Euclidean space. An intuitive generalisation is then provided. Finally, we will discuss informally the extension to discrete differential system and RKHS defined by Hermitian matrices."
date:       2020-10-07 20:00
author:     "edenx"
tags: 		[kernel, Lapalcian, PDE]
category:   math
---
_There's actually something that I need to fix, so take those concepts with caution_
<br/><br/>

Before the main content, just for my interest in graphs and Laplace operators (which has nice properties and wide applications owing to its representation of second order information and its spectral properties), here's a blog ['Why Laplacian?'](https://donskerclass.github.io/post/why-laplacians/) written by Prof David Childers at CMU Economics on some applications of Laplacians and their interpretations in each context. One of the purpose of this article is to provide with another manifestation of Laplacian's usefulness in function smoothing, in terms of its use in regularisation and RKHS constructed by it.

<h2 class="section-heading">Spectral properties of Laplace operator, and its connection to RKHS</h2>

The aim of this section is to provide with some solid examples on the connections between RKHS and Elliptical operators. Although the results can be extended to more complex geometry, we only focus on the Euclidean space $\R^d$ for simplicity.

We first give an overview of the spectral property of Dirichlet Laplace operator in Euclidean space, and how it allows the construction of a RKHS. Then, we will take a look at the heat equation on Euclidean space (as a special example of compact Riemannian manifold), which induces the famous Diffusion semi-group that has been a topic of great interest in Harmonic analysis and Manifold learning.

Finally, some intuitive introduction to the general theory that connects the Green's functions of differential systems to reproducing kernels is presented.

<h3 class="section-heading">Example: Eigenvalue problem of Laplace operator in Euclidean space</h3>

Let us consider the Laplace operator $\Delta\_D:\calL^2(\Omega)\to \calL^2(\Omega)$ on the Hilbert space $\calL^2(\Omega)$, where $\Omega\subset\R^d$ is a bounded domain with Dirichlet boundary condition, i.e. $\forall f \in \calL^2(\Omega), \;f=0$ on $\partial \Omega$. We may call $\Delta\_D$ as Dirichlet Laplace operator. Now, we have the eigenvalue problem of $\Delta\_D$ as followed
<div>
$$
  \begin{align}
    -\Delta_D  f = \lambda f
    \label{Eq:eigenproblem}
  \end{align}
$$
</div>
In this case, the solution to this problem is given by the eigen-system of the resolvent $(\Delta\_D+ I)^{-1} := \calR : \calL^2(\Omega) \to \calL^2(\Omega)$. It is notable that $\calR$ is compact, self-adjoint and positive. Recall from [Part 3](2020-09-28-mercers-theorem.md), we know such an operator admits a countable set of positive eigenvalues $\\{\lambda\_i\\}\_i$ with finite multiplicity that goes to 0 as $i\to\infty$; in addition, its eigenfunctions $\\{\phi\_i\\}\_i$ forms a CONS for $\calL^2(\Omega)$. Therefore, by the spectral property of compact self-adjoint operators,
<div>
$$
  \calR = \sum_i \lambda_i (\phi_i \otimes \phi_i).
$$  
</div>

**Remark.** _It is easy to see that $\\{\phi\_i\\}\_i$ and $\\{\mu_i\\}\_i=\\{1/\lambda\_i-1\\}\_i$ gives the Sturm-Liouville decomposition of $\Delta\_D$, where $0<\mu\_i\to\infty$ as $i\to \infty$._

In fact, $\calR$ is an Integral operator with the Green's function $G(x,x')$ to the system in \eqref{Eq:eigenproblem}, such that
<div>
$$
  \begin{align*}
    (\Delta_D + I) G(x,x') &= \delta(x-x')\\
    \calR f(x') &= \int G(x,x')f(x) dx,
  \end{align*}
$$
</div>
where $\delta$ is the distribution function (Dirac delta), and $G$ admits the expansion $G(x,x')=\sum\_i \lambda\_i \phi\_i(x)\phi\_i(x')$.

Naturally, we can define a RKHS via $\\{\phi\_i\\}\_i$ and $\\{\lambda\_i\\}\_i$ as in Part 3, where
<div>
$$
  H_{\Delta} = \left\{f\in\calL^2(\Omega):
  f = \sum_i^{\infty} a_i \phi_i, \;
  \left(\frac{\abs{a_i}^2}{\lambda_i}\right)\in\ell^2\right\}
$$
</div>
with inner product as $\inner{f,g}\_{H\_{\Delta}} = \sum\_i^{\infty} \frac{a\_i b\_i}{\lambda\_i}$.

<h3 class="section-heading">Example: Heat equation in Euclidean space</h3>

Another well known example is the Heat equation on a bounded domain $\Omega\subset\R^d$ with Dirichlet boundary condition, where $f:\Omega\times\Omega\times\R^+ \to \R$, then
<div>
  $$
  \begin{align}
    \partder{f}{t} = -\Delta_D f,\;\;\; f(\cdot,0) = F(\cdot)
    \label{Eq:heat}
  \end{align}
  $$
</div>
for $F$ the initial value function.
Further, we can show that a unique smooth quadratic form $p: \Omega\times\Omega\times\R^+ \to\R$ exists s.t.
<div>
$$
  \begin{align}
  \label{Eq:propagator}
  e^{-t\Delta_D}f = \int_{\Omega} p(\cdot, y, t)f(y)\;dy
  \end{align}
$$
</div>
for any $f\in\calL^2(\Omega)$. Then $p$ satisfies the followings for $t>0$,

1. $p(x,x',t) = p(x',x,t) > 0$;
2. $\lim\_{t\to 0}p(x,x',t) = \delta_(x-x')$;
3. $\partder{p}{t} + \Delta_D p = 0$, since $\partder{}{t}e^{-t\Delta_D}f = -\Delta_D e^{-t\Delta_D}f$;
4. Lastly, by setting the intial value function as $F(\cdot) = p(\cdot, x',s)$, it gives that
<div>
$$
  p(x,x',t+s) = \int_{\Omega} p(x,x'',t)p(x'', x',s)\;dx''
  \;\;\; t,s>0, x,x'\in\Omega.
$$
</div>
The unique smooth function $p$ is called the fundamental solution to the heat equation in \eqref{Eq:heat}, also known as the heat kernel; and $e^{-t\Delta_D}:\calL^2(\Omega)\to \calL^2(\Omega)$ is called the heat propagator \eqref{Eq:propagator} [9]. Note that in this case the Green's function to \eqref{Eq:heat} is $p$ with initial value function $F$ as $\delta\_x$.

In addition, it can be shown that the Integral operator  $e^{-t\Delta_D}$ is self-adjoint, compact and positive [9]. So $p$ is the reproducing kernel for $e^{-t\Delta_D}$. Indeed, from the spectral property of $\Delta_D$ and [holomorphic functional calculus](https://en.wikipedia.org/wiki/Holomorphic_functional_calculus), we obtain the following expression
<div>
$$
  e^{-t\Delta_D} = \sum_i e^{-t\mu_i} \phi_i\otimes \phi_i
$$
</div>
with $p(x,x',t) = \sum\_i e^{-t\mu\_i}\phi\_i(x) \phi\_i(x')$, for $\\{\mu\\}\_i$ the eigenvalues and $\\{\phi\_i\\}\_i$ the eigenfunctions of $\Delta$, which consequently forms the Sturm-Liouville decomposition of $\calL^2(\Omega)$. Complete proof can be found in [9].

**Remark.**_In fact, the above result holds for any compact Riemannian manifold [9]._

<h3 class="section-heading">Intuitive introduction to the general case</h3>

Following the two differential system as inspirational examples, it is pointed out in [1] that in the case of a self-adjoint elliptic problem, the Green's function exists if the problem is well-posed (i.e. 0 is not an eigenvalue of the corresponding eigenvalue problem); a Green's function exists and is a reproducing kernel if and only if the problem is positive definite (i.e. all the eigenvalues are positive). From the statement of Mercer's theorem, it is intuitive to think of why this is the case.

Notably, this applies to the differential system defined for domains in Euclidean space with $\Delta\_D$ and also relatively compact domains in differential Manifold with Laplace-Beltrami operator $\Delta\_{LB}$.

In [10], the general case is presented without an involved background. Consider a bounded regular domain $D$ whose boundary consists of a finite number of analytic Jordan curves. Suppose $G(x,x')$ is the solution for some linear differential operator $L$ on some function space defined on $D$ that satisfies the following
<div>
$$
  \begin{align}
  LG(x,x') = \delta_x(x')
  \label{Eq:greens}
  \end{align}
$$
</div>
where $\delta\_x(x')$ is the dirac delta function as seen before. In fact, $G$ is called the fundamental solution for $L$ if it only depends on $|x-x'|$; and is called Green's function for the differential system defined by $L$ and some boundary conditions when such boundary conditions are satisfied.

In fact, for the self-adjoint operator $L^{\ast}L$ and its Green's function $G(x,x')$ satisfying \eqref{Eq:greens}, we obtain the representation
<div>
$$
  f(x') = \int_D f(x)L^{\ast}L G(x,x')\;dx
$$
</div>
and by Stoke's formula,
<div>
$$
  f(x') = \int_D Lf(x)L G(x,x')\;dx + \text{some boundary integrals}
$$
</div>
the additional term becomes zero with e.g. Dirichlet boundary condition or no boundaries. It is notable that this defines an Integral operator with $G$ as the kernel. Subsequently, we can define a Hilbert space $\calH$ such that the norm is given by
<div>
$$
\norm{f}_{\calH} = \int_D |Lf(x)|^2 \;dx.
$$
</div>
The operator $L$ is also called the regularisation operator in [3,4,5].

<h2 class="section-heading">Extension to discrete Green's functions</h2>

One natural extension of the above discussion is to discrete differential systems, e.g. combinatorial games, diffusion process on graph etc., which are important problems in combinatorics.

Assume $V$ is the set of vertices of a graph $\calG$. The discrete Laplace operator (or the Random walk Laplacian) can be defined as $L\_{rw} = I-D^{-1}W$, such that $W$ is the weight matrix and $(D\_{ii}) = (\sum\_j W\_{ij})$ is the degree matrix of $W$. In particular, for $f:V\to\R$,
<div>
$$
  \inner{f, L_{rw}f} = \sum_{i\sim j} (f(i) - f(j))^2 \frac{w_{i,j}}{D_{ii}}.
$$
</div>
where $x\sim y$ denotes that $x$ is in the neighborhood of $y$ and vice versa.
It is notable that such definition of $L\_{rw}$ is not self-adjoint (Hermitian), since it is not symmetric to begin with. However, it is in fact equivalent to a self-adjoint counterpart, which is the normalised Laplacian
<div>
$$
  L_{norm} = D^{1/2}L_{rw}D^{-1/2} = I - D^{-1/2}WD^{-1/2}
$$
</div>
Then, the Green's function for a differential system with the normalised Laplacian is defined as
<div>
$$
  G L_{norm} = I
$$
</div>
where identity is on the RHS.

In the discrete case, we are able to find eigenvalues $\\{\mu\_i\\}\_i$ of $L\_{norm}$ with power iteration alogorithm, where we assume $\calG$ is connected (this condition can be relaxed by taking a connected subgraph of $\calG$). Then, we obtain formula for the Green's function $G$ analogous to the continuous case, where
<div>
$$
  G(x,y) = \sum_i \frac{1}{\lambda_i}\phi_i(x)\phi_i(y)\;\;\; x,y\in V
$$
</div>
 For more detailed discussions on discrete differential system, [7] is a very good reference.

**Remark.** _We have seen in Part 3 that the compact self-adjoint positive operator $\calT$ is the infinite dimensional counterpart to the strictly positive definite Hermitian matrix $A$, which forms a valid RKHS. One intuitive way to see why it works is by considering the inner product defined by $\inner{v, w}\_A = \inner{Av, w}$ on $\R^d$ for $v, w\in \R^d$._

 It is also noted that, by the holomorphic functional calculus (or more generally the Borel one), we are able to find the eigenvalues and eigenfunctions/vectors of $r(\Delta)$ or $r(L\_{norm})$, such that $r$ is a holomorphic (Borel) function, e.g. polynomials and inverse functions (resolvent). [4] gives many kernels on graphs constructed in this way.

<h2 class="section-heading">References</h2>

1. Nachman Aronszajn and Kennan Taylor Smith. Characterization of positive reproducing kernels.applications to green’s functions. American Journal of Mathematics, 79(3):611–622, 1957.
2. De Vito E, Mücke N, Rosasco L. Reproducing kernel Hilbert spaces on manifolds: Sobolev and Diffusion spaces. arXiv preprint. arXiv:1905.10913. 2019.
3. Alex J Smola, Bernhard Schölkopf, and Klaus-Robert Müller. The connection between regularization operators and support vector kernels.Neural networks, 11(4):637–649, 1998.
4. Alexander J Smola and Risi Kondor. Kernels and regularization on graphs. In Learning theory and kernel machines, pages 144–158. Springer, 2003.
5. Belkin M, Niyogi P, Sindhwani V. Manifold regularization: A geometric framework for learning from labeled and unlabeled examples. Journal of machine learning research. 2006;7(Nov):2399-434.
6. Borovitskiy V, Terenin A, Mostowsky P, Deisenroth MP. Matern Gaussian processes on Riemannian manifolds. arXiv preprint arXiv:2006.10160. 2020 Jun 17.
7. Chung F, Yau ST. Discrete Green's functions. Journal of Combinatorial Theory, Series A. 2000 Jul 1;91(1-2):191-214.
8. De Vito E, Mücke N, Rosasco L. Reproducing kernel Hilbert spaces on manifolds: Sobolev and Diffusion spaces. arXiv preprint arXiv:1905.10913. 2019 May 27.
9. Canzani Y. Analysis on manifolds via the Laplacian. [Lecture Notes](http://www.math.harvard.edu/canzani/docs/Laplacian.pdf). 2013.
10. Saitoh, S and Sawano, Y. Theory of reproducing kernels and applications. Springer, 2016.
