# WIS and Representation

## The problem

When does an encryption system produce ciphertexts that reveal nothing about the message? Shannon's perfect secrecy requires that the ciphertext be independent of the message. But what mathematical structure is forced by this requirement?

## The answer

A deterministic encoder $E: \mathcal M \times \mathcal K \to \mathcal C$ is *universally optimal* if and only if its multiplicity matrix $n_{mc}$ (the number of keys mapping $m$ to $c$) admits a factorisation

\[
n_{mc} = \frac{\beta(c)}{w(m)} \qquad\text{for every }(m,c)\in I,
\]

where $w: \mathcal M \to \mathbb R_{>0}$ and $\beta: \mathcal C \to \mathbb R_{>0}$ are positive weight functions. This is the **Representation Theorem** (Chapter 5).

## Why this matters

- The factorisation separates the contribution of the message (through $w$) from the contribution of the ciphertext (through $\beta$).
- The only ambiguity is a global scaling: $(w,\beta)$ and $(\lambda w, \lambda^{-1}\beta)$ produce the same multiplicities. This *gauge symmetry* defines a quotient space.
- The **cycle factorisation criterion** (Chapter 4) gives a purely graph-theoretic test: around every simple cycle, the alternating products of edge multiplicities must agree.

## Encoder realizability

A weighted incidence structure corresponds to an actual encoder if and only if two conditions hold (Chapter 4):

1. **Integrality**: $\beta(c)/w(m) \in \mathbb N$ for every incidence.
2. **Balance**: there exists $K>0$ such that $B\beta = K w$.

## Key references

- [Chapter 4 (WIS)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
- [Chapter 5 (Representation)](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
