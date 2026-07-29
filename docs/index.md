# Weighted Incidence Structures

**A mathematical framework for universal optimal encoding.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/fabriziobiondi/wis-theory/blob/main/LICENSE)

---

## Overview

A deterministic encryption system is *universally optimal* if, after observing the ciphertext, every compatible message is equally likely. This monograph provides a complete classification of such systems, together with a canonical Hilbert-space geometry that emerges inevitably from the combinatorial data.

The key insight: the logarithmic representation of the multiplicity matrix transforms a multiplicative factorisation into an additive linear structure, opening the door to operator theory, spectral geometry, and universal bounds for information-theoretic quantities.

---

## Main paper

[📄 Download the full monograph (PDF, 204 pages)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)

### Abstract

**Problem.** A deterministic encryption system is universally optimal if, after observing the ciphertext, every compatible message is equally likely. Despite decades of study, the full set of such systems—and their geometric structure—remained unknown.

**Main theorem.** A deterministic encoder is universally optimal if and only if its multiplicity matrix admits a factorisation $n_{mc} = \beta(c) / w(m)$ into message and ciphertext weights. Taking logarithms transforms this multiplicative factorisation into a linear condition, forcing a canonical Hilbert-space geometry on every such system.

**Main consequence.** The Universal Optimality Defect (UOD) $\mathcal D(P) = \|\delta(P)\|^2$ is the squared norm in this forced geometry. Every information-theoretic quantity (Shannon entropy, Rényi entropy, min-entropy, Bayes vulnerability, guessing entropy) is Lipschitz continuous with respect to the UOD, with explicit constants that depend only on the system's incidence structure.

**Practical impact.** The UOD provides a quantitative tool for evaluating real-world encryption systems—side-channel resistance, anonymity set size, privacy–utility trade-offs—replacing the binary verdict of perfect secrecy with a continuous scale.

---

## Key results

| Result | Statement | Chapter |
|--------|-----------|---------|
| **Representation Theorem** | $E$ is universally optimal $\iff$ $n_{mc} = \beta(c)/w(m)$ | 5 |
| **Cycle factorisation** | Existence of WIS weights $\iff$ cycle product $= 1$ | 4 |
| **Universal Lipschitz bound** | $\|S(P) - S(Q)\| \le L \sqrt{\mathcal D(P,Q)}$ | 15 |
| **Three-Level Theorem** | Critical points of $\mathcal D$ collapse to 3 values | 25 |
| **Bregman identity** | $D_\phi(P,Q) = \frac12 \Delta^{\mathsf T} \overline H_\phi \Delta$ | 16 |

---

## Repository structure

```
wis-theory/
├── paper/           # Monograph source (LaTeX + PDF)
├── code/            # Computational companion (Apollonian framework)
├── examples/        # Example configurations and data
├── docs/            # This documentation site
└── references/      # External references and notes
```

---

## License

This work is licensed under the MIT License.

## Contact

Fabrizio Biondi — `biondif@gmail.com`

<!-- GitHub Pages: https://fabriziobiondi.github.io/wis-theory/ -->
