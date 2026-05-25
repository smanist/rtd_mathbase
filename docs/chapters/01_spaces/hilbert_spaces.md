# Pre-Hilbert and Hilbert Spaces

(spaces:pre-hilbert)=
## Pre-Hilbert Spaces

A pre-Hilbert space is an inner product space viewed with the norm and metric
induced by that inner product. In this sense, every inner product space is a
pre-Hilbert space.

This terminology becomes useful because the induced metric lets us discuss
limits. A sequence $\{f_n\} \subset H_0$ is Cauchy if, for every
$\epsilon>0$, there exists an integer $N$ such that

```{math}
m,n>N
\quad\Rightarrow\quad
\|f_n-f_m\| < \epsilon.
```

A Cauchy sequence is internally consistent: its terms eventually become
arbitrarily close to each other. However, the sequence may still converge to a
limit outside the original space.

(spaces:hilbert)=
## Hilbert Spaces

A Hilbert space is a complete inner product space. Completeness means every
Cauchy sequence converges, with respect to the induced norm, to an element that
is still in the space.

If $H_0$ is a pre-Hilbert space, its completion is commonly denoted

```{math}
H = \overline{H_0}.
```

The completion adds the missing limits of all Cauchy sequences in $H_0$. This
is what allows one to do analysis with infinite expansions while staying inside
the same space.

For example, let $V_0$ be the space of piecewise linear functions on $[0,1]$
with any finite number of nodes, equipped with the $L^2$ inner product. Let
$f_n$ be the piecewise linear interpolant of $f(x)=x^2$ on $n$ evenly spaced
points. Then $f_n \in V_0$, and $f_n$ converges to $f$ in $L^2$, but
$f \notin V_0$ because $x^2$ is not piecewise linear on a finite partition.
Thus $V_0$ is not complete.

Completeness is the property that prevents this failure. If

```{math}
x_k = \sum_{i=1}^k c_i v_i
```

is a Cauchy sequence in a Hilbert space $H$, then there is some $x^\ast \in H$
such that

```{math}
x^\ast = \lim_{k\to\infty} x_k.
```

This is why Hilbert spaces are the natural setting for many mathematical constructs,
such as Fourier expansions, orthogonal projections, spectral decompositions,
and kernel methods.
