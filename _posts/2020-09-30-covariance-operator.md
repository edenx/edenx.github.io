---
layout:     post
title:      "Part 4: Covariance operator for reproducing kernels"
subtitle:   "Another important operator defined on a RKHS is Covariance operator, which is essential for doing kernel PCA, kernel CCA, and independence testing etc. We will see that under certain conditions, the centered Covariance operator is Hilbert-Schmidt, moreover, sharing the same spectrum as the HS Integral operator introduced in Part 3."
date:       2020-09-30 15:40
author:     "Eden"
tags: 		  [kernel, fundamentals of RKHS]
category:   math
---

_**Disclaimer.** This post is served as a summarisation of my study notes on RKHS theory [1], and classes I took on relevant topics, containing theoratical details from [1, 3] along with my interpretations directed by my personal interests on those topics. I am by no means an expert in functional analysis and spectral theory, so please feel free to point out any mistakes in the post.
<br/><br/>_

For the last post of the fundamentals of RKHS, we will take a look at the Covariance operator, which we will show is a HS operator on the RKHS. It serves as an important and widely-applicable tool for data analysis, e.g. for feature selections using KPCA, KCCA, or by independence testing with COCO or HSIC etc. (Interested reader may be referred to [3].) Furthermore, it also plays an important role in the analysis of spectral/regularised algorithm, in determining the optimal non-asymptotic rate of convergence [2]. We will probably see more of this in the future post.

In this article, we assume $\calX$ is a Metric spaces, and let $(\calX, \Omega\_{\calX}, \P)$ be a probability space. Then, we denote $X$ as a random variable supported on $\calX$. In addition, assume $\calL^2(\calX, \P) = \calL^2(\P)$ a separable Hilbert space. Then we denote $H\_k$ as a separable RKHS equipped with reproducing kernel $k: \calX\times\calX \to \R$, such that $k(x,\cdot) = \phi(x) \in H\_k$, and $k\_{\max} = \sup\_{x\in\calX}k(x, x)<\infty$.

We have already seen in [Part 3](2020-09-24-hilbert-basis.md) that the integral operator
<div>
$$
\begin{align}
  \calK(f)(t) = \int_{\calX} f(x)k(x,y)\;d\mu(x),\quad \calK: \calL^2(\calX) \to \calL^2(\calX)
\end{align}
$$
</div>
is a HS operator if $k\in\calL^2(\calX\times\calX, \mu)$. In fact, we may impose the following assumption to get a nice property on the spectrum of the HS operator $\calK$.

**Lemma 2.** _With the above notation, assume $\E\_{X}[\norm{\phi(X)}\_{H_k}] = \int k(x,x) \;d\P < \infty$, then $\calK$ is HS and of trace class (i.e. $\tr{\calK} = \sum\_i \lambda\_i < \infty$)._

_Proof._
The fact that $\calK$ is HS is obvious, since
<div>
$$
  \E_{X,Y}[k^2(X,Y)] =
  \int_{\calX}\int_{\calX} k(x,y)^2\; d\P(x)d\P(y)
  \leq [\E\norm{\phi(X)}^2]^2 < \infty,
$$
</div>
therefore $k\in\calL^2(\calX\times\calX, \mu)$. Now, we also have that
<div>
$$
  \int k(x,x) \;d\P
  = \int \sum_i \lambda_i \phi_i(x)\phi_i(x) \;d\P
   = \sum_i \lambda_i \int \phi_i(x)\phi_i(x) \;d\P = \sum_i \lambda_i = \tr{\calK}
$$
</div>
since the LHS is bounded, we get the result.
<div style="text-align: right"> $\square$ </div>
This Lemma is relevant in linking the Integral operator with the centered Covariance operator via the linear operator considered in [Part 2](2020-09-24-hilbert-basis.md). What is most interesting is that the eigenvalues of the two coincides.

<h2 class="section-heading">Covariance operator of reproducing kernel</h2>
Just as remarked in Part 3, the definition of (centered) Covariance operator is also comparable to the Covariance/Gram matrix in the finite dimensional space. But as a start, we will need to define the mean element in the RKHS.

**Definition 6 (Mean element).** _The mean element in $H_k$ is defined as $\mu\_X = \E\_X[k(X, \cdot)]\in H\_k$ such that for any $f\in H\_k$_
<div>
$$
   \inner{f, H_k}_{H_k} = \E[f(X)].
$$
</div>

**Definition 7 (Cross-covariance operator).** _With the same setup in the beginning, assume $(\calY, \Omega\_{\calY}, \Q)$ is another probability space, such that $\calY$ is a metric space. Then let $Y$ denote a random variable supported on $\calY$. Finally, denote $G\_h$ a RKHS equipped with reproducing kernel $h$._

_Let $\mu\_X, \mu\_Y$ be the two mean elements in $H\_k$ and $G\_h$ respectively. Then the Cross-covariance operator is defined as_
<div>
$$
  C_{X,Y} = \E_{X,Y}[(k(X,\cdot) - \mu_X)\otimes (h(Y,\cdot) - \mu_Y)],
$$
</div>
_where for any $f\in H\_k, g\in G\_h$,_
<div>
$$
  \begin{align*}
    \inner{f, C_{X,Y}g}_{H_k}
    &= \E_{X,Y}[\inner{k(X,\cdot)- \mu_X, f}_{H_k}\inner{h(Y,\cdot) - \mu_Y, g}_{G_h}]\\
    &= \E_{X,Y}[(f(X)-\E_X[f])(g(Y)-\E_Y[g])].
  \end{align*}
$$
</div>
_Therefore, the (Auto-)covariance operator is as followed_
<div>
$$
\Sigma_X = C_{X,X} = \E_{X,X}[(k(X,\cdot) - \mu_X)\otimes (k(X,\cdot) - \mu_X)].
$$
</div>

Indeed, the covariance operator is HS, since
<div>
$$
\begin{align*}
  \norm{\Sigma_X}_{HS}
  &\leq \E_{X,X}[\norm{(k(X,\cdot) - \mu_X)\otimes (k(X,\cdot) - \mu_X)}_{HS}^2]\\
  &= \E_{X,X}[\norm{k(X,\cdot) - \mu_X}_{H_k}^4]\\
  &\leq \E_{X,X}[\norm{k(X,\cdot)}_{H_k} + \norm{\mu_X}_{H_k}]^4\\
  &\leq \E_{X,X}[\sqrt{k(X,X)} + \sqrt{k(X,X)}]^4\\
  &= 16k_{\max}^2 < \infty
\end{align*}
$$
</div>
where the first inequality is by Jensen's inequality, and the last inequality is due to
<div>
$$
  \norm{k(X,\cdot)}_{H_k} = \sqrt{k(X,X)} \leq \sqrt{k_{\max}}\quad \text{and for $X'$ an i.i.d copy of $X$}
$$
</div>
<div>
$$
  \norm{\mu_X}_{H_k}^2 = E_{X'}\inner{k(X',\cdot), \mu_X}_{H_k} = \E_{X'}\E_{X}[k(X',X)] < k_{\max}.
$$
</div>

**Remark.** _It is to note that, the operator $L:H\_k\to\R$, s.t. $L(f) = \E\_X[f(X)]\; \forall f\in H\_k$ is linear and continuous if $k$ is uniformly bounded, i.e. $\sup\_{x\in\calX} k(x,x)<\infty$. Then by Riesz representation theorem, the existence of $\mu\_X$ is guaranteed._

**Remark.** _Since $H\_k$ is compact, it guarantees the empirical mean element to be in $H\_k$. Similarly, as the space of HS operator is a Hilbert space, it is therefore compact, which also means the empirical estimator of the covariance function is in the same space of $\Sigma\_X$. This suggests the consistency of the estimators._

From now on, we assume the Covariance operator is centered, i.e. $\mu\_X=0$. We will show next that the spectrum of the Integral operator and the Covariance operator coincides. This important result is fundamental to the analysis of a class of spectral/regularised algorithms, e.g. ridge regression and gradient methods [2].

**Theorem 7.** _Let $(\calX, \Omega\_{\calX}, \P)$ be a probability space, $H\_k$ separable RKHS with kernel $k$ and feature map $\phi$ as assumed in the beginning. In addition, let $\E\norm{\phi(X)}\_{H_k}^2<\infty$. Then, both of the integral operator $\calK$ and the Covariance operator $\Sigma\_X$ can be characterised by a continuous linear operator. Moreover, their eigenvalues (all positive) coincides._

_Proof._

It is obvious from Lemma 2. that $\calK$ is a HS trace class integral operator. Now, let us consider a linear map $\calT:H\_k\to \calL^2(\P)$ s.t.
<div>
$$
  \calT h = \inner{h, \phi(\cdot)}_{H_k}.
$$
</div>
This is in fact the linear (evaluation) operator.
Indeed $\calT h\in\calL^2(\P)$, since by Cauchy-Schwartz (CS),
<div>
$$
  \norm{\calT h}_{\calL^2}
  = \E[\calT h(X)]^2
  = \E\inner{h,\phi(X)}_{H_k}^2
  \leq \norm{h}^2_{H_k} \E\norm{\phi(X)}^2_{H_k}
  < \infty
$$
</div>
We can similarly show that $\calT$ is indeed continuous with
<div>
$$
  \norm{\calT h_1 - \calT h_2}_{\calL^2(\P)}
  \leq \norm{h_1 - h_2}_{H_k}^2 \E\norm{\phi(X)}_{H_k}^2.
$$
</div>
Then $\calT^{\ast}$ is also continuous. We will show that the adjoint is of the form $L$ introduced in Part 2. Now, let $f\in\calL^2(\P)$ it gives
<div>
$$
  \inner{\calT^{\ast}f, h}_{H_k}
  = \inner{f, \calT h}_{\calL^2(\P)}
  = \E[f(X)\inner{h, \phi(X)}_{H_k}]
  = \inner{h, \E[f(X)\phi(X)]}_{H_k},
$$
</div>
hence $\calT^{\ast}f = \E[f(X)\phi(X)] = \inner{f, \phi(\cdot)}\_{\calL^2(\P)}$. Moreover, we can show that $\calT^{\ast}f\in H\_k$, where
<div>
$$
  \norm{\calT^{\ast}f}_{H_k}
  \leq \E\norm{f(X)\phi(X)}_{H_k}
  \leq [\E\norm{f(X)}_{H_k}^2\E\norm{\phi(X)}_{H_k}^2]^{1/2}
  <\infty,
$$
</div>
then $\calT^{\ast}: \calL^2(\P) \to H\_k$. In addition, for $h, h'\in H\_k$
<div>
$$
  \inner{h, \calT^{\ast}\calT g'}_{H_k}
  = \inner{\calT h, \calT h'}_{\calL^2(\P)}
  = \E[h(X)h'(X)],
$$
</div>
hence $\Sigma\_X = \calT^{\ast}\calT$; and for $f\in\calL^2(\P)$,
<div>
$$
  \calT\calT^{\ast}f
  = \inner{\calT^{\ast}f, \phi(\cdot)}_{H_k}
  = \E[f(X)\inner{\phi(X), \phi(\cdot)}_{H_k}]
  = \int_{\calX} f(x)k(x,\cdot) \;d\P(x)
$$
</div>
therefore $\calK = \calT\calT^{\ast}$.

Now, what is left to prove is that $\Sigma\_X$ and $\calK$ have the same spectrum. Let $\lambda(A) = \\{\lambda: Ax = \lambda x\\}$ be the spectrum for $A$, and $E\_{\lambda}(A) = \\{x: Ax = \lambda x\\}$ the eigenspace associated with the eigenvalue $\lambda$. Observe that for $f\in E\_{\lambda}(\calK)$,
<dic>
$$
  (\calT^{\ast}\calT)\calT^{\ast}f = \calT^{\ast}(\calT\calT^{\ast})f
  = \lambda\calT^{\ast} f
$$
</dic>
so $\calT^{\ast}f\in E\_{\lambda}(\Sigma\_X)$, i.e. $\calT^{\ast}E\_{\lambda}(\calK)\subset E\_{\lambda}(\Sigma\_X)$. Apply $\calT$ on both sides gives
<dic>
$$
  \calT\calT^{\ast}E_{\lambda}(\calK)
  = \calK E_{\lambda}(\calK) = E_{\lambda}(\calK)
  \subset \calT E_{\lambda}(\Sigma\_X)
$$
</dic>
Similarly $\calT E\_{\lambda}(\Sigma\_X)\subset E\_{\lambda}(\calK)$, hence $E\_{\lambda}(\calK)\subset \calT E\_{\lambda}(\Sigma\_X) \subset E\_{\lambda}(\calK)$. Therefore,
the equality holds, i.e. $E\_{\lambda}(\calK) = \calT E\_{\lambda}(\Sigma\_X)$.

The same procedure also gives $E\_{\lambda}(\Sigma\_X) = \calT^{\ast} E\_{\lambda}(\calK)$. Consequently, we have $\dim{E\_{\lambda}(\Sigma\_X)} = \dim{E\_{\lambda}(\calK)}$, i.e. $\lambda$ is the eigenvalue of both of $\calK$ and $\Sigma\_X$ and with the same multiplicity.
<div style="text-align: right"> $\square$ </div>
With the necessary concepts introduced in these four articles, many interesting topics emerge naturally linking to spectral properties of RKHS. Apart from the use of RKHS in learning theory as we briefly mentioned in this post, we also have the connection of (stochastic) differential equations to the reproducing kernels. An evidence would be Gaussian Process (GP). Extensions on the domain of the RKHS is also possible, to e.g. compact Riemannian manifold.

Since much theory is quite involved, it would take much more time to read through the necessary details on Harmonic analysis, SDE and probably Riemannian manifold. So the following posts may be largely consists of my intuitions and comments, and may serve as a recording of my thinkings that I would like to share.

<h2 class="section-heading">References</h2>

1. Harchaoui, Z. STAT 538 Statistical Learning: Modeling, Prediction, And Computing, [Lecture 6](../stat538lec6.pdf). University of Washington, 2019.
2. Lin J, Rudi A, Rosasco L, Cevher V. Optimal rates for spectral algorithms with least-squares regression over Hilbert spaces. Applied and Computational Harmonic Analysis. 2020 May 1;48(3):868-90.
3. Gretton, A. [Notes on mean embeddings and covariance operators](http://www.gatsby.ucl.ac.uk/~gretton/coursefiles/lecture5_covarianceOperator.pdf). UCL, 2020 Jan.
