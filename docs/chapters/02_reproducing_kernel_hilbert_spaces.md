# Reproducing Kernel Hilbert Spaces

(rkhs:overview)=
## From Hilbert Spaces to Kernels

A reproducing kernel Hilbert space, or RKHS, is a Hilbert space of functions in
which point evaluation can be represented as an inner product. The construction
combines the Hilbert-space structure from {ref}`spaces:hilbert` with a kernel
function that acts as an inner-product generator.

Let $X$ be an input set. A kernel is a function

```{math}
\kappa : X \times X \to \mathbb{R}.
```

For a fixed point $x_1 \in X$, the expression

```{math}
\kappa(\cdot,x_1) : X \to \mathbb{R}
```

is itself a real-valued function on $X$. The RKHS is built from linear
combinations of such functions.

(rkhs:kernels)=
## Positive-Definite Kernels

The kernels used to build RKHSs are symmetric and positive definite. Symmetry
means

```{math}
\kappa(x_i,x_j)=\kappa(x_j,x_i).
```

Positive definiteness means that, for any $n \in \mathbb{N}$, any points
$x_1,\ldots,x_n \in X$, and any coefficients
$\alpha_1,\ldots,\alpha_n \in \mathbb{R}$,

```{math}
\sum_{i=1}^n \sum_{j=1}^n
\alpha_i\alpha_j\kappa(x_i,x_j)
\ge 0.
```

Equivalently, every Gram matrix $K \in \mathbb{R}^{n\times n}$ with entries

```{math}
K_{ij} = \kappa(x_i,x_j)
```

is positive semidefinite.

(rkhs:construction)=
## Constructing the RKHS

Start with the set of all finite linear combinations of kernel sections:

```{math}
H_0 =
\left\{
f : f(\cdot)=\sum_{i=1}^n \alpha_i \kappa(\cdot,x_i),
\ \alpha_i \in \mathbb{R},\ x_i \in X,\ n \in \mathbb{N}
\right\}.
```

This is a vector space. Define the inner product first on kernel sections by

```{math}
\left\langle \kappa(\cdot,x_i),\kappa(\cdot,x_j)\right\rangle_{H_0}
=
\kappa(x_i,x_j),
```

and extend it bilinearly. Thus, for

```{math}
f(\cdot)=\sum_{i=1}^n \alpha_i \kappa(\cdot,x_i),
\qquad
g(\cdot)=\sum_{j=1}^m \beta_j \kappa(\cdot,z_j),
```

define

```{math}
\langle f,g\rangle_{H_0}
=
\sum_{i=1}^n \sum_{j=1}^m
\alpha_i\beta_j\kappa(x_i,z_j)
=
\alpha^T K_{xz}\beta.
```

If the kernel is only positive semidefinite, different coefficient
representations can describe the same zero-norm function. The rigorous
construction quotients out zero-norm elements before completing the space. Once
that identification is made, the completion

```{math}
H = \overline{H_0}
```

is the RKHS associated with $\kappa$.

The Moore-Aronszajn theorem states the two-way correspondence: every symmetric
positive-definite kernel has a unique RKHS for which it is the reproducing
kernel, and every RKHS has a unique symmetric positive-definite reproducing
kernel.

(rkhs:reproducing)=
## The Reproducing Property

The defining property of an RKHS is that evaluating a function at a point is the
same as taking an inner product with a kernel section:

```{math}
:label: eq:rkhs-reproducing-property

f(x) = \langle f,\kappa(\cdot,x)\rangle_H.
```

For $f \in H_0$ with

```{math}
f(\cdot)=\sum_{i=1}^n \alpha_i\kappa(\cdot,x_i),
```

the identity follows directly:

```{math}
\begin{aligned}
\langle f,\kappa(\cdot,x)\rangle_{H_0}
&=
\left\langle
\sum_{i=1}^n \alpha_i\kappa(\cdot,x_i),
\kappa(\cdot,x)
\right\rangle_{H_0} \\
&=
\sum_{i=1}^n \alpha_i \kappa(x_i,x) \\
&=
f(x).
\end{aligned}
```

Continuity extends the identity to all $f \in H$. This property is the basis of
kernel methods: a function can be manipulated through coefficients and kernel
evaluations rather than through an explicit coordinate representation.

(rkhs:norm-metric)=
## Norms, Metrics, and Smoothness

The RKHS inner product induces an RKHS norm. For a single kernel section,

```{math}
\|\kappa(\cdot,x)\|_H
=
\sqrt{\langle \kappa(\cdot,x),\kappa(\cdot,x)\rangle_H}
=
\sqrt{\kappa(x,x)}.
```

For a finite kernel expansion

```{math}
f(\cdot)=\sum_{i=1}^n \alpha_i\kappa(\cdot,x_i),
```

the norm is

```{math}
\|f\|_H^2 = \alpha^T K\alpha,
\qquad
K_{ij}=\kappa(x_i,x_j).
```

The induced distance between two kernel sections is

```{math}
\begin{aligned}
d_H\!\left(\kappa(\cdot,x_i),\kappa(\cdot,x_j)\right)^2
&=
\|\kappa(\cdot,x_i)-\kappa(\cdot,x_j)\|_H^2 \\
&=
\kappa(x_i,x_i)+\kappa(x_j,x_j)-2\kappa(x_i,x_j).
\end{aligned}
```

For general finite expansions

```{math}
f(\cdot)=\sum_{i=1}^n \alpha_i\kappa(\cdot,x_i),
\qquad
g(\cdot)=\sum_{j=1}^m \beta_j\kappa(\cdot,z_j),
```

the distance is

```{math}
d_H(f,g)
=
\sqrt{
\alpha^T K_{xx}\alpha
+ \beta^T K_{zz}\beta
- 2\alpha^T K_{xz}\beta
}.
```

The RKHS norm also controls pointwise variation. Using the reproducing property
and the Cauchy-Schwarz inequality,

```{math}
\begin{aligned}
|f(x)-f(x')|
&=
\left|
\left\langle
f,\kappa(\cdot,x)-\kappa(\cdot,x')
\right\rangle_H
\right| \\
&\le
\|f\|_H\,
\|\kappa(\cdot,x)-\kappa(\cdot,x')\|_H.
\end{aligned}
```

Thus, when the kernel sections vary smoothly with $x$, functions with small
RKHS norm also vary smoothly. This is why RKHS norms naturally appear as
regularizers in kernel regression.

(rkhs:mercer)=
## Mercer Representation

Mercer's theorem gives a spectral view of kernels. Under appropriate
conditions, such as compact $X$ and continuous positive-definite $\kappa$, the
kernel defines an integral operator

```{math}
[T_\kappa f](x)
=
\int_X \kappa(x,z) f(z)\,\dd z.
```

This operator acts on $L^2(X)$ and has eigenfunctions $\varphi_i$ and positive
eigenvalues $\sigma_i$ satisfying

```{math}
T_\kappa\varphi_i = \sigma_i\varphi_i.
```

For compact, self-adjoint, positive operators of this type, the eigenvalues can
be arranged as a countable decreasing sequence with $\sigma_i \to 0$, and the
eigenfunctions form an orthonormal basis of $L^2(X)$ on the range relevant to
the kernel. The kernel has the Mercer expansion

```{math}
\kappa(x,y)
=
\sum_{i=1}^{\infty}
\sigma_i \varphi_i(x)\varphi_i(y),
```

with uniform convergence under the standard Mercer assumptions.

The associated RKHS can then be described by weighted square summability:

```{math}
H =
\left\{
f \in L^2(X)
\;:\;
\sum_{i=1}^{\infty}
\frac{\langle f,\varphi_i\rangle_{L^2}^2}{\sigma_i}
< \infty
\right\}.
```

Its inner product is

```{math}
\langle f,g\rangle_H
=
\sum_{i=1}^{\infty}
\frac{
\langle f,\varphi_i\rangle_{L^2}
\langle g,\varphi_i\rangle_{L^2}
}{\sigma_i}.
```

Small eigenvalues are penalized strongly. Therefore the kernel determines which
directions in function space are cheap or expensive in the RKHS norm.

(rkhs:examples)=
## Examples

### Linear Kernel

Let

```{math}
\kappa(x,y)=xy,
\qquad
x,y \in [0,1].
```

Positive definiteness follows from

```{math}
\sum_{i,j=1}^n \alpha_i\alpha_j\kappa(x_i,x_j)
=
\left(\sum_{i=1}^n \alpha_i x_i\right)^2
\ge 0.
```

The RKHS consists of one-dimensional linear functions through the origin:

```{math}
H = \{f : f(x)=ax,\ a\in\mathbb{R}\}.
```

The corresponding integral operator is

```{math}
[T_\kappa f](x)
=
\int_0^1 xy f(y)\,\dd y
=
\left(\int_0^1 y f(y)\,\dd y\right)x.
```

Its normalized eigenfunction is $\varphi(x)=\sqrt{3}x$ with eigenvalue
$\sigma=1/3$, so this RKHS is one-dimensional.

### Polynomial Kernel

Let

```{math}
\kappa(x,y)=(1+xy)^2,
\qquad
x,y \in [-1,1].
```

With the feature map

```{math}
\phi(x)=
\begin{bmatrix}
1\\
\sqrt{2}x\\
x^2
\end{bmatrix},
```

we have

```{math}
\kappa(x,y)=\phi(x)^T\phi(y).
```

Therefore

```{math}
\sum_{i,j=1}^n \alpha_i\alpha_j\kappa(x_i,x_j)
=
\left\|
\sum_{i=1}^n \alpha_i\phi(x_i)
\right\|^2
\ge 0.
```

The RKHS is the space of polynomials of degree at most two on $[-1,1]$:

```{math}
H =
\{f : f(x)=a^T\phi(x),\ a\in\mathbb{R}^3\}.
```

Finite-dimensional feature maps always produce finite-dimensional RKHSs.

### Brownian Motion Kernel

Let

```{math}
\kappa(x,x')=\min(x,x'),
\qquad
x,x'\in[0,1].
```

This kernel can be written as an $L^2$ inner product of indicator functions:

```{math}
\kappa(x,x')
=
\int_0^1 \mathbf{1}_{[0,x]}(t)\mathbf{1}_{[0,x']}(t)\,\dd t.
```

The associated RKHS is the Sobolev-type space

```{math}
H =
\left\{
f : [0,1]\to\mathbb{R}
\;:\;
f \text{ is absolutely continuous},\
f' \in L^2[0,1],\
f(0)=0
\right\},
```

with inner product

```{math}
\langle f,g\rangle_H
=
\int_0^1 f'(x)g'(x)\,\dd x.
```

Because $\partial_t\kappa(t,x)=\mathbf{1}_{[0,x]}(t)$ almost everywhere,

```{math}
\langle f,\kappa(\cdot,x)\rangle_H
=
\int_0^1 f'(t)\mathbf{1}_{[0,x]}(t)\,\dd t
=
\int_0^x f'(t)\,\dd t
=
f(x).
```

The Mercer eigenproblem can be reduced to an ordinary differential equation,
giving eigenvalues

```{math}
\sigma_i =
\left(\frac{2}{(2i-1)\pi}\right)^2,
\qquad
i=1,2,\ldots,
```

with sine eigenfunctions after normalization.

### Translation-Invariant Periodic Kernels

Suppose

```{math}
\kappa(x,y)=\psi(x-y),
```

where $\psi$ is even and $2\pi$-periodic. Over one period, the eigenfunctions
are Fourier modes. The kernel expansion becomes a cosine series,

```{math}
\kappa(x,y)
=
\psi(x-y)
=
\sum_{n=0}^{\infty}
\lambda_n\cos(n(x-y)).
```

The kernel is positive definite when the Fourier coefficients
$\lambda_n$ are nonnegative. The RKHS consists of periodic functions whose
Fourier coefficients are square-summable with weights $\lambda_n^{-1}$.

(rkhs:krr)=
## Kernel Ridge Regression

The RKHS view explains kernel ridge regression. Given data

```{math}
\{(x_i,y_i)\}_{i=1}^n
```

and a kernel $\kappa$, choose a model in the finite span of kernel sections:

```{math}
f(\cdot)
=
\sum_{i=1}^n \alpha_i\kappa(\cdot,x_i).
```

At the training inputs,

```{math}
f(x_j)
=
\sum_{i=1}^n \alpha_i\kappa(x_i,x_j)
=
[K\alpha]_j.
```

Least squares over the coefficients is

```{math}
\min_\alpha \|K\alpha-y\|_2^2.
```

The RKHS norm adds a smoothness penalty:

```{math}
\min_\alpha
\|K\alpha-y\|_2^2
+ \lambda \|f\|_H^2.
```

Since

```{math}
\|f\|_H^2 = \alpha^T K\alpha,
```

the regularized objective becomes

```{math}
\min_\alpha
\|K\alpha-y\|_2^2
+ \lambda \alpha^T K\alpha.
```

When $K$ is invertible, the normal equations give the familiar solution

```{math}
\alpha = (K+\lambda I)^{-1}y.
```

The representer theorem gives the broader justification: for many regularized
empirical-risk problems over an RKHS, an optimizer exists in the span of the
kernel sections at the training points.
