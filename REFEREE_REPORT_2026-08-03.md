# REFEREE REPORT — Verifica matematica completa

**Opera**: *Weighted Incidence Structures: Geometry, Information, and Cryptography* (WIS Book), v1.0.0, 34 capitoli, ~7.000 righe LaTeX.
**Redatto da**: Piz, assistente AI di Mecenates
**Data**: 03/08/2026
**Stato**: REVIEW COMPLETATA — nessun file .tex modificato
**Destinatari**: Fabrizio Biondi (autore)

---

## 1. Sintesi esecutiva

La revisione ha coperto **tutti i 34 file** della cartella `paper/chapters/`: lettura integrale (personale o tramite subagent con report estratti e verificati), check strutturali automatici su label/ref/ambienti, e verifica numerica (sympy/numpy) dei punti critici.

**Esiti**:
- **17 BUG** (errori matematici certi o strutture rotte)
- **~45 WARN** (errori probabili, ipotesi mancanti, incoerenze, ref sbagliati)
- **~18 INFO** (osservazioni minori)

**Cosa è risultato CORRETTO** (verificato passo-passo):
- Cycle Factorisation Theorem (wis.tex:103-152) — ogni passaggio algebrico.
- Representation Theorem (representation.tex:14-23) e corollari.
- Three-Level Theorem come struttura (ECT): regge nonostante B13 e B03.
- Tutti i valori numerici degli esempi di hilbert_geometry (autovalori 0.3820/1.3820/2.6180/3.6180, σ_min⁺=0.6180, C=1.6180, δ=0.3515/0.1839/0.0338).
- Identità algebriche principali: ΦᵀΦ a blocchi, Schur complement, ker(ΦᵀΦ)=ker Φ.
- Check automatici: 0 undefined ref, 0 multiply defined, ambienti bilanciati, nessun titolo duplicato.

**Nessun errore invalida la struttura del libro.** Gli errori sono localizzati e correggibili; due richiedono una decisione di design (B05 fattore n della UOD; B17 definizione di g-entropy).

---

## 2. BUG certi (da correggere)

### B01 — Gauge transformation errata e autocontraddittoria
- **File:riga**: representation.tex:82, 117, 125; dictionary.tex:18; historical_notes.tex:38
- **Severity**: BUG
- **Descrizione**: il testo afferma che la gauge che preserva le molteplicità è (w,β) → (λw, λ⁻¹β). Calcolo: n'_mc = λ⁻¹β/(λw) = λ⁻²·n_mc, NON invariante. La trasformazione corretta è (λw, λβ).
- **Agravante**: il Teorema di Unicità (representation.tex:92-97) e l'esempio a r.128 usano correttamente (λw, λβ) — il libro si contraddice da solo nella stessa sezione.
- **Fix**: sostituire tutte le occorrenze λ⁻¹β con λβ (5 punti).

### B02 — Teorema Geometric Entropy Estimate falso
- **File:riga**: entropy_bounds.tex:57-58 (Thm 11-3), :73 (Cor 11-4)
- **Severity**: BUG
- **Descrizione**: |H(P)−H(P⋆)| ≤ C·‖P−P⋆‖²_g richiede DH_{P⋆}=0 (punto stazionario), mai assunto. La sola regolarità C¹/C² dà un bound *lineare* in ‖P−P⋆‖; di conseguenza |ΔH| = Θ(√D), non O(D), in generale.
- **Nota**: per la Shannon entropy il punto stazionario esiste (massimo all'uniforme), quindi il bound quadratico vale *localmente attorno a U*, non attorno a un P⋆ generico.
- **Fix**: aggiungere l'ipotesi di punto stazionario, oppure riformulare come bound Lipschitz locale lineare.

### B03 — Esempio simmetrico del Three-Level incoerente
- **File:riga**: variational.tex:310-343
- **Severity**: BUG
- **Descrizione**: (a) "Adding the two equations gives α = βδ tanh δ" ha il segno sbagliato: il calcolo corretto dà α = −βδ tanh δ. (b) Più grave: con p=r la media ā = (p(−δ)+q·0+p·δ)/n = 0 è forzata; la stazionarietà in b=0 dà allora α=0, che contraddice la soluzione con β≠0, δ>0. L'esempio come scritto non ammette soluzioni.
- **Fix**: ricalcolare l'esempio (probabile: la configurazione simmetrica ha solo 2 livelli, o α=0 e il punto critico è il caso banale). Da validare numericamente dopo la correzione.

### B04 — Hessian della KL errata
- **File:riga**: bregman.tex:226-232
- **Severity**: BUG
- **Descrizione**: afferma Hessian diag(e^{x_i−n}) di e^{x_i−n}(x_i−y_i); la derivata seconda corretta è e^{x_i−n}(x_i−y_i+2).
- **Agravante**: con la formula corretta l'Hessian NON è globalmente PSD (se x_i ≪ y_i, x_i−y_i+2 < 0) → il Lemma "Geodesic Convexity of the KL Divergence" (bregman.tex:219-232) va rivisto: la convessità in coordinate logaritmiche non segue dalla convessità in coordinate P.
- **Fix**: correggere la formula; verificare (numericamente o con dimostrazione) se il lemma regge su tutto F(P) o solo su un intorno; in caso negativo, restringere l'enunciato.

### B05 — UOD con fattore n incoerente tra capitoli
- **File:riga**: algebra_uod.tex:46-58 vs variational.tex:47-54 (e smooth_functionals.tex:290-299, applications.tex)
- **Severity**: BUG
- **Descrizione**: algebra_uod definisce D = Σ(a_i−ā)² = n·Var_U_n(a); variational e smooth_functionals usano D = Var_U(a) = (1/n)Σ(a_i−ā)². Stesso simbolo, due oggetti che differiscono di un fattore n. Si propaga in tutti i bound e negli esempi numerici.
- **Fix**: DECISIONE DI DESIGN di Fabrizio (vedi Roadmap Fase 0): (a) unificare su D = Σ(a_i−ā)² (coerente con la definizione geometrica ‖q(Y)‖²), oppure (b) unificare su D = Var, oppure (c) introdurre due simboli distinti (es. D e d).

### B06 — Total Variation incoerente
- **File:riga**: comparative_geometry.tex:257 vs :270
- **Severity**: BUG
- **Descrizione**: r.257 definisce TV = ½Σ|P−Q|; r.270 afferma il limite TV(P_ε,Q) → ⅔ per P_ε → (0,½,½) vs (⅓,⅓,⅓). Con la definizione data il limite è ⅓ (il valore ⅔ è la somma non normalizzata Σ|·|).
- **Fix**: allineare: o cambiare la definizione in TV = Σ|P−Q| (allora ⅔ è corretto, ma va verificato che nessun altro uso assuma il ½), o cambiare il limite in ⅓.

### B07 — Posteriore Dirac per l'AES (errore concettuale)
- **File:riga**: basics.tex:109 (e motivating_examples.tex:17-19 incoerente con esso)
- **Severity**: BUG
- **Descrizione**: con incidenza completa I=M×C e n_mc=1, Bayes dà Pr[M=m|C=c] = π(m) (posteriore = prior), NON δ_mc. La Dirac mass richiederebbe cloak={c}, incompatibile con l'incidenza completa. L'ottimalità universale (posteriore uniforme sul cloak=M) vale solo con π uniforme.
- **Fix**: riscrivere: "posteriore = prior; universal optimality se π è uniforme". Correggere anche la frase in motivating_examples.tex:17-19.

### B08 — Teorema Spectral Bounds troncato
- **File:riga**: bregman.tex:134-148
- **Severity**: BUG (strutturale)
- **Descrizione**: l'enunciato del Teorema 15-3 non dichiara mai la conclusione e contiene la dimostrazione incastonata nel corpo del teorema (prima della fine dell'enunciato).
- **Fix**: completare l'enunciato con il bound cercato (λ_min·‖Δ‖²/2 ≤ D_φ ≤ λ_max·‖Δ‖²/2 con λ_min/λ_max definiti dall'integrale pesato), e spostare il blocco proof dopo \end{theorem}.

### B09 — Dimostrazione del Thm 17-1 (Piecewise Smoothness) spazzatura
- **File:riga**: piecewise_smooth.tex:97-101
- **Severity**: BUG (strutturale)
- **Descrizione**: la dimostrazione contiene testo copiato dal Crossing Time ("P_i(t)∝P_i^{1−t}Q_i^t", "log(P_i/P_j)≠...") invece di una dimostrazione.
- **Fix**: riscrivere: su un intervallo di regolarità l'ordine è fisso → max/min/rank si riducono a selezioni fisse di indici → per l'ipotesi (2) l'espressione è C^k in P(t) e quindi C^k in t.

### B10 — Dimostrazione di Continuity ripetuta + frase tronca
- **File:riga**: functional_analytic_uod.tex:11, 40-43
- **Severity**: BUG (strutturale)
- **Descrizione**: (a) r.11 "The results below are consequences of" — frase tronca senza oggetto; (b) r.40-43 la dimostrazione di Continuity replica quella di Smoothness senza provare la continuità.
- **Fix**: completare la frase (rimuovere o collegare); scrivere la dimostrazione vera della continuità (es. via stima ‖S(P)−S(Q)‖ ≤ ...).

### B11 — Simboli non definiti in due dimostrazioni
- **File:riga**: hilbert_geometry.tex:223 (S, Y_S); posterior_manifold.tex:55 (P, C, "open subset")
- **Severity**: BUG
- **Descrizione**: hilbert:223 la dimostrazione del quotient-Hilbert theorem usa "For any z∈S … Y−z=(Y_S−z)+Y^⊥" senza mai definire S né Y_S (probabilmente S=Im(C) e la proiezione di Y su S). posterior_manifold:55 "P = ∏_c Δ_c° is an open subset of this hyperplane" è falso per |C|>1 (il prodotto vive in un sottospazio affine proprio), e P, C non sono definiti in quel capitolo; c'è anche un "." spurio in math mode.
- **Fix**: definire S e Y_S (o riscrivere la dimostrazione); correggere l'affermazione topologica e definire gli oggetti.

### B12 — Dimostrazione circolare
- **File:riga**: stability.tex:81 (Thm 9-3)
- **Severity**: BUG
- **Descrizione**: la dimostrazione inizia "From Theorem ch:thm:9-3" — si cita da sé. L'espansione δ(P)=J_{P⋆}(P−P⋆)+O(‖P−P⋆‖²) è Taylor su F, non una conseguenza del teorema.
- **Fix**: riscrivere la dimostrazione usando Taylor sul map F (e la stabilità di J), senza auto-riferimento.

### B13 — Wronskian errato
- **File:riga**: variational.tex:177
- **Severity**: BUG
- **Descrizione**: il libro afferma W_4(x) = e^{3x}; il calcolo esatto (sympy) dà e^{2x}. La proprietà di non-annullamento (e quindi l'ECT) regge: solo il valore intermedio è sbagliato.
- **Fix**: sostituire e^{3x} con e^{2x}.

### B14 — Refuso LaTeX "hangle"
- **File:riga**: hilbert_geometry.tex:59-60
- **Severity**: BUG (LaTeX)
- **Descrizione**: manca la backslash in \rangle ("\Phi hangle", "hangle"); il PDF renderizza "Φhangle" come testo e l'inner product non si chiude mai.
- **Fix**: "\Phi h\rangle", "h\rangle".

### B15 — Frazione invertita nel testo introduttivo
- **File:riga**: wis.tex:8
- **Severity**: BUG
- **Descrizione**: "the normalised ratio n_mc = w(m)/β(c)" è il reciproco della definizione formale n_mc = β(c)/w(m) a r.24 della stessa sezione.
- **Fix**: invertire la frazione in β(c)/w(m).

### B16 — Hessiano della Rényi divergence confuso con la metrica di Fisher
- **File:riga**: smooth_functionals.tex:774-798
- **Severity**: BUG
- **Descrizione**: il teorema afferma che a P=Q l'Hessiano di D_α(·‖Q) rispetto alla metrica pullback è (α/2)g_Q, quindi D_α ≈ (α/2)·UOD con costante C=α/2 indipendente da n. Calcolo esatto in coordinate log: Hess = [α²/(α−1)]·(diag(Q) − QQᵀ), che NON è proporzionale alla metrica euclidea proiettata del WIS (δ_ij − 1/n). Già per α=1 (KL) il secondo ordine è ΣQ_i·a_i² (pesato), non Σ(a_i−ā)². La formula vale per la metrica di Fisher, non per la pullback euclidea.
- **Fix**: ricalcolare; se il risultato desiderato è D_α ≈ (α/2)·χ²_Q(P,Q) (chi-quadro pesato), dichiararlo esplicitamente e distinguere dalla UOD; altrimenti allineare la costante al calcolo corretto.

### B17 — g-entropy: definizione e tabella incoerenti
- **File:riga**: smooth_functionals.tex:390 vs 397-400 e 932-943
- **Severity**: BUG
- **Descrizione**: la definizione H_g(P) = g(Σ g⁻¹(−log P_i)) non produce nessuna entropia della tabella con le g date: con g(x)=x si ottiene −Σ log P_i (non Shannon); con g(x)=exp((1−α)x/α) non si ottiene Rényi. La definizione standard di Briët–Harremoës usa g⁻¹(P_i), non g⁻¹(−log P_i). Inoltre il denominatore (ΣP_i^α)² nel gradiente (r.416, 899) è un residuo della Rényi, privo di senso per g generica.
- **Fix**: DECISIONE DI DESIGN (vedi Roadmap Fase 0): adottare la definizione standard g⁻¹(P_i) (e ricalcolare tabella + gradiente), oppure mantenere la variante logaritmica con le g corrette per Shannon/Rényi/Tsallis.

---

## 3. WARN

### Blocco A (fondamenti) — da subagent, verificato
- **motivating_examples.tex:16** — "Every pair (M,K) maps to a distinct ciphertext" falsa per conteggio (2^256 coppie, 2^128 ciphertext); la proprietà richiesta da n_mc=1 è l'iniettività di K↦E(M,K) per M fissato.
- **motivating_examples.tex:21-24** — "n_mc=1 for every triple (M,C)": la molteplicità è indicizzata da coppie (m,c), non triple; e D≡0 vale solo con π uniforme.
- **motivating_examples.tex:55-59** — "posterior uniform on a closed disk" falso per Laplace (posteriore ∝ π(m)e^{−ε‖c−m‖}); UOD=2/ε² asserito senza derivazione.
- **basics.tex:90** — "The two notions coincide only when the prior is uniform on every cloak": condizione necessaria ma non sufficiente (manca la completezza).
- **wis.tex:101** — "the product of multiplicities around every cycle must equal 1": parafrasi sbagliata (la condizione è l'uguaglianza dei due prodotti alternati = rapporto 1).
- **wis.tex:287-289** — la classificazione omette la terza condizione w∝π (presente invece in representation.tex:32-37).
- **wis.tex:309** — proof del Lemma row-sum con frasi pendenti non corrispondenti all'enunciato ("Dividing by |K| gives the transition probability. The last assertion..." — il lemma ha una sola asserzione).
- **wis.tex:320** — "Substitute the second identity of Lemma row-sum": il lemma ha una sola identità; usare la legge di probabilità totale.
- **wis.tex:349** — "the incidence structure is the complete bipartite graph … Every ciphertext is its own cloak": con incidenza completa il cloak è tutto M, non {c}.
- **representation.tex:92-97** — Teorema Unicità: manca l'ipotesi "nessun vertice isolato"; λ_H non è definito su componenti isolate.
- **linearization.tex:61** — quote "Mathematical intuition": ω=Φ(u,v) con componenti u_m−v_c, mentre nel resto del capitolo ω := log n = v_c−u_m; stesso simbolo con segno opposto.
- **linearization.tex:126** — esempio geo-indistinguishability: errore di tipo su Φ (agisce su potenziali, non su edge) e incoerenza con motivating_examples.
- **wis.tex:293,296 / representation.tex:1 / linearization.tex:1 / introduction.tex:1 / discussion.tex:1 / open_problems.tex:1** — caratteri BOM U+FEFF spuri (in wis.tex anche a metà file).

### Blocco B (geometria) — da subagent, verificato
- **hilbert_geometry.tex:31-35 / 41-45** — blocco "Let V_M=…, V_C=…, V_I=…, A,C" definito due volte verbatim (con paragrafo editoriale incastrato tra le copie).
- **hilbert_geometry.tex:179** — "selecting the orthogonal representative QY as the canonical gauge" confonde due quozienti diversi (mod ker Φ vs V_I/Im(C)).
- **hilbert_geometry.tex:239** — "D(P)=‖δ(P)‖²" ill-typed: δ(Y)=‖q(Y)‖ è già uno scalare; la mappa P↦Y non è data.
- **hilbert_geometry.tex:300** — "|K|=12" incoerente con la matrice N mostrata (somma 36, righe da 12); serve "12 keys per message".
- **posterior_manifold.tex:65-67** — proof del Thm 1-5 che invoca T_P P = ∏_c T_{P_c}Δ_c° con P mai definito (non sequitur).
- **posterior_manifold.tex:98** — Q sovraccarico: mappa quoziente vs proiettore ortogonale Q=I−CD_C⁻¹Cᵀ in hilbert_geometry.
- **posterior_manifold.tex:134** — L sovraccarico: mappa logaritmica vs Laplaciano posteriore L=AᵀQA.
- **posterior_manifold.tex:184** — "dim(Im(DL_P))=k−1 by Theorem ch:thm:1-5" cita il teorema sbagliato (dovrebbe essere ch:thm:3-2/ch:cor:3-3); ripetuto in projection.tex:260.
- **projection.tex:27** — self-reference "Recall the quotient space (Section ch:sec:canonical-projection-and-differential-factorisation)" (label del proprio capitolo).
- **projection.tex:260** — running example AES: copia verbatim del paragrafo DP/Laplace di posterior_manifold (contenuto DP, non AES) + ref sbagliato.
- **diffeomorphism_local.tex:6** — "F=Q∘L introduced in Chapter ch:sec:the-posterior-manifold" ref sbagliato (F è definita in projection.tex).
- **diffeomorphism_local.tex:69** — "DF_P(Q−P)=Q(log P−log Q)" sbagliato: DF_P(Q−P)=Q((Q_i−P_i)/P_i)_i; l'euristica "D≈‖δ‖²/min_i P_i" non derivata.
- **diffeomorphism_local.tex:71** — "The next chapter extends this to a global diffeomorphism" — pullback_metric non lo dimostra.
- **pullback_metric.tex:2,62** — "F: P → F(P) global diffeomorphism established in Chapter ch:sec:local-diffeomorphism": quel capitolo prova solo locale, e per Δ_k°, non per ∏_c Δ_c°; Q_c mai definita.
- **pullback_metric.tex:27** — "distance on the manifold = Euclidean distance between images" troppo forte: richiede F(P) geodesicamente convesso, non stabilito.
- **pullback_metric.tex:140** — formula running-example g_P(u,v) ill-typed (F* su tangent vectors, denominatore che dipende da Q, F(P)∘F(Q) indefinito).
- **stability.tex:35,95** — "D(P)=g_{P⋆}(δ(P),δ(P))" ill-typed (δ non è un tangent vector in P⋆); δ vettore vs scalare di hilbert_geometry (clash).
- **stability.tex:118-121** — "By Theorem ch:thm:9-3, D(P)≥0": la nonnegatività segue dalla definizione (norma al quadrato), non dal teorema.
- **stability.tex:145-148 / 151-154** — paragrafi "Running example: AES" e "Having established … Fisher" duplicati verbatim.
- **entropy_bounds.tex:19** — ref sbagliato per la metrica pullback (punta a stability, non a pullback_metric); manca il punto finale.
- **entropy_bounds.tex:81** — bound min-entropy con L=1/min_i π_i e l'espansione H_∞ ≤ log n − ½D asseriti senza prova; mescolano prior π in affermazioni su posterior P,Q.

### Blocco C (funzionali) e D (variazionale/applicazioni) — verifica personale
- **universal_bounds.tex:115** — "Transition to Chapter~\ref{ch:sec:universal-geometric-bounds}" è un auto-riferimento (label del capitolo stesso).
- **universal_bounds.tex:33** — "‖S(P)−S(Q)‖ ≤ L d_g(P,Q)" usa norma su uno scalare (dovrebbe essere |·|); coerente con l'abuso ripetuto in smooth_functionals:24, 108, 111, 372.
- **bregman.tex:3,52,235** — "Chapter~15" per i universal bounds: il capitolo giusto è 16 (sfalsamento sistematico, vedi W-HC).
- **bregman.tex:421-422** — riga finale duplicata ("related quantities become instances of the same geometric theory").
- **functionals.tex:30-37** — paragrafo "An information functional is any mapping…" duplicato.
- **universal_security_bounds.tex:45-47, 70-94, 125-137** — sezioni intere ripetute (Smooth Security Bounds, Unified Stability Principle, Scope and Limitations).
- **piecewise_smooth.tex:63-80** — blocco "Regularity Regions" duplicato.
- **smooth_functionals.tex:88-100** — gradiente Rényi con fattore "·max_i P_i" sospetto (coerenza con la metrica da verificare).
- **smooth_functionals.tex:303-343** — esempio binario min-entropy: costanti L²=90, L=9.49 e la soglia D≤0.011 da verificare con calcolo completo (in particolare la derivazione di L_∞²).
- **smooth_functionals.tex:404-419** — gradiente g-entropy con denominatore (ΣP_i^α)² che non ha senso per g generica (residuo Rényi; legato a B17).
- **smooth_functionals.tex:556-565** — definizione di chi-quadro duplicata.
- **smooth_functionals.tex:956-966** — tabella costanti: per α<2, "max_i P_i^{α−2}" si realizza sul minimo P; scrittura ambigua (vs r.235 che lo riconosce).
- **smooth_functionals.tex:1007** — "Lipschitz ratio ranges from 60× to over 400,000×": la tabella mostrata arriva a 20,700×; il 400,000× non è supportato.
- **smooth_functionals.tex:998** — \label{tab:empirical-lipschitz} dentro \begin{array} (non un ambiente table): il cross-ref "Table" non funziona.
- **variational.tex:3** — "explored in Chapter~29 (Open Problems)": open_problems è il capitolo 30.
- **variational.tex:139** — dimostrazione del Lemma 29-2: "Since e^{-x}(1−x+ā) is bounded" — falso su tutto R (diverge per x→−∞); l'argomento "ψ' ha finitamente molti zeri ⟹ ψ ha ≤3 zeri" è incompleto (la dimostrazione corretta è nel Lemma 29-5 via ECT).
- **variational.tex:203 vs 208** — Teorema 29-3: l'enunciato dice "five equations in five unknowns", la dimostrazione conta 8 incognite e 6 equazioni; incoerenza interna.
- **variational.tex:227** — "a system of five equations in the unknowns a,b,c,α,β plus the integer multiplicities" — conteggio diverso da quello del teorema.
- **algebra_uod.tex:26-27,63,65** — "$x-\bar x,\mathbf1$" con virgola (dovrebbe essere prodotto scalare senza virgola).
- **algebra_uod.tex:99** — item spezzato: "\end{itemize} constant in logarithmic coordinates" (end{itemize} nel mezzo della frase).
- **comparative_geometry.tex:4** — "discussion of related work in Chapter~27": discussion è il capitolo 28.
- **comparative_geometry.tex:257** — TV usa \|P_i−Q_i\| (norma) invece di |P_i−Q_i| su scalari.
- **analytic_theory.tex:4** — "The analytic theory of this chapter (Chapter~20) is developed concretely in Chapters~21--23, and its variational consequences appear in Chapters~24--25": analytic_theory È il capitolo 21 → tutti i numeri sfalsati di 1.
- **discussion.tex:48** — frase tronca: "…a canonical Hilbert-space geometry whose analytic constructions." (manca il predicato).
- **discussion.tex:188** — frase malformata: "…the canonical Hilbert-space geometry its associated Hilbert-space formalism."
- **applications.tex:46,98,457** — fattorizzazione scritta "log n_mc = u_m + v_c" invece di v_c − u_m (segno; le altre occorrenze del libro usano la differenza).
- **applications.tex:165-167** — geo-indistinguishability: D = (ε²/2π)∫‖k‖²e^{−ε‖k‖}dk = 2/ε²: l'integrale esatto vale 6/ε² (confusione tra varianza 1D e 2D). Si propaga in dictionary.tex:27, hilbert_geometry.tex:387 e nell'esempio numerico r.179-182.
- **applications.tex:296-306** — mix network: formula H ≥ log n − (n/2)D ma esempio con −0.025 (cioè D/2, non nD/2); numeri incoerenti tra loro (log₂100 − 0.025 ≠ 6.57).
- **applications.tex:301,357,408** — parentesi graffe rotte in math mode ("r=3\)", "δ_mc=0.1\)", "3.5/(2·0.004)").
- **applications.tex:402-414** — "log₂ T ≥ 8 − 437 = vacuous": il calcolo è onesto ma l'interpretazione "distinguishing them requires T≥10 traces" non deriva dal bound.
- **open_problems.tex:36** — "|Cloak(c,·)| = |K|·Pr[M=m|C=c]" formula sospetta (dimensionalmente non torna: dovrebbe essere 1/Pr o simile).
- **open_problems.tex:258** — "pitchfork bifurcations described in Section~25.9.1": numero di sezione hardcoded che non corrisponde alla struttura reale.
- **comparison.tex:23-24** — "every posterior is a Dirac mass" per l'AES: contraddice applications.tex:54-57 (posteriore uniforme 1/256) e B07.
- **comparison.tex:12-18** — "Shannon perfect secrecy = posterior uniform on the cloak": confonde perfetta segretezza con universal optimality (il libro stesso li distingue in discussion.tex:72-81).
- **dictionary.tex:27** — "Laplace mechanism & D=2/ε²": valore errato (vedi applications.tex:165-167).
- **conclusions.tex:59,127** — "this appendix": il capitolo è numerato (27), non un'appendice.
- **historical_notes.tex:70** — "Pinsker KL ≥ ½‖P−Q‖_TV²": con TV=½Σ|·| del libro la costante corretta è 2, non ½.
- **historical_notes.tex:106** — "The final chapter of the book (open problems)": open_problems è il 30°, l'ultimo è notation (34).
- **notation.tex:37-38** — δ "non-squared" e D=‖δ‖²: incoerente con δ(Y)=‖q(Y)‖ scalare di hilbert_geometry (clash di notazione, vedi stability.tex:35).

### W-HC — Riferimenti hardcoded "Chapter~N" sistematicamente sfalsati
- **File:riga**: ~50 occorrenze in ~20 file. Esempi: bregman.tex:3,52,235; projection.tex:24; variational.tex:3; analytic_theory.tex:4; posterior_manifold.tex:13; diffeomorphism_local.tex:19; smooth_functionals.tex:3; piecewise_smooth.tex:3; universal_bounds.tex:3; universal_security_bounds.tex:3; entropy_bounds.tex:4; roadmap.tex:31-65 (intero diagramma).
- **Severity**: WARN (sistematico)
- **Descrizione**: quasi tutti i "Chapter~N" testuali sono sfalsati di 1-2 rispetto alla numerazione reale (1=Motivating, 2=Introduction, 3=Roadmap, 4=Basics, 5=WIS, 6=Representation, 7=Linearization, 8=Hilbert Geometry, …).
- **Fix**: (consigliato) sostituire con \ref{} ai label di capitolo esistenti; in alternativa correggere i numeri uno a uno.

---

## 4. INFO (selezione)

- motivating_examples.tex:51 — notazione "Lap(0,ε⁻¹)²" non spiegata (probabile Laplace planare).
- motivating_examples.tex:70-73 — ottimalità del Laplace asserita senza rinvio a dimostrazione.
- wis.tex:293,296 — BOM spuri (già citati in WARN).
- introduction.tex:16-18 — "UOD misura la distanza dalla perfetta segretezza": il riferimento formale è l'ottimalità universale, più debole; formulazione imprecisa.
- hilbert_geometry.tex:84,97 — Q=I−CD_C⁻¹Cᵀ richiede D_C invertibile (cloak non vuoti): ipotesi dichiarata solo in linearization.
- hilbert_geometry.tex:123 — convergenza del gradient-based optimization asserita senza prova (euristica).
- hilbert_geometry.tex:304-311 — segno Φ(u,v)=−ω non dichiarato nell'esempio.
- posterior_manifold.tex:80,86 — k in R^k mai definito.
- projection.tex:257 — "UOD as squared norm": la definizione formale dà δ=‖q(Y)‖ (una norma), il "quadrato" è solo nell'intuition informale.
- pullback_metric.tex:62 — "\\\\(F\\\\)" con quattro backslash: tipografa come interruzioni di riga, non inline math.
- stability.tex:62-63 — P⋆ (reference posterior) mai definito.
- entropy_bounds.tex:77 — la citazione di Thm 9-3 è troppo forte (il teorema dà leading term + O(‖·‖³)).
- smooth_functionals.tex:1061 — label ch:thm:29-3 con numero di file "29" che non corrisponde al numero di capitolo reale (26).
- variational.tex:379 — ref a ch:thm:14-1/14-2 (label del file 14) ok, ma coerenza numerica label/capitolo da uniformare (vedi anche smooth_functionals:1061).

---

## 5. Roadmap di correzione

### Fase 0 — Decisioni di design (richiedono Fabrizio)
1. **B05 — Fattore n della UOD**: scegliere (a) D=Σ(a_i−ā)² ovunque, (b) D=Var ovunque, (c) due simboli distinti. Raccomandazione: (a) o (c), coerenti con la definizione geometrica ‖q(Y)‖².
2. **B17 — Definizione di g-entropy**: adottare la definizione standard g⁻¹(P_i) di Briët–Harremoës (e ricalcolare tabella + gradiente) oppure mantenere la variante logaritmica con g corrette.
3. **W-HC — Riferimenti "Chapter~N"**: confermare la strategia \ref{} ai label di capitolo (consigliata, allineata alla regola "MAI hardcoded").

### Fase 1 — Refusi, LaTeX e strutture rotte (rischio basso, nessuna matematica)
- B14 (hangle), B13 (Wronskian), B15 (frazione), B10a (frase tronca), B08 (Spectral Bounds: spostare proof fuori dal theorem), B09 (proof Thm 17-1), B10b (proof Continuity).
- Rimozione duplicati: hilbert_geometry:31-45; functionals:30-37; universal_security_bounds:45-47/70-94/125-137; piecewise_smooth:63-80; smooth_functionals:556-565; bregman:421-422; stability:145-154.
- Rimozione BOM U+FEFF in 6 file (wis, representation, linearization, introduction, discussion, open_problems).
- Parentesi rotte in applications.tex:301,357,408.
- algebra_uod:26-27,63,65 (virgola nel prodotto scalare), :99 (item spezzato); comparative_geometry:257 (norma su scalari); pullback_metric:62 (quattro backslash).
- conclusions:59,127 ("appendix" → "chapter").

### Fase 2 — BUG matematici puntuali con fix noto (rischio medio)
- **B01 gauge**: 5 occorrenze (representation:82,117,125; dictionary:18; historical_notes:38) → (λw, λβ).
- **B06 TV**: allineare definizione e limite (⅓ se TV=½Σ; altrimenti definire TV=Σ|·| e verificare gli usi).
- **B04 Hessian KL**: formula corretta e verifica del Lemma di convessità (eventuale restrizione dell'enunciato).
- **B07 posteriore AES**: riscrivere la frase (posteriore=prior, ottimalità con π uniforme) + motivating_examples:17-19.
- **B11 simboli non definiti**: definire S/Y_S in hilbert:223; P/C in posterior:55 e correggere "open subset".
- **B12 proof circolare**: riscrivere stability:81 via Taylor su F.
- **B02 entropy bound**: aggiungere ipotesi di punto stazionario o trasformare in bound lineare; correggere Cor 11-4 di conseguenza.

### Fase 3 — Ricalcoli che richiedono verifica numerica (rischio alto, da validare)
- **B03 esempio simmetrico**: ricalcolare e verificare con sympy dopo la modifica.
- **B16 Hessiano Rényi divergence**: ricalcolare; decidere se il risultato è χ² pesato o altro; aggiornare C=α/2 e il paragrafo.
- **B17 g-entropy**: dopo la decisione Fase 0, ricalcolare gradiente e costanti (r.404-419, 932-943).
- **B05 fattore n UOD**: dopo la decisione Fase 0, allineare algebra_uod/variational/smooth_functionals/applications.
- **smooth_functionals:88-100, 303-343**: ricalcolare gradiente Rényi e costanti min-entropy (L²=90, L=9.49, soglia 0.011).
- **applications.tex:165-167 e 296-306**: correggere 6/ε² (2/ε²) e i numeri del mix network; verificare gli esempi numerici dipendenti.
- **dictionary.tex:27 e hilbert_geometry.tex:387**: allineare il valore Laplace (2/ε² → 6/ε² o alla convenzione scelta).
- **WARN vari (dimostrazioni non sequitur)**: posterior_manifold:65-67 e 184; diffeomorphism:69; pullback:27,140; projection:260; entropy:81 — riscrivere le dimostrazioni.

### Fase 4 — Riferimenti e notazione (rischio medio, massivo ma meccanico)
- **W-HC**: sostituire "Chapter~N" con \ref{} ai label di capitolo (verificare che ogni label esista; i label di capitolo sono già presenti in tutti i file).
- **Ref \ref sbagliati**: entropy_bounds:19; diffeomorphism:6; posterior_manifold:184; projection:27/260; universal_bounds:115 (auto-ref); pullback:2.
- **Clash di notazione**: documentare o rinominare Q (proiezione vs quoziente) e L (log map vs Laplaciano); chiarire δ (vettore) vs δ(Y)=‖q(Y)‖ (scalare) e D(P)=‖δ(P)‖² (hilbert:239, stability:35, notation:37-38).

### Fase 5 — Verifica finale
Per ogni modifica:
1. Modifica con metodo sicuro (skill latex-file-surgery / scrittura mirata — MAI write_file generico su .tex senza la procedura).
2. Compilazione: `pdflatex main && bibtex main && pdflatex main && pdflatex main` (una passata non basta).
3. Controllo `main.log`: 0 undefined refs, 0 multiply defined.
4. Verifica PDF: timestamp aggiornato, nessun "hangle"/artefatto visibile.
5. Per le correzioni matematiche: riconferma numerica (sympy/numpy) dell'esempio corretto.
6. Commit su git con messaggio descrittivo (per la repo wis-theory, con credential helper keepass — niente token in URL).

### Ordine consigliato di esecuzione
1. Fase 0 (decisioni) → 2. Fase 1 (refusi, ~mezza giornata) → 3. Fase 2 (BUG puntuali) → 4. Fase 3 (ricalcoli + validazione numerica) → 5. Fase 4 (ref e notazione) → 6. Fase 5 (verifica completa e commit).

### Cosa NON toccare
- Struttura dei capitoli e ordine di inclusione in main.tex.
- Label esistenti (verificare che ogni \ref continui a risolvere dopo ogni modifica).
- I teoremi-cardine (Cycle Factorisation, Representation) — già verificati corretti.
- L'architettura dei Part (label ch:part:*).

---

*Redatto da Piz, assistente AI di Mecenates — 03/08/2026. Nessun file .tex modificato durante la review.*
