# Weighted Incidence Structures (WIS)

**Geometry, Information, and Cryptography**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-blue)](LICENSE)
[![DOI](https://img.shields.io/badge/DOI-10.5281/zenodo.XXXXXXX-blue)](https://doi.org/10.5281/zenodo.XXXXXXX)
[![Pages](https://img.shields.io/badge/GitHub%20Pages-online-success)](https://fabriziobiondi.github.io/wis-theory/)
[![arXiv](https://img.shields.io/badge/arXiv-XXXX.XXXXX-b31b1b)](https://arxiv.org/abs/XXXX.XXXXX)
[![Paper](https://img.shields.io/badge/PDF-204%20pages-red)](paper/main.pdf)
![Status](https://img.shields.io/badge/status-stable-green)

A complete classification of universally optimal deterministic encoders, together with the forced Hilbert-space geometry that emerges from their algebraic structure.

---

## Abstract

A deterministic encryption system is *universally optimal* if, after observing the ciphertext, every compatible message is equally likely. This monograph provides:

- A **complete classification** of all universally optimal deterministic encoders through weighted incidence structures.
- A **forced Hilbert-space geometry** where the Universal Optimality Defect (UOD) measures the distance from perfect secrecy.
- **Universal Lipschitz and quadratic bounds** for every smooth and piecewise-smooth information functional.
- A **Three-Level Theorem** showing that interior critical points of the UOD collapse to at most three distinct log-likelihood values.

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

---

## Quick links

| What | Where |
|------|-------|
| 📄 **Read the paper** | [`paper/main.pdf`](paper/main.pdf) (204 pages) |
| 🌐 **Documentation site** | [fabriziobiondi.github.io/wis-theory](https://fabriziobiondi.github.io/wis-theory/) |
| 📖 **Theory overview** | [docs/theory/overview.md](docs/theory/overview.md) |
| 💡 **Examples** | [docs/examples.md](docs/examples.md) |
| ❓ **FAQ** | [docs/faq.md](docs/faq.md) |
| 🔮 **Open problems** | [docs/open-problems.md](docs/open-problems.md) |
| 📋 **Current status** | [docs/roadmap.md](docs/roadmap.md) |

---

## Repository structure

```
wis-theory/
├── paper/                  # Monograph source (LaTeX + PDF)
│   ├── main.pdf            # Compiled monograph
│   ├── main.tex            # Main LaTeX file
│   ├── chapters/           # 34 chapter sources
│   └── figures/            # Diagrams and illustrations
├── docs/                   # MkDocs documentation site
│   ├── index.md            # Homepage (with buttons)
│   ├── theory/             # Theory pages (5 areas)
│   ├── examples.md         # Running examples
│   ├── faq.md              # Frequently asked questions
│   ├── roadmap.md          # Current status tracker
│   └── open-problems.md    # Future directions
├── code/                   # Computational companion
├── examples/               # Example configurations
├── notebooks/              # Jupyter notebooks
├── references/             # External references
└── .github/workflows/      # CI/CD (deploy to Pages)
```

---

## Key results

| Result | Chapter | Statement |
|--------|---------|-----------|
| **Representation Theorem** | 5 | \(E\) universally optimal \(\iff n_{mc} = \beta(c)/w(m)\) |
| **Cycle factorisation** | 4 | Existence of WIS weights \(\iff\) cycle product \(= 1\) |
| **Encoder realizability** | 4 | Integrality + balance \(B\beta = Kw\) |
| **Universal Lipschitz bound** | 16 | \(\|S(P)-S(Q)\| \le L\sqrt{\mathcal D(P,Q)}\) |
| **Universal quadratic bound** | 16 | \(|S(P)-S(Q)| \le C\,\mathcal D(P,Q)\) for small defects |
| **Average Hessian Operator** | 17 | \(D_\phi(P,Q) = \frac12 \Delta^{\mathsf T} \overline H_\phi \Delta\) |
| **Three-Level Theorem** | 26 | Critical points of \(\mathcal D\) collapse to at most \(3\) values |
| **Stability** | 13 | \(\mathcal D\) is continuous and locally strictly convex |

---

## Citation

```bibtex
@book{biondi2026wis,
  author    = {Fabrizio Biondi},
  title     = {Weighted Incidence Structures: Geometry, Information, and Cryptography},
  year      = {2026},
  note      = {\url{https://github.com/fabriziobiondi/wis-theory}}
}
```

---

## License

The manuscript and documentation in the `paper/` directory are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).  
The source code in this repository is licensed under the [MIT License](LICENSE-MIT).

---

## Contact

Fabrizio Biondi — [`biondif@gmail.com`](mailto:biondif@gmail.com)
