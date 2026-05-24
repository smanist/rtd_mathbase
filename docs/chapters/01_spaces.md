# Spaces

(spaces:overview)=
## Why Spaces Matter

Many models in applied mathematics are easiest to understand after separating
the algebraic, geometric, and limiting structures they require. A useful
hierarchy is

```{math}
\begin{aligned}
&\boxed{\text{Vector space}} \\
&\xrightarrow{\text{add an inner product}}
\boxed{\text{Inner product space}} \\
&\xrightarrow{\text{use the induced norm and metric}}
\boxed{\text{Pre-Hilbert space}} \\
&\xrightarrow{\text{complete the space}}
\boxed{\text{Hilbert space}} .
\end{aligned}
```

Each step adds operations that make new questions meaningful. A vector space
lets us form linear combinations. A norm lets us measure error. An inner product
lets us talk about angles, orthogonality, and projections. Completeness ensures
that limits of convergent approximations remain in the space.

(spaces:vector-space)=
## Vector Spaces

A vector space consists of a nonempty set $V$ of vectors, a field $F$ of
scalars, vector addition, and scalar multiplication,

```{math}
+ : V \times V \to V,
\qquad
\cdot : F \times V \to V.
```

For all $u,v,w \in V$ and $a,b \in F$, vector addition must satisfy

```{math}
u + (v + w) = (u + v) + w,
\qquad
u + v = v + u,
```

and there must be a zero vector $0 \in V$ and an additive inverse $-v \in V$
such that

```{math}
v + 0 = v,
\qquad
v + (-v) = 0.
```

Scalar multiplication must be compatible with the field operation and must
distribute over both vector addition and scalar addition:

```{math}
a(bv) = (ab)v,
\qquad
1v = v,
```

```{math}
a(u+v)=au+av,
\qquad
(a+b)v=av+bv.
```

The familiar Euclidean space $V=\mathbb{R}^d$ over $F=\mathbb{R}$ is the
standard finite-dimensional example. Function spaces are often more important
in modeling. For example, the set $P^p$ of polynomials of degree at most $p$
with real coefficients is a vector space, since every element can be written as
a finite linear combination of the basis functions

```{math}
1, x, x^2, \ldots, x^p.
```

The square-integrable functions on $[0,1]$ form an infinite-dimensional example:

```{math}
L^2[0,1]
=
\left\{
f : \int_0^1 |f(x)|^2 \,\dd x < \infty
\right\}.
```

The word "infinite-dimensional" means that no finite basis can span the whole
space.

(spaces:metric-norm)=
## Metrics and Norms

A metric adds a notion of distance. It is a map

```{math}
d : V \times V \to \mathbb{R}
```

such that, for all $x,y,z \in V$,

```{math}
d(x,x)=0,
\qquad
x \ne y \Rightarrow d(x,y)>0,
```

```{math}
d(x,y)=d(y,x),
\qquad
d(x,z) \le d(x,y) + d(y,z).
```

A norm adds a notion of magnitude. It is a map

```{math}
\|\cdot\| : V \to \mathbb{R}
```

such that, for all $x,y \in V$ and $\lambda \in F$,

```{math}
\|x\| \ge 0,
\qquad
\|x\| = 0 \iff x=0,
```

```{math}
\|\lambda x\| = |\lambda|\,\|x\|,
\qquad
\|x+y\| \le \|x\|+\|y\|.
```

Every norm induces a metric by

```{math}
d(x,y)=\|x-y\|.
```

The reverse is not true. For example, the discrete distance

```{math}
d(x,y)=
\begin{cases}
0, & x=y,\\
1, & x\ne y
\end{cases}
```

is a metric, but it is not induced by a norm because it is not compatible with
scaling. Similarly, many norms do not come from inner products. The
$\ell^1$ norm

```{math}
\|x\|_1 = \sum_i |x_i|
```

is a norm on $\mathbb{R}^d$, but it is not induced by an inner product.

(spaces:inner-product)=
## Inner Product Spaces

An inner product equips a vector space with a way to multiply vectors:

```{math}
\langle \cdot,\cdot\rangle : V \times V \to F.
```

For complex vector spaces, it satisfies conjugate symmetry,

```{math}
\langle x,y\rangle = \overline{\langle y,x\rangle},
```

linearity in the first argument,

```{math}
\langle ax + by,z\rangle
=
a\langle x,z\rangle + b\langle y,z\rangle,
```

and positive definiteness,

```{math}
x \ne 0 \Rightarrow \langle x,x\rangle > 0.
```

For real vector spaces, conjugate symmetry reduces to ordinary symmetry. An
inner product induces a norm,

```{math}
\|x\| = \sqrt{\langle x,x\rangle},
```

and therefore also induces a metric,

```{math}
d(x,y)
=
\|x-y\|
=
\sqrt{\langle x-y,x-y\rangle}.
```

The Euclidean inner product is

```{math}
\langle x,y\rangle = x^T y.
```

On $L^2[0,1]$, a standard complex inner product is

```{math}
\langle f,g\rangle_{L^2}
=
\int_0^1 f(x)\overline{g(x)}\,\dd x.
```

Inner products make orthogonality and projection possible. Given a basis
$\{v_i\}$ and a dual family $\{u_j\}$ satisfying

```{math}
\langle u_j,v_i\rangle =
\begin{cases}
1, & i=j,\\
0, & i\ne j,
\end{cases}
```

the coefficients in an expansion can be recovered by taking inner products:

```{math}
x_k = \sum_{i=1}^k c_i v_i,
\qquad
c_i = \langle u_i,x_k\rangle.
```

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

This is why Hilbert spaces are the natural setting for Fourier expansions,
orthogonal projections, spectral decompositions, and kernel methods.

(spaces:summary)=
## Summary

The hierarchy can be read as a list of added capabilities:

| Structure | Added operation | What it enables |
| --- | --- | --- |
| Vector space | Addition and scalar multiplication | Linear combinations, span, basis, dimension |
| Metric space | Distance | Convergence, continuity, limits |
| Normed vector space | Magnitude | Approximation error, stability, bounded operators |
| Inner product space | Angle | Orthogonality, projections, least squares, spectral theory |
| Hilbert space | Completeness | Limits of approximations, infinite expansions, well-posed projections |

The next chapter uses this hierarchy to construct reproducing kernel Hilbert
spaces, where functions are studied through inner products with kernels.
