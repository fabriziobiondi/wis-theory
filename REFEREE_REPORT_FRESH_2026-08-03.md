# REFEREE REPORT FRESCO — WIS Book (03/08/2026, seconda revisione)

**Opera**: Weighted Incidence Structures: Geometry, Information, and Cryptography, v1.0.0
**Data**: 03/08/2026 (sera) — dopo il completamento della roadmap B01-B17 del mattino
**Metodo**: check automatici (struttura, ref, label, pattern stale) + verifica numerica
sympy/numpy (g-entropy, integrali, UOD, ratio tabelle) + lettura riga-per-riga delegata
(3 subagent: blocco A capp.1-5, B capp.6-12, C capp.13-19; A e C andati in timeout dopo
lettura integrale — i loro transcript confermano i finding diretti) + lettura diretta
capitoli 20-33.
**Stato**: SOLO LETTURA. Nessun file .tex modificato.
**Decisioni autore (Fase 0, confermate da Fabrizio)**: D1 = (a) caso speciale Tsallis
dichiarato (coppie (g,h) non-inverse ammesse; per Tsallis h(y)=e^{(1-α)y}); D2 = (i)
convenzione unica con Π esplicito: 𝒟 = ‖ΠY‖², Π proiettore ortogonale su Im(C)^⊥,
definito in stability e allineato a hilbert_geometry e notation.

---

## A. BUG matematici certi (da correggere)

### N01 — g-entropy: la voce Tsallis è incoerente con h = g^{-1}
- **File:riga**: smooth_functionals.tex L399-426 (definizione + tabella), L428-446
  (Teorema g-Entropy Gradient), L964-976 (costante L_Tsallis^2)
- **Severity**: BUG (decisione autore richiesta)
- **Descrizione**: con H_g(P) = g(Σ_i P_i h(-log P_i)) e h = g^{-1} dichiarato a L404
  e L430, la riga L416 "g(x) = (x-1)/(1-α) → Tsallis entropy" è FALSA. Per
  g(x)=(x-1)/(1-α) si ha h(y) = (1-α)y + 1, quindi Σ P_i h(-log P_i) = 1 + (1-α)H_Shannon
  e H_g = H_Shannon, non Tsallis. Verifica numerica: max |H_pesata - Tsallis| = 0.86
  (α=0.5), 0.80 (α=2), 1.11 (α=3) su 200 campioni; usando h(y)=e^{(1-α)y} (la h della
  Rényi) si ottiene Tsallis esatto (errore 1e-15) MA quella h NON è g^{-1} per quella g.
- **Conseguenze**: (a) il Teorema g-Entropy Gradient usa h=g^{-1} → per "Tsallis"
  calcola il gradiente di Shannon; (b) L426 "The Tsallis case is identical with
  g(x)=(x-1)/(1-α)" è falso; (c) L_Tsallis^2 (L973-976) è copiata dalla Rényi e non è
  derivata da un gradiente Tsallis valido; (d) introduction.tex L80 eredita la formula.
- **Fix proposto**: aggiungere il caso speciale "Tsallis: h(y)=e^{(1-α)y}, g(x)=(x-1)/(1-α),
  h ≠ g^{-1} qui" e trattarlo come caso speciale nel teorema del gradiente; oppure
  cambiare g per Tsallis; oppure rimuovere Tsallis dalla tabella unificata.
  Raccomandazione: opzione (a) — preserva la costante già scritta e l'unità della teoria.

### N02 — UOD: formula del difetto con proiettore invertito
- **File:riga**: hilbert_geometry.tex L233 (quote "Mathematical intuition") e
  notation.tex L38; propagazione in stability.tex L35 (vedi N03)
- **Severity**: BUG (verificato numericamente dal subagent blocco B)
- **Descrizione**: la quote scrive 𝒟(Y) = ‖q(Y)‖² = ‖Y - ΠY‖². Ma Π = I - C D_C^{-1} C^T
  è il proiettore ortogonale su Im(C)^⊥ (L78), quindi ‖q(Y)‖ = dist(Y, Im(C)) = ‖ΠY‖,
  e ‖Y - ΠY‖² è la norma della componente IN Im(C). Verifica numerica sull'Example 2:
  ‖ΠY'‖ = 0.3515 (valore usato correttamente a L329) vs ‖Y' - ΠY'‖ = 2.1662.
- **Fix**: sostituire ‖Y - ΠY‖² con ‖ΠY‖² nella quote e in notation.tex L38.

### N03 — stability.tex: Π non definito e formula incoerente col Thm 9-3
- **File:riga**: stability.tex L30-35 (proof continuità)
- **Severity**: BUG
- **Descrizione**: la formula 𝒟(P) = ‖(F(P)-F(P*)) - Π(F(P)-F(P*))‖² usa Π mai definito
  nel capitolo (né in capp. 10-11; in hilbert:78 Π è un proiettore su V_I). Inoltre è
  incoerente con la dimostrazione del Thm 9-3 (L91-95) che usa 𝒟(P) = g_{P*}(η,η) = ‖η‖²
  senza Π: coincidono solo se Π = Id. Stesso errore di identificazione di N02.
- **Fix**: definire Π (proiezione su Im(C)^⊥ o la mappa quoziente corretta per
  F(𝒫)) e allineare le due formule, oppure eliminare Π dalla formula e usare ‖η‖².

## B. Regressioni e ref errati

### N04 — Norme su funzionali a valori reali ricomparse
- **File:riga**: smooth_functionals.tex L26 (‖H(P)-H(P*)‖) e L394 (‖S(P)-S(P*)‖);
  piecewise_smooth.tex L98 (‖S(P)-S(P*)‖)
- **Severity**: BUG (regressione del fix "norma su scalari" del 3/8)
- **Descrizione**: H e S sono funzionali a valori reali → deve essere |H(P)-H(P*)| e
  |S(P)-S(P*)|. Le righe vicine della stessa sezione usano correttamente |.| (L24, L388).
- **Fix**: sostituire ‖·‖ con |·| in quei 3 punti.

### N05 — Auto-ref: smooth_functionals punta al proprio capitolo
- **File:riga**: smooth_functionals.tex L3 e L910
- **Severity**: BUG (ref errato)
- **Descrizione**: "compared with the piecewise-smooth bounds of
  Chapter~\ref{ch:sec:classical-smooth-information-functionals}" — quel label è il
  capitolo CORRENTE (Classical Smooth Functionals); il riferimento corretto è
  ch:sec:piecewise-smooth (introdotto dal fix Fase 4 dei Chapter~N).
- **Fix**: sostituire con \ref{ch:sec:piecewise-smooth} in entrambi i punti.

### N06 — Geo-indistinguishability: esempio numerico col vecchio 2/ε²
- **File:riga**: applications.tex L181-184 (esempio ε=0.5, n=100)
- **Severity**: BUG (regressione — il fix 6/ε² ha corretto la formula ma non l'esempio)
- **Descrizione**: formula a L165-172 corretta (6/ε²), ma l'esempio dice "𝒟 = 8 bits"
  e "H2 ≥ log₂100 - 8/100 ≈ 6.58". Con 𝒟 = 6/ε² = 24: bound = log₂100 - 24/100 = 6.40
  (non 6.58). Il valore 8 = 2/ε² è il vecchio.
- **Fix**: ricalcolare l'esempio: 𝒟 = 24 (nats) o convertire in bit; bound ≈ 6.40;
  rivedere "accurate to within 0.02 bits" e il valore "actual ≈ 6.60".

## C. WARN

1. **hilbert_geometry.tex L89, L137, L330** — Q usato senza definizione nel capitolo
   (proiettore = Π, mappa quoziente = q). L89 "Writing Q explicitly", L137 "ker L =
   {u : QA u = 0}" (deve essere ΠA u = 0 — la prova L142-145 usa Π), L330 "Q, quotient".
   Residuo classe B11 in righe diverse da quelle fixate.
2. **diffeomorphism_local.tex L69** — δ ricomparso come vettore di spostamento
   ("δ = P - Q"), ricreando il clash con δ(Y) = ‖q(Y)‖ scalare. Fix C1 (δ→η) regge in
   stability:91 ma qui va rinominato η.
3. **diffeomorphism_local.tex L69** — "𝒟 ≈ Σ δ_i²/P_i" non deriva dal calcolo mostrato:
   il termine del primo ordine è Q(δ_i/P_i) con norma² Σ(δ_i/P_i)² - (1/k)(Σδ_i/P_i)²;
   la scrittura δ_i²/P_i corrisponde alla metrica di Fisher, non alla pullback euclidea.
4. **pullback_metric.tex L2-7** — F riusata con dominio 𝒫 e codominio ∏_c T_{P_c}Δ_c^∘
   non definiti nel blocco; Thm 5-4 vale per fattore. Solo notazione fuorviante.
5. **variational.tex L289-296** (proof Corollary Two-Parameter Family) — conteggio
   confuso: "5 unknowns, 5 equations, one degree absorbed" non giustifica una famiglia
   a 2 parametri; la tesi regge solo contando le molteplicità intere p,q,r. Riscrivere
   il proof con conteggio onesto (verifica sympy su n=3).
6. **stability.tex L91-96** — 𝒟(P) = g_{P*}(η,η): η vive in F(𝒫), g_{P*} su T_{P*}𝒫;
   vale a meno di O(‖P-P*‖³) via DF_{P*}. Tesi corretta ma da esplicitare.
7. **stability.tex L144-145** — Thm 9-4 vacuo nel caso AES degenere (𝒟≡0); qualificare.

## D. INFO (da non fixare salvo indicazione)

1. linearization.tex L13-16 — frammento di frase orfano ("which is the bridge...").
2. linearization.tex L11 — "Φ sarà l'oggetto centrale dei Capitoli 7 e 8": in cap. 8 Φ
   non compare.
3. posterior_manifold.tex L186 — esempio DP: W_P con π_i invece di P_i; k per n.
4. pullback_metric.tex L140 — "g_P(u,v) ≈ (ε²/2)⟨u,v⟩" non derivato; scala in tensione
   con 𝒟=6/ε².
5. stability.tex L143 — paragrafo "Outlook." vuoto.
6. introduction.tex L152, analytic_theory.tex L4, representation.tex L82 — auto-ref
   descrittivi ("this chapter (Chapter~\ref{proprio-label})"): compilano, ridondanti.

## E. Teoremi verificati CORRETTI (blocco B, 26)

linearization: Prop potential, Prop canonical lifting, Thm mismatch, Thm operator-WIS.
hilbert_geometry: Thm normal equations, Thm convexity, Cor global-min, Cor critical-points,
Lemma kernel-Φ, Lemma nullspace Hessian (con Q→Π), Lemma ker(ΦᵀΦ)=kerΦ, Thm strict
convexity mod gauge, Cor unique-min, Thm stability, Thm quotient-Hilbert, Thm characterisation.
posterior_manifold: Prop 1-1/1-2/1-3, Thm 1-4/1-5, Prop 2-1/2-1-dim/2-2/2-3, Cor 2-4,
Prop 2-5, Thm 3-2, Cor 3-3.
projection: Prop 4-1/4-2, Cor 4-3, Thm 4-4, Def 4-5, Cor 4-6.
diffeomorphism_local: Prop 5-1/5-2, Cor 5-3, Thm 5-4 (locale), Cor 5-5.
pullback_metric: Prop 7-1/7-3/7-4/7-5, Thm 7-6, Cor 7-7.
stability: Prop 9-1/9-2, Thm 9-3 (tesi corretta), Thm 9-4 (vacuo nel caso degenere), Cor 9-5.

Verifiche numeriche confermate: autovalori ΦᵀΦ 0.3820/1.3820/2.6180/3.6180, σ_min⁺=0.6180,
C=1.6180, δ Ex2=0.3515, Ex3 δ=0.1839/δ²=0.0338, ciclo 2·6=3·4. Tabelle F2 ricalcolate
(D one-heavy 46.39/5.35/51.68/51.35/43.89; ratio Lipschitz 11-590×, quadratico 12-32×).
Mix network: log₂100 - 2.5 = 4.14 ✓. Hessian KL = e^{x-n}(x-y+2) ✓. Wronskian e^{2x} ✓.
Integrale planar Laplace 6/ε² ✓. g-entropy: Shannon ✓, Rényi ✓, Tsallis ✗ (N01).

---

## ROADMAP DETTAGLIATA

### Fase 0 — Decisioni autore (richieste, nessun fix prima)
- **D1. Tsallis/g-entropy (N01)**: scegliere (a) caso speciale h=e^{(1-α)y} dichiarando
  h≠g^{-1}, (b) cambiare g, (c) togliere Tsallis dalla tabella. Raccomando (a).
- **D2. Formula del difetto (N02/N03)**: confermare che 𝒟 = ‖ΠY‖² (distanza da Im(C))
  e che Π è il proiettore ortogonale su Im(C)^⊥; decidere come definirlo in stability.

### Fase 1 — Fix meccanici immediati (rischio basso, ~1h)
1. N04: |·| al posto di ‖·‖ in smooth_functionals L26/L394, piecewise_smooth L98.
2. N05: ref a ch:sec:piecewise-smooth in smooth_functionals L3/L910.
3. N06: ricalcolo esempio geo (𝒟=24 o in bit; bound 6.40; testo "accurate to...").
4. N02: ‖ΠY‖² in hilbert_geometry L233 e notation.tex L38.
5. C1: rimuovere la frase orfana in linearization L13-16; C5: paragrafo "Outlook." vuoto.

### Fase 2 — BUG matematici con verifica (rischio medio)
6. N01: riscrivere la sezione g-entropy secondo D1 (definizione, tabella, teorema del
   gradiente, L_Tsallis^2, introduction L80) — verifica sympy finale per tutti i casi.
7. N03: riscrivere la formula in stability L35 con Π definito (o ‖η‖² senza Π),
   allineare col Thm 9-3; verifica della continuità.
8. WARN 5: riscrivere il proof del Corollary Two-Parameter Family in variational con
   conteggio onesto (includere p,q,r; verifica sympy su n=3 che le soluzioni sono
   isolate per molteplicità fisse).

### Fase 3 — Pulizia notazione (rischio medio, massivo ma meccanico)
9. C1/C2: hilbert_geometry L89/L137/L330: sostituire Q con Π (o q) e verificare la
   coerenza; diffeomorphism_local L69: δ→η e riscrivere l'euristica 𝒟≈Σδ²/P.
10. C4: pullback_metric L2-7: definire 𝒫 e F componentwise o chiarire la notazione.
11. C6/C7: stability L91-96 (O(‖P-P*‖³)) e L144-145 (caso degenere) — frasi chiarificatrici.
12. D2/D3/D4: INFO minori (linearization L11, posterior L186, pullback L140).

### Fase 4 — Completamento revisione (se richiesto)
13. Ripetere i blocchi A (capp. 1-5) e C (capp. 13-19) con subagent a timeout più alto
    o lettura diretta: i transcript mostrano lettura integrale completata e verifiche
    parziali (ref, bib, 6/ε², Dirac assente, Laplace corretto) senza finding critici
    aggiuntivi oltre a quelli già riportati.
14. Verifica matematica finale degli esempi AES, fingerprinting, DP in applications.

### Fase 5 — Verifica finale e commit
15. Compilazione da zero (rm aux, pdflatex x3 + bibtex): 0 errori / 0 undefined /
    0 multiply.
16. Ricalcolo numerico di ogni esempio toccato (N01, N06, N02).
17. Commit singoli in inglese (es. fix(smooth_functionals): Tsallis case special in
    g-entropy (N01)), push con credential helper keepass.

### Ordine consigliato
Fase 0 (decisioni) → 1 (meccanici) → 2 (matematici) → 3 (notazione) → 4 (completamento)
→ 5 (verifica+commit).

### Cosa NON toccare
- Struttura capitoli e ordine include in main.tex; label esistenti.
- Teoremi-cardine verificati (Cycle Factorisation, Representation, Three-Level, Thm 9-3).
- Tabelle empiriche F2 (ricalcolate e verificate).
