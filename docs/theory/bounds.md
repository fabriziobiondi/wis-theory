# Universal Bounds

## The problem

Given two posterior distributions $P$ and $Q$ on the manifold, how much can an information-theoretic quantity change?

## The answer

Every sufficiently regular functional $S: \mathcal P \to \mathbb R$ satisfies two universal bounds:

### Lipschitz bound

\[
|S(P) - S(Q)| \le L_S \sqrt{\mathcal D(P,Q)},
\]

where $L_S = \sup_{P \in \mathcal P} \|\nabla_g S(P)\|_g$ is the Lipschitz constant of $S$ with respect to the manifold metric.

### Quadratic bound

For smooth functionals:

\[
|S(P) - S(Q) - \langle \nabla_g S(Q), \exp^{-1}_Q(P) \rangle_g| \le \frac{M_S}{2} \mathcal D(P,Q),
\]

where $M_S$ bounds the Hessian of $S$.

## Why this matters

- The bounds are **universal**: they apply to every functional whose gradient norm is bounded.
- The constants depend only on the incidence structure, not on the functional.
- For Bregman divergences, the inequalities become **exact identities** through the **Average Hessian Operator**:

\[
D_\phi(P,Q) = \frac12 \Delta^{\mathsf T} \overline H_\phi(P,Q) \Delta.
\]

## What functionals are covered

| Type | Examples | Lipschitz constant |
|------|----------|-------------------|
| **Smooth** | Shannon, Rényi, $g$-entropy, KL, $\chi^2$ | $L_S = \sup_P \|H_P^{-1} \nabla S(P)\|$ |
| **Piecewise-smooth** | Min-entropy, Bayes vulnerability, guessing entropy | $L_S$ computed per region |
| **Rank-based** | Any functional depending only on posterior ordering | $L_S$ via transition times |

## Key references

- [Chapter 13 (Entropy Bounds)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
- [Chapter 15 (Universal Geometric Bounds)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
- [Chapter 16 (Average Hessian Operator)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
