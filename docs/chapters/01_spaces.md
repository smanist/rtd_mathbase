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

The weakest linear structure starts with addition. A set with an operation
$+$ is an abelian group if addition is closed, associative, commutative, has a
zero element, and every element has an additive inverse. In symbols, for
$u,v,w \in V$,

```{math}
u + (v+w) = (u+v) + w,
\qquad
u+v=v+u,
```

and there are elements $0 \in V$ and $-v \in V$ such that

```{math}
v+0=v,
\qquad
v+(-v)=0.
```

A vector space adds scalar multiplication to this additive structure. More
precisely, a vector space consists of a nonempty set $V$ of vectors, a field
$F$ of scalars, vector addition, and scalar multiplication,

```{math}
+ : V \times V \to V,
\qquad
\cdot : F \times V \to V.
```

For all $u,v \in V$ and $a,b \in F$, scalar multiplication is compatible with
the field operations and distributes over both vector addition and scalar
addition:

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

At this level there is no distance, length, angle, coordinate system, or
preferred basis. The only meaningful operations are linear combinations.

(spaces:finite-dimensional)=
### Bases and Dimension

A basis of a vector space $V$ is a linearly independent spanning set. If

```{math}
\mathcal{B}=\{e_1,\ldots,e_n\}
```

is a basis, then each $v \in V$ can be written in exactly one way as

```{math}
v = x_1 e_1 + \cdots + x_n e_n.
```

The coordinate vector of $v$ in the basis $\mathcal{B}$ is

```{math}
[v]_{\mathcal{B}}
=
\begin{pmatrix}
x_1\\
\vdots\\
x_n
\end{pmatrix}.
```

The number of basis vectors is independent of the chosen basis. This number is
the dimension of $V$, written $\dim V$. In finite dimensions, dimension
classifies vector spaces up to linear isomorphism: if
$\dim V=\dim W=n$, then both spaces are linearly isomorphic to $F^n$, and
therefore to each other.

The basis is a choice, while the dimension is not. Changing the basis changes
coordinates, but it does not change the underlying vector or the dimension of
the space.

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

(spaces:linear-maps)=
### Linear Maps

Once the only accepted operations are addition and scalar multiplication, the
natural structure-preserving maps are the maps that preserve exactly those
operations. A map $T:V\to W$ is linear if, for all $u,v\in V$ and
$a\in F$,

```{math}
T(u+v)=T(u)+T(v),
\qquad
T(av)=aT(v).
```

Equivalently, linear maps preserve every finite linear combination:

```{math}
T\left(\sum_{j=1}^n a_j v_j\right)
=
\sum_{j=1}^n a_j T(v_j).
```

Linear maps compose: if $T:U\to V$ and $S:V\to W$ are linear, then
$S\circ T:U\to W$ is linear. Each vector space also has an identity map
$\mathrm{id}_V:V\to V$. Thus vector spaces and linear maps form a category:
objects are vector spaces, arrows are linear maps, composition is ordinary
function composition, and identities are identity maps.

(spaces:matrices)=
### Matrices as Coordinate Representations

A matrix is not an additional linear object. It is the coordinate
representation of a linear map after bases have been chosen.

Let $T:V\to W$ be linear. Choose a basis
$\mathcal{B}=\{e_1,\ldots,e_n\}$ for $V$ and a basis
$\mathcal{C}=\{f_1,\ldots,f_m\}$ for $W$. Since the values of $T$ on a basis
determine the whole map, write

```{math}
T(e_j)
=
a_{1j} f_1 + \cdots + a_{mj} f_m,
\qquad j=1,\ldots,n.
```

The coefficients form the $m\times n$ matrix

```{math}
[T]_{\mathcal{C}\leftarrow\mathcal{B}}
=
\begin{pmatrix}
a_{11} & \cdots & a_{1n}\\
\vdots & & \vdots\\
a_{m1} & \cdots & a_{mn}
\end{pmatrix}.
```

If $v=x_1e_1+\cdots+x_ne_n$, then the coordinates of $T(v)$ are obtained by
ordinary matrix-vector multiplication:

```{math}
[T(v)]_{\mathcal{C}}
=
[T]_{\mathcal{C}\leftarrow\mathcal{B}} [v]_{\mathcal{B}}.
```

Matrix multiplication is forced by composition. If
$U\xrightarrow{T}V\xrightarrow{S}W$, and the chosen bases represent $T$ by
$A$ and $S$ by $B$, then the coordinate representation of the composite must
satisfy

```{math}
[S(T(u))] = B(A[u]).
```

Therefore the matrix of $S\circ T$ is $BA$. The familiar row-by-column rule is
the unique bilinear rule that makes this compatibility hold for every input
coordinate vector.

Changing bases changes the matrix but not the underlying map. For an operator
$T:V\to V$, a change of basis transforms its matrix by similarity,

```{math}
A \mapsto S A S^{-1}.
```

For a general map $T:V\to W$, independent changes of basis in the source and
target transform the matrix by left and right multiplication by invertible
matrices,

```{math}
A \mapsto P A Q^{-1}.
```

The numerical entries of a matrix are therefore basis-dependent. The
invariants of the linear map are the quantities and subspaces that survive
these coordinate changes.

(spaces:kernel-image-rank)=
### Kernel, Image, and Rank

Two subspaces are attached canonically to every linear map $T:V\to W$. The
kernel records the directions that $T$ sends to zero:

```{math}
\ker T
=
\{v\in V : T(v)=0\}.
```

The image records the part of the target that $T$ actually reaches:

```{math}
\operatorname{im} T
=
\{T(v): v\in V\}
\subseteq W.
```

Both are subspaces. They are intrinsic to $T$; changing bases only changes how
they are written in coordinates.

In finite dimensions, their dimensions give two basic numerical invariants:

```{math}
\operatorname{rank} T = \dim \operatorname{im} T,
\qquad
\operatorname{nullity} T = \dim \ker T.
```

The rank-nullity theorem says that

```{math}
\dim V
=
\dim \ker T + \dim \operatorname{im} T
=
\operatorname{nullity} T + \operatorname{rank} T.
```

This is a dimension balance law. The dimension of the source is split into
directions that are annihilated and directions that have an observable effect
in the target.

Rank also classifies finite-dimensional linear maps up to independent changes
of basis in the source and target. If $\dim V=n$, $\dim W=m$, and
$\operatorname{rank}T=r$, then suitable bases make the matrix of $T$ equal to

```{math}
\begin{pmatrix}
I_r & 0\\
0 & 0
\end{pmatrix}.
```

In these coordinates, the first $r$ source coordinates are copied into the
first $r$ target coordinates, while all remaining source directions land in the
kernel. Once $m$ and $n$ are fixed, the rank is the only numerical invariant
left under arbitrary source and target basis changes.

(spaces:epi-mono)=
### Quotients and the Epi-Mono Factorization

The kernel and image also give a canonical factorization of a linear map. For
$T:V\to W$, first collapse the kernel by the quotient map

```{math}
q:V\to V/\ker T.
```

In the quotient $V/\ker T$, two vectors are identified when their difference
lies in $\ker T$. After this collapse, $T$ becomes injective on the effective
part of the source. The induced map

```{math}
\widetilde{T}:V/\ker T \to \operatorname{im} T,
\qquad
\widetilde{T}([v])=T(v),
```

is a linear isomorphism. Finally, include the image into the target:

```{math}
i:\operatorname{im}T\hookrightarrow W.
```

Together,

```{math}
T = i \circ \widetilde{T} \circ q.
```

This factorization says: first kill the kernel, then identify the quotient
with the image, then embed the image into the target. In categorical language,
it is the regular epi-mono factorization of a linear map: a surjective quotient
map, followed by an isomorphism, followed by an injective inclusion.

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
\langle x,y\rangle = x^\top y.
```

On $L^2[0,1]$, a standard complex inner product is

```{math}
\langle f,g\rangle_{L^2}
=
\int_0^1 f(x)\overline{g(x)}\,\dd x.
```

In finite-dimensional real spaces, inner product spaces are still classified
up to isometric isomorphism by dimension. If two real inner product spaces have
the same finite dimension, orthonormal bases identify both of them with
$\mathbb{R}^n$ with its standard dot product. What changes after adding an
inner product is not the list of possible finite-dimensional objects, but the
maps treated as geometry-preserving: arbitrary invertible maps are replaced by
inner-product-preserving maps.

(spaces:orthogonality-projection)=
### Orthogonality and Projection

Inner products make orthogonality and projection meaningful. Vectors $x$ and
$y$ are orthogonal, written $x\perp y$, if

```{math}
\langle x,y\rangle = 0.
```

The Pythagorean identity follows immediately: if $x\perp y$, then

```{math}
\|x+y\|^2 = \|x\|^2 + \|y\|^2.
```

Thus orthogonal directions contribute independently to squared length.

If $u$ is a unit vector, the orthogonal projection of $v$ onto the line spanned
by $u$ is

```{math}
P_u v = \langle v,u\rangle u.
```

The residual is orthogonal to $u$:

```{math}
v-P_u v \perp u.
```

More generally, if $U\subset V$ is a finite-dimensional subspace, then every
$x\in V$ has a unique decomposition

```{math}
x = u + w,
\qquad
u\in U,\quad w\in U^\perp.
```

The map $P_Ux=u$ is the orthogonal projection onto $U$. It is linear and
satisfies

```{math}
P_U^2=P_U,
\qquad
\operatorname{im}P_U=U,
\qquad
\ker P_U=U^\perp.
```

Projection combines the additive structure of subspaces with the geometric
structure supplied by the inner product.

Given a basis $\{v_i\}$ and a dual family $\{u_j\}$ satisfying

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

(spaces:orthogonal-operators)=
### Orthogonal Operators

A linear map $Q:V\to V$ is orthogonal, or isometric, if it preserves the inner
product:

```{math}
\langle Qx,Qy\rangle = \langle x,y\rangle
\qquad
\text{for all }x,y\in V.
```

It follows that $Q$ preserves lengths and angles. In an orthonormal basis, the
matrix of $Q$ satisfies

```{math}
Q^\top Q = I,
```

so

```{math}
Q^{-1}=Q^\top.
```

For example, the planar rotation

```{math}
R_\theta
=
\begin{pmatrix}
\cos\theta & -\sin\theta\\
\sin\theta & \cos\theta
\end{pmatrix}
```

is orthogonal. It moves the unit disk rigidly; it does not stretch it into an
ellipse. Orthogonal maps therefore represent changes of orthonormal viewpoint,
rotations, and reflections rather than changes of shape.

(spaces:adjoints-spectral)=
### Adjoints and Self-Adjoint Operators

The inner product also lets us reverse a linear operator from one argument of
the inner product to the other. The adjoint of a linear operator $T:V\to V$ is
the operator $T^\ast$ satisfying

```{math}
\langle Tx,y\rangle = \langle x,T^\ast y\rangle
\qquad
\text{for all }x,y\in V.
```

In an orthonormal basis, the matrix of $T^\ast$ is the conjugate transpose of
the matrix of $T$. For real matrices this is the ordinary transpose.

An operator is self-adjoint if

```{math}
T=T^\ast.
```

For real matrices in an orthonormal basis, self-adjoint operators are exactly
symmetric matrices. A typical example is

```{math}
A=
\begin{pmatrix}
2 & 1\\
1 & 3
\end{pmatrix}.
```

The finite-dimensional spectral theorem says that every self-adjoint operator
has an orthonormal basis of eigenvectors. Equivalently, in the real matrix
case, every symmetric matrix can be written as

```{math}
A=Q\Lambda Q^\top,
```

where $Q$ is orthogonal and $\Lambda$ is diagonal. In the orthonormal
eigenbasis, the operator only stretches or compresses each eigendirection:

```{math}
Av_i=\lambda_i v_i.
```

Thus eigenvectors are directions that are not rotated into different
directions, and eigenvalues are the signed scaling factors on those directions.

(spaces:svd)=
### Singular Value Decomposition

The spectral theorem applies directly to self-adjoint operators. A general
linear map $T:V\to W$ need not be self-adjoint, but in finite dimensions it
still has a canonical orthogonal-coordinate description: the singular value
decomposition.

Choose orthonormal bases of $V$ and $W$, and let $A$ be the matrix of $T$.
Then there are orthogonal matrices $U$ and $V$ and a rectangular diagonal
matrix $\Sigma$ such that

```{math}
A = U\Sigma V^\top.
```

The nonzero diagonal entries of $\Sigma$ are the singular values,

```{math}
\sigma_1\ge \sigma_2\ge \cdots \ge \sigma_r > 0,
\qquad
r=\operatorname{rank}A.
```

They can be obtained from the self-adjoint positive semidefinite operator
$A^\top A$. If

```{math}
A^\top A = V\Lambda V^\top,
```

with $\Lambda=\operatorname{diag}(\lambda_i)$ and $\lambda_i\ge 0$, then

```{math}
\sigma_i=\sqrt{\lambda_i}.
```

Geometrically, $V^\top$ first chooses orthonormal coordinates in the source,
$\Sigma$ stretches the first $r$ coordinate directions by
$\sigma_1,\ldots,\sigma_r$ and kills the remaining directions, and $U$ chooses
orthonormal coordinates in the target. The unit ball is sent to an ellipsoid
whose principal axis lengths are the singular values and whose nonzero axis
directions are the left singular vectors.

This refines the algebraic rank normal form. If arbitrary invertible changes
of basis are allowed, a rank-$r$ map reduces to

```{math}
\begin{pmatrix}
I_r & 0\\
0 & 0
\end{pmatrix}.
```

After an inner product is fixed, only orthogonal basis changes preserve the
geometry. The corresponding normal form is $\Sigma$, so rank records how many
directions survive and singular values record how strongly each surviving
orthogonal direction is stretched.

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

At the purely algebraic level, finite-dimensional objects are classified up to
linear isomorphism by dimension, while linear maps are classified up to
independent source and target basis changes by rank. The kernel, image, and
quotient factorization keep track of how a map discards directions, acts on its
effective quotient, and embeds the result into the target.

After an inner product is added, the geometry-preserving transformations are
orthogonal rather than arbitrary invertible maps. This finer equivalence keeps
track of lengths and angles, which is why projections, self-adjoint spectral
decompositions, and singular values become meaningful.

The next chapter uses this hierarchy to construct reproducing kernel Hilbert
spaces, where functions are studied through inner products with kernels.
