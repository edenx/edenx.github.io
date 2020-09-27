---
layout:     post
title:      "Reproducing Kernels, Green's Functions and Regularisation Theory"
subtitle:   "With the spectral perspective of RKHS introduced in the last post, we now look at a special and important category of reproducing kernels, which is the Green's functions to positive systems of differential equations. We will have Laplace operator as a motivating example, which is based on spectral theory of Linear operators."
date:       2020-09-23 08:00
author:     "edenx"
tags: 		[kernel, Lapalcian]
category:   math
---

_**Disclaimer.** This post is served as a summarisation of my study notes on RKHS theory [1], and papers I read on relevant topics, containing theoratical details from [1, 2] along with my interpretations directed by my personal interests on those topics. I am by no means an expert in functional analysis and spetral theory, so please point out any mistakes in the post and send me an email about it.
<br/><br/>_


I do personally have an interest in graphs, and graph Laplacian (and Laplace operators as well), who has nice properties and wide applications owing to its representation of second order information and its spctral properties. Here's a blog ['Why Laplacian?'](https://donskerclass.github.io/post/why-laplacians/) written by Prof David Childers at CMU Economics on some applications of Laplace operator/ Graph Laplacians and their interpretations in each context. One of the purpose of this article is to provide with another manifestation of Laplacian's usefulness in function smoothing, in terms of its Green's functions and RKHS constructed by it.

We first give an overview of Laplace operator, which is the continuous counterpart in $\mathcal{L}^2$ space, as a case study, and how it relates to a RKHS. Then we give a more general relationship of RKHS and Green's functions of differential equations. Finally, as a practical example, we consider RKHS on discrete graphs, which is closely related to regularisation on graphs (manifold regularisation by Belkin et al.).

<h2 class="section-heading">Case-study: Spectral properties of Laplace operator, and its connection to RKHS</h2>

<h2 class="section-heading">Green's functions and Reproducing Kernels</h2>

<h2 class="section-heading">Example: Kernel/Regularisation Operators on Graph </h2>

<h2 class="section-heading">References</h2>

1. Nachman Aronszajn and Kennan Taylor Smith. Characterization of positive reproducing kernels.applications to green’s functions.American Journal of Mathematics, 79(3):611–622, 1957.

2. Alex J Smola, Bernhard Schölkopf, and Klaus-Robert Müller. The connection between regular-ization operators and support vector kernels.Neural networks, 11(4):637–649, 1998.

3. Alexander J Smola and Risi Kondor. Kernels and regularization on graphs. In Learning theory and kernel machines, pages 144–158. Springer, 2003.

