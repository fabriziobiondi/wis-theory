# FAQ

## What is a Weighted Incidence Structure?

A weighted incidence structure $\mathfrak W = (\mathcal M, \mathcal C, I, w, \beta)$ is a bipartite graph with vertex weights: messages $m \in \mathcal M$ have weight $w(m)$, ciphertexts $c \in \mathcal C$ have weight $\beta(c)$. The edge multiplicity is $n_{mc} = \beta(c)/w(m)$.

## What is universal optimality?

A deterministic encoder is universally optimal if, after observing the ciphertext, every compatible message is equally likely. This is a stronger condition than Shannon's perfect secrecy (which requires *all* messages to be equiprobable, not just the compatible ones).

## What is the UOD?

The Universal Optimality Defect (UOD) measures how far a distribution is from the set of universally optimal ones. Zero means perfect secrecy; larger values indicate leakage.

## Why is the geometry forced?

The logarithmic representation $n_{mc} = \beta(c)/w(m)$ becomes $v(c) - u(m) = \log n_{mc}$. This additive structure defines a linear operator $\Phi$, and from it the Hilbert-space geometry follows by standard operator theory. No choices are made—every construction is forced by the factorisation.

## Is the UOD computable?

Yes. The UOD is the solution of a least-squares problem that reduces to linear algebra on the incidence graph. The computational load is polynomial in the size of the message and ciphertext spaces.

## How does the UOD compare with differential privacy?

The UOD for the Laplace mechanism equals $6/\varepsilon^2$. The geometric Lipschitz bound recovers the optimal privacy–utility trade-off. The UOD is a generalisation that applies to any deterministic encoder, not just to mechanisms adding noise.
