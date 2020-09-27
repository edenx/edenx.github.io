---
layout: post
title: Flake it till you make it
subtitle: Excerpt from Soulshaping by Jeff Brown
cover-img: ""
thumbnail-img: ""
share-img: ""
header-img: ""
tags: [test]
category: math
---

Finally, we end this section with a remark:

**Remark 1.** _We can define a evaluation functional on $\calX$ that $k\_x\; s.t. \; k\_x(f) = f(x)$ for $f\in\calH$, which is a linear operator. Then we have that a Hilbert space is a RKHS iff $k\_x$ is continuous $\forall x\in \calX$. In addition, this implies all the functions in RKHS are continuous._
_Proof._
Here, we only prove for the necessary condition, see [2] for full details. 

Since in this case $k\_x$ is a continuous linear operator, by Riesz representation theorem, we can find $g\_x\in\calH\; s.t.\; f(x) = k\_x(f) = \inner{f, g\_x}\_{\calH},\; \forall f\in\calH$. 
Consider $k(x,y)$ as a function of $y$, then $k(x,y) = k\_y(g\_x) = \inner{g\_x, g\_y}\_{\calH} = g\_x(y)$, for $g\_x\in\calH$ a function of $x$, corresponding to the $f$ in last paragraph; and $g\_y\in\calH$ a function of $y$ given by Riesz.
<div style="text-align: right"> $\square$ </div>

In fact, we will see in the following posts, an RKHS is characterised by a linear operator (associated to a feature map or a PSD kernel). Moreover, this view allows the smoothness property of RKHS to be analysed with spectral properties of the Integral operator of $k$, which gives connections to Harmonic analysis.

<h2 class="section-heading">References</h2>

1. Saburou Saitoh and Yoshihiro Sawano. Theory of reproducing kernels and applications. Springer, 2016.
2. Zaid Harchaoui, UW [STAT538 Lecture1 handout](/docs/STAT538lec1.pdf). 2019.

