# Weighted Incidence Structures

**A mathematical framework for universal optimal encoding.**

<div class="grid cards" markdown>

-   :fontawesome-solid-file-pdf: **Read the paper**

    Full monograph in PDF
    (204 pages, 34 chapters)

    [:octicons-arrow-right-24: Download](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)

-   :fontawesome-brands-github: **GitHub**

    Source code, issues, contributions

    [:octicons-arrow-right-24: Repository](https://github.com/fabriziobiondi/wis-theory)

-   :fontawesome-solid-book: **Documentation**

    Theory, definitions, examples, FAQ

    [:octicons-arrow-right-24: Browse](theory/overview.md)

-   :fontawesome-solid-flask: **Examples**

    AES, geo-indistinguishability, differential privacy

    [:octicons-arrow-right-24: Explore](examples.md)

-   :fontawesome-solid-lightbulb: **Open Problems**

    Structural, geometric, algorithmic, applications

    [:octicons-arrow-right-24: See](open-problems.md)

-   :fontawesome-solid-map: **Current Status**

    What is done, what remains

    [:octicons-arrow-right-24: Track](roadmap.md)

</div>

---

## Abstract

**Problem.** A deterministic encryption system is *universally optimal* if, after observing the ciphertext, every compatible message is equally likely. Despite decades of study, the full set of such systems—and their geometric structure—remained unknown.

**Main theorem.** A deterministic encoder is universally optimal if and only if its multiplicity matrix admits a factorisation $n_{mc} = \beta(c) / w(m)$ into message and ciphertext weights.

**Main consequence.** The Universal Optimality Defect (UOD) is the squared norm in the forced Hilbert-space geometry. Every information-theoretic quantity is Lipschitz continuous with respect to the UOD, with explicit constants.

---

## Key results

| Result | Chapter | Statement |
|--------|---------|-----------|
| **Representation Theorem** | 5 | $E$ universally optimal $\iff n_{mc} = \beta(c)/w(m)$ |
| **Cycle factorisation** | 4 | Existence of WIS weights $\iff$ alternating edge products agree on every cycle |
| **Universal Lipschitz bound** | 15 | $|S(P)-S(Q)| \le L\sqrt{\mathcal D(P,Q)}$ |
| **Three-Level Theorem** | 25 | Critical points of $\mathcal D$ collapse to $3$ values |

---

## The logical chain

```
Universally Optimal Encoder
        │
        ▼
Multiplicity Matrix  n_mc
        │
        ▼
Weighted Incidence Structure  (w, β)
        │
        ▼
Gauge Class  [w, β]
        │
        ▼
Mismatch Operator  Φ = [A  −C]
        │
        ▼
Least-Squares Problem  min ‖Au − ω‖²
        │
        ▼
Normal Operator  ΦᵀΦ
        │
        ▼
Posterior Laplacian  L = AᵀQA
        │
        ▼
Quotient Geometry  V_I / Im(C)
        │
        ▼
Universal Optimality Defect  D(P)
```
