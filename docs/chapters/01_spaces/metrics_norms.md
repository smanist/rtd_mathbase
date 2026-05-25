(spaces:metric-norm)=
# Metrics and Norms

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
