---
layout: post
title: Flake it till you make it
subtitle: Excerpt from Soulshaping by Jeff Brown
<!-- cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg -->
header-img: /assets/img/thumb.png
tags: [test]
category: math
---

_**Disclaimer.** This post is served as a summarisation of my study notes on RKHS theory [1], and classes I took on relevant topics, containing theoretical details from [1, 2] along with my interpretations directed by my personal interests on those topics. I am by no means an expert in functional analysis and spectral theory, so please feel free to point out any mistakes in the post._
<br/><br/>

**Definition 2 (Positive Definite Quadratic Form).** _A function $k: \calX \times \calX \to \R$ is called a positive definite quadratic form, or positive definite function, if for any function $h:\calX\to \mathbb{R}$ and for any finite subset $\calX' \subset \calX$,_

<div>
$$
	\sum_{x_1, x_2 \in \calX'} h(x_1)h(x_2)k(x_1, x_2)\geq 0
$$
</div>

_It is said to be strictly positive definite if $h\equiv 0$, i.e. function $h$ is the zero function._

**Theorem 1 (Aronszajn, 1950).** _Let $\calX$ be a metric space, and $k:\calX\times \calX \to \mathbb{R}$ be a positive definite function, there exists a unique Hilbert space $(H_k, \inner{\cdot, \cdot}\_{H\_k})$ of functions on $\calX$ satisfying the followings:_
1. $\phi(x) = k(x,\cdot)\in \calH,\; \forall x\in \calX$;
2. $\span\\{\phi(x): x\in \mathcal{X}\\}$ is dense in $\calH$; and
3. $f(x) = \inner{\phi(x), f}\_{\calH}\; \forall f\in\calH,\, x\in\calX$.

_Therefore, $\calH$ is the unique RKHS with reproducing kernel $k$, thus denoted by $H_k$._

_Proof._ We here give a walk-through of the proof, for full details please refer to [2].

Consider 

\begin{align}
	H\_{0,k} &= \span\\{\phi(x): x\in\calX\\} \\
	&= \\{f=\sum_{i=1}^s \alpha\_i\phi(x\_i):x\_i \in \calX, \alpha\_i\in\R\; \forall i=1,\dots,s, \;\mathrm{and} \;s\in\N\\},
\end{align}

\displaylines{
	H\_{0,k} &= \span\\{\phi(x): x\in\calX\\} \\
	&= \\{f=\sum_{i=1}^s \alpha\_i\phi(x\_i):x\_i \in \calX, \alpha\_i\in\R\; \forall i=1,\dots,s, \;\mathrm{and} \;s\in\N\\},
}

then we show the bilinear form $\inner{\cdot, \cdot}\_{H\_{0,k}}: H\_{0,k} \times H\_{0,k} \to \R$,

$$
	\inner{f, g}\_{H\_{0,k}}
	= \inner{\sum\_{i=1}^s\alpha\_i\phi(x\_i), \sum_{j=1}^r\beta\_j\phi(y\_j)}
	= \sum\_{i=1}^s\sum\_{j=1}^r \alpha\_i\beta\_j k(x\_i, y\_j)\, ,
$$

is a well-defined inner product, which gives $H\_{0,k}$ the structure of a pre-Hilbert space. Moreover, we can prove that $(H_{0,k}, \inner{\cdot, \cdot}\_{H\_{0,k}})$ satisfies all three conditions in the statement. Note that the definition of the inner product gives condition 3., where 

$$
	\inner{f, \phi(x)}\_{H\_{0,k}} = \sum\_{i=1}^s k(x\_i, x) = f(x).
$$

The following step is to show the completion of $H_{0,k}$ (by adding the limit of every Cauchy sequence $\\{f_n\\}\_{n\in\N}\subset H_{0,k}$) is a Hilbert space denoted by $H_k$, with bilinear form $\inner{\cdot, \cdot}\_{H\_k}, \;s.t.$ there exists sequences $\\{f\_n\\}\_{n\in\N}, \\{g\_n\\}\_{n\in\N} \subset H\_{0,k}$,

$$
	\inner{f,g}\_{H_k} = \lim\_{n\to \infty} \inner{f\_n, g\_n}\_{H\_{0,k}}.
$$

To do this, we need to verify that the limit exists (i.e. to show the sequence of inner product $\\{\inner{f\_n, g\_n}\_{H\_{0,k}}\\}\_{n\in\N}$ is a Cauchy sequence). Then, all three conditions follows directly from the definition of completion.

Lastly, the uniqueness of RKHS can be verified such that if $G_k$ is also a Hilbert space satisfying those three conditions, then $G\_k = H\_k$ and $\inner{\cdot, \cdot}\_{G\_k} = \inner{\cdot, \cdot}\_{H\_k}$. Notably, $H\_{0,k} \subset G\_k$ due to condition 2., and the equivalence of the inner product is directly given by 3. Now, since both $G\_k$ and $H\_k$ are completions of $H\_{0,k}$, the uniqueness follows from the uniqueness of the completion procedure.

$\square$
{:.right}

Under what circumstances should we step off a path? When is it essential that we finish what we start? If I bought a bag of peanuts and had an allergic reaction, no one would fault me if I threw it out. If I ended a relationship with a woman who hit me, no one would say that I had a commitment problem. But if I walk away from a seemingly secure route because my soul has other ideas, I am a flake?

The truth is that no one else can definitively know the path we are here to walk. It’s tempting to listen—many of us long for the omnipotent other—but unless they are genuine psychic intuitives, they can’t know. All others can know is their own truth, and if they’ve actually done the work to excavate it, they will have the good sense to know that they cannot genuinely know anyone else’s. Only soul knows the path it is here to walk. Since you are the only one living in your temple, only you can know its scriptures and interpretive structure.

At the heart of the struggle are two very different ideas of success—survival-driven and soul-driven. For survivalists, success is security, pragmatism, power over others. Success is the absence of material suffering, the nourishing of the soul be damned. It is an odd and ironic thing that most of the material power in our world often resides in the hands of younger souls. Still working in the egoic and material realms, they love the sensations of power and focus most of their energy on accumulation. Older souls tend not to be as materially driven. They have already played the worldly game in previous lives and they search for more subtle shades of meaning in this one—authentication rather than accumulation. They are often ignored by the culture at large, although they really are the truest warriors.

A soulful notion of success rests on the actualization of our innate image. Success is simply the completion of a soul step, however unsightly it may be. We have finished what we started when the lesson is learned. What a fear-based culture calls a wonderful opportunity may be fruitless and misguided for the soul. Staying in a passionless relationship may satisfy our need for comfort, but it may stifle the soul. Becoming a famous lawyer is only worthwhile if the soul demands it. It is an essential failure if you are called to be a monastic this time around. If you need to explore and abandon ten careers in order to stretch your soul toward its innate image, then so be it. Flake it till you make it.
