# Hilbert Geometry and the UOD

## The problem

The factorisation $n_{mc} = \beta(c)/w(m)$ is multiplicative. How do we turn it into a linear, geometric problem?

## Logarithmic linearisation

Take logarithms:

\[
\log n_{mc} = v(c) - u(m), \qquad u = \log w,\; v = \log \beta.
\]

This additive structure defines the **mismatch operator**

\[
\Phi(u,v) = Au - Cv,
\]

where $A$ and $C$ are the incidence matrices. The factorisation problem becomes: does $\omega = \log n$ lie in the image of $\Phi$?

## Least-squares formulation

The squared norm $\|\Phi(u,v)\|^2$ defines a quadratic energy. Its minimiser is the projection of $\omega$ onto $\operatorname{Im}(\Phi)$. The **normal operator**

\[
\Phi^{\mathsf T}\Phi = \begin{pmatrix} D_M & -A \\ -A^{\mathsf T} & D_C \end{pmatrix}
\]

has a Schur complement that is the **posterior Laplacian**

\[
L = A^{\mathsf T} Q A = D_M - A D_C^{-1} A^{\mathsf T},
\]

where $Q$ is the canonical projection onto the gauge quotient.

## Universal Optimality Defect

The **Universal Optimality Defect** (UOD) is the squared distance from a distribution to the set of universally optimal ones:

\[
\mathcal D(P) = \|\delta(P)\|^2 = \min_{u,v} \|\Phi(u,v) - \omega(P)\|^2.
\]

Zero means the system is perfectly secret. Larger values quantify the leakage.

## Key properties

- **Convex**: the energy is strictly convex modulo the gauge direction.
- **Stable**: small changes in the encoder produce small changes in the UOD (Lipschitz continuity).
- **Geometric**: the UOD is the squared norm in a quotient Hilbert space, giving it a natural Riemannian structure.

## Key references

- [Chapter 6 (Logarithmic Linearisation)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
- [Chapter 7 (Hilbert Geometry)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
- [Chapter 8–10 (Posterior Manifold and Projection)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
- [Chapter 11 (Pullback Metric)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
