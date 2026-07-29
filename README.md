# Weighted Incidence Structures

**Geometry, Information, and Cryptography**

A mathematical framework for universal optimal encoding.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)

---

## Overview

A deterministic encryption system is *universally optimal* if, after observing the ciphertext, every compatible message is equally likely. This monograph provides a complete classification of such systems, together with a canonical Hilbert-space geometry that emerges inevitably from the combinatorial data.

The key insight: the logarithmic representation of the multiplicity matrix transforms a multiplicative factorisation into an additive linear structure, opening the door to operator theory, spectral geometry, and universal bounds for information-theoretic quantities.

---

## Main paper

[📄 Read the paper](paper/main.pdf) (204 pages, 34 chapters)

### Abstract

**Problem.** A deterministic encryption system is universally optimal if, after observing the ciphertext, every compatible message is equally likely. Despite decades of study, the full set of such systems—and their geometric structure—remained unknown.

**Main theorem.** A deterministic encoder is universally optimal if and only if its multiplicity matrix admits a factorisation $n_{mc} = \beta(c) / w(m)$ into message and ciphertext weights.

**Main consequence.** The Universal Optimality Defect (UOD) is the squared norm in the forced Hilbert-space geometry. Every information-theoretic quantity (Shannon entropy, Rényi entropy, min-entropy, Bayes vulnerability, guessing entropy) is Lipschitz continuous with respect to the UOD, with explicit constants.

**Practical impact.** The UOD provides a quantitative tool for evaluating real-world encryption systems—side-channel resistance, anonymity set size, privacy–utility trade-offs—replacing the binary verdict of perfect secrecy with a continuous scale.

---

## Key results

| Result | Statement |
|--------|-----------|
| **Representation Theorem** | Universal optimality $\iff$ $n_{mc} = \beta(c)/w(m)$ |
| **Cycle factorisation criterion** | Graph-theoretic test for the existence of WIS weights |
| **Universal Lipschitz bound** | $\|S(P) - S(Q)\| \le L \sqrt{\mathcal D(P,Q)}$ for every smooth functional $S$ |
| **Three-Level Theorem** | Interior critical points of the UOD collapse to at most three distinct log-likelihood values |
| **Bregman identity** | $D_\phi(P,Q) = \frac12 \Delta^{\mathsf T} \overline H_\phi \Delta$ |

---

## Repository structure

```
wis-theory/
├── paper/           # Monograph source (LaTeX + PDF)
│   ├── main.pdf     # Compiled monograph
│   ├── main.tex     # Main LaTeX file
│   ├── chapters/    # Chapter sources (34 files)
│   └── figures/     # Diagrams and illustrations
├── code/            # Computational companion (Apollonian framework)
├── examples/        # Example configurations and data
├── notebooks/       # Jupyter notebooks for exploration
├── docs/            # Documentation site (MkDocs)
└── references/      # External references and notes
```

---

## Citation

```bibtex
@book{biondi2026wis,
  author    = {Fabrizio Biondi},
  title     = {Weighted Incidence Structures: Geometry, Information, and Cryptography},
  year      = {2026},
  note      = {Available at \url{https://github.com/fabriziobiondi/wis-theory}}
}
```

---

## License

This work is licensed under the MIT License — see [LICENSE](LICENSE) for details.

---

## Contact

Fabrizio Biondi — `biondif@gmail.com`

Comments, corrections, and suggestions are welcome.
