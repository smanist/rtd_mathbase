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

## Chapter Sections

- {doc}`Vector Spaces <vector_spaces>` introduces the algebraic layer: bases,
  dimension, linear maps, matrices, rank, kernels, images, and quotients.
- {doc}`Metrics and Norms <metrics_norms>` adds distance and magnitude, while
  separating metric structure from normed vector space structure.
- {doc}`Inner Product Spaces <inner_product_spaces>` adds angles, projections,
  orthogonal maps, adjoints, spectral decompositions, and singular values.
- {doc}`Pre-Hilbert and Hilbert Spaces <hilbert_spaces>` adds the limiting
  structure needed for complete inner product spaces.

```{toctree}
:hidden:

vector_spaces
metrics_norms
inner_product_spaces
hilbert_spaces
```

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
