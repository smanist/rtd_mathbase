(spaces:inner-product)=
# Inner Product Spaces

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
## Orthogonality and Projection

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
## Orthogonal Operators

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
## Adjoints and Self-Adjoint Operators

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
## Singular Value Decomposition

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
