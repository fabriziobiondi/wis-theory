# Variational Structure

## The problem

The UOD $\mathcal D(P)$ defines a function on the posterior manifold. What are its critical points? How many distinct values can they take?

## The Three-Level Theorem

The central result of Part V (Chapter 25):

> Every interior critical point of the UOD $\mathcal D(P, U_n)$ on the posterior manifold $\mathcal P$ has a stationarity function $\varphi$ that takes at most **three distinct values**.

This collapse from $n$ (the dimension of the simplex) to $3$ is the signature of the quadratic energy. It has no analogue in classical information geometry.

## What this implies

- The critical points of $\mathcal D$ are completely classified.
- The optimisation problem reduces from a high-dimensional search to a finite algebraic system.
- The three values satisfy explicit equations derived from the Chebyshev structure of the stationarity function.

## Extended Chebyshev structure

The stationarity function $\varphi$ belongs to an **Extended Chebyshev system** (Section \u201cExtended Chebyshev Structure\u201d, Chapter 25). This gives:

- A **Wronskian condition** characterising admissible triples $(\varphi_1, \varphi_2, \varphi_3)$.
- **Explicit bounds** on the number of critical points.
- **Bifurcation analysis**: the pitchfork bifurcations at the boundary of the admissible region.

## Related results

- **Boundary behaviour**: critical points at the boundary of the simplex correspond to collapsed message classes.
- **Gradient flow**: the UOD gradient flow converges to a critical point (the Three-Level Theorem constrains the limit set).
- **Comparison geometry**: the UOD geometry is compared with Fisher, Hellinger, $\chi^2$, and optimal transport.

## Key references

- [Chapter 22 (Differential Theory of the UOD)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
- [Chapter 24 (Comparative Geometry)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
- [Chapter 25 (Variational Structure)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
