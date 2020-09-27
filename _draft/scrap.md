
## Unfounded claim with regularisation operator, the concept is wierd in itself.
**Remark 1.**_One interesting consequence with this definition of RKHS is that we can define in closed form the regularisation operator [2] on functions in $H_k$, in the sense that we can find a corresponding positive operator $T_{H_k}: H_k \to \calH$ satisfying 
$$
\inner{f, g}_{H_k} = \inner{T_{H_k}f, T_{H_k}g}_{\calH};
$$
therefore, the norm would be equivalent to $\norm{f}_{H_k} = \norm{T_{H_k}f}_{\calH}$. So the regularisation property of the RKHS norm can be analysed via the operator $T_{H_k}$. In particular, if the kernel is stationary, i.e. $\exists h\in L^1(\R^d)$ strictly positive definite such that $k(x,x') = h(x-x')$, then by a variation of Bochner's theorem (Wendland 2015), the regularisation property of $T_{H_k}$ can be analysed via the scaled Fourier transform of $k$ [2]._

Now, we give the regularisation operator $T_{H_k}: H_k \to \calH$ defined as followed,
$$

$$
We can easily see that $T_{H_k}$ satisfies the property stated in Remark 1:

_Proof._
Let $f, g \in H_k$ with $F, G\in \calH$ such that $f = LF$, $g = LG$. Here we do not require $L$ to be injective. Then, using Parseval's identity, we obtain
\begin{equation*}
\begin{align}
\inner{f, g}_{H_k} 
&= \sum_{i=1}^{\infty} \inner{\Pker F, V_j}_{\calH}\inner{V_j, \Pker G}_{\calH}\\
&= \sum_{i=1}^{\infty} \inner{f, v_j}_{H_k} \inner{g, v_j}_{H_k}\\
&= \sum_{i,j=1}^{\infty} \inner{f, v_i}_{H_k} \inner{g, v_j}_{H_k} \inner{V_i, V_j}_{\calH}\\
&= \inner{T_{H_k}f, T_{H_k}g}_{\calH}.
\end{align}
\end{equation*}

$\square$
{:.right}

It is shown in [1] that $T_{H_k}$ is an isometry from $H_k$ to $\calH$. In addition, for any $f\in H_k$, $T_{H_k}(f)$ is a unique element in $\ker{L}^{\perp}$.



## Bochner's Theorem

<h3>Regularisation property of stationary kernels</h3>

The most common function space that can be applied to the above formulation is $\calL^2$ space, which is also very important in Fourier analysis. In particular, we will see the following Theorem connecting stationary kernel, Fourier analysis and regularisation theory.

**Theorem 4 (Bochner's Theorem, Wendland 2015)**_A continuous function $h$ on $\R^d$ is positive definite iff there exists a finite non-negative Borel measure $\mu$ on $\R^d$ such that
$$
h(x) = \int_{\R^d} e^{-i\inner{x,\omega}\; d\mu(\omega)}
$$_

Assume $\nu(\omega)$ is integrable and $L^2(\R^d)$ with uniform measure, by Theorem 4, we have
$$
k(x,x') = \int e^{-i\inner{x-x', \omega}} \nu(\omega)\;d\omega 
= \int e^{-i\inner{x, \omega}} \overline{e^{-i\inner{x', \omega}}} \nu(\omega)\;d\omega.
$$
Recall the $d$-dim Fourier transform is given by
$$
\calF(f)(\omega) = (2\pi)^{-d/2} \int f(x) e^{-i\inner{x,w}}\;dx
$$
Then the Fourier transform of $k(x,x')$ is 
\begin{equation*}
\begin{align}
\calF(k(x,\cdot))(\omega) 
& = (2\pi)^{-d/2} \int\int(\nu(\omega')e^{-i\inner{x, \omega'}})
e^{i\inner{x', \omega'}}\;d\omega' e^{-i\inner{x', \omega}} dx' \\
&= (2\pi)^{-d/2}\nu(\omega)e^{-i\inner{x, \omega}}
\end{align}
\end{equation*}
Substuting back the expression of $e^{-i\inner{x, \omega}}$ in terms of $\calF(k(x,\cdot))(\omega)$ into the kernel gives the following
$$
k(x,x') = (2\pi)^{-d/2}\int \frac{\calF(k(x,\cdot))(\omega) \overline{\calF(k(x',\cdot))(\omega)}}{\nu(\omega)}\;d\omega
$$
This leads to the regularisation operator $T = $
