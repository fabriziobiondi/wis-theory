# Examples

## AES S-box

The main running example throughout the monograph. The AES S-box is a $16 \times 16$ lookup table that realises a universally optimal encoder. Each message-ciphertext pair is unique, and every posterior is a Dirac mass. The UOD is zero; the system achieves perfect secrecy.

[Details in Chapter 1](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)

## Browser fingerprinting

The Panopticlick study analysed how uniquely browsers are identified by their configuration. Each browser corresponds to an incidence structure where the messages are browsers and the ciphertexts are configuration vectors. The WIS framework explains why small anonymity sets produce large UOD values.

[Details in Chapter 1](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)

## Geo-indistinguishability

A location-privacy mechanism perturbing GPS coordinates. The WIS is continuous (not discrete), and the UOD measures how distinguishable two nearby locations are. The Laplace mechanism achieves $\mathcal D = 2/\varepsilon^2$.

[Details in Chapter 1](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)

## Differential privacy

Adding Laplace noise to a database query makes neighbouring databases incognisable. The UOD measures distinguishability; the classical Laplace mechanism achieves the optimal UOD for a given $\varepsilon$.

[Details in Chapter 1](https://github.com/fabriziobiondi/wis-theory/raw/main/paper/main.pdf)
