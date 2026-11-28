# Delta adversarial review of the casBound paper, version 2

Reviewer: verifier subagent (Claude Fable 5.2), launched by the mathematics agent. 2026-11-27.
Brief: `BRIEF-delta-adversarial-v2.md` in this folder. Read-only: this report is the only file written in the repository.

Reviewed: `local-source/_Scratch/mathematics-codex/vance-casbound-v2/v2/paper/paper.tex` (1,817 lines; byte-identical to `docs/publications/casbound-release-v2/paper/paper.tex`) and its `paper.pdf` (24 pages), against version 1 (`.../vance-casbound-review/in/paper.tex`) and the Lean tree `.../mathematics-lean-exposition/targets/alpoge/lean/src`.

## Verdict

**SURVIVED. PROOF CORRECT.** I found no mathematical error in version 2.

- The displayed statements of Theorem A and Propositions 1 to 9 are character-identical to version 1 after white-space normalisation, and each matches its Lean declaration symbol by symbol.
- Every new mathematical statement checks out: Theorem B (a), (b), (c), the Observation, the running example, Figure 1, Propositions 10 and 11, the content route, the equality statement of Section 5.1, the remarks, and the numbers of Section 4. Theorem B(b) is proved below and confirmed in exact arithmetic with two negative controls.
- Findings that need a change: one small gap (the abstract's inequality is stated without labels, and no sentence derives it from Theorems A and B), three concordance slips, two lists of non-Lean material that disagree, one citation whose scope is narrower than its use, and three wording points. None affects a theorem.

Counts over the 18 findings: MATH-FATAL 0, MATH-GAP 1 (two sentences fix it), CITATION 1, EXPOSITION 5, OK 11.

How I worked. I checked the mathematics from the paper and the Lean sources alone, without opening the seven earlier reports. After that I searched those reports only for the provenance of numbers the paper quotes about its own process (finding 18). The revision log was read as a list of claims to test, not as evidence.

## Findings

Labels are those of the adversarial manuscript brief. Line numbers are lines of version 2's `paper.tex` unless a file is named.

### 1. OK. Theorem A and Propositions 1 to 9 are unchanged and match the Lean

Statement text. `python3 /tmp/casbound-v2-verifier/compare_statements.py` (source in Appendix B) prints:

```
thm:bound  -> thm:A   identical: True   (701 chars)
prop:1     -> prop:1  identical: True   (271 chars)
prop:2     -> prop:2  identical: True   (189 chars)
prop:3     -> prop:3  identical: True   (312 chars)
prop:4     -> prop:4  identical: True   (292 chars)
prop:5     -> prop:5  identical: True   (267 chars)
prop:6     -> prop:6  identical: True   (312 chars)
prop:7     -> prop:7  identical: True   (557 chars)
prop:8     -> prop:8  identical: True   (571 chars)
prop:9     -> prop:9  identical: True   (614 chars)
control (m_i+2i+1-n changed to m_i+2i-1-n in v2's Theorem A): False
```

The last line is the control: a one-character change is detected.

The definitions the statements rest on are also unchanged. Version 1 gave them in the paragraph before the theorem (v1 lines 231–237), the notation table (v1 lines 374–415) and the routine-facts list (v1 lines 990–992); version 2 gives them in Sections 2.1 and 2.2 (lines 227–250, 305–336). I compared L_n, V, the inner product (conjugate-linear in the first argument), P_pq including P_pp = Id, the matrix unit E^(p)_{ii'}, G_{ii'}, K, m_i, S_c, C_S, d, h_c, T(γ,b) and U(γ,S). They agree.

Against the Lean (read in full: the five proof files, `KTypeData.lean`, `StepFormula.lean`):

| Paper | Lean declaration and location | What I compared | Match |
|---|---|---|---|
| Theorem A | `CasBound`, StepFormula.lean:88–94, proved by `casBound_holds`, CasBoundHolds.lean:9–32 | `IsTab col b` (KTypeData.lean:51–52) is hypotheses 1 and 2; `∀ p q, col p = col q → (p ∈ S ↔ q ∈ S)` is hypothesis 3; `∀ p q, col p = col q → p ≠ q → pm (Equiv.swap p q) f = -f` is hypothesis 4; conclusion `(star f ⬝ᵥ (∑ a, ∑ c, tE S 0 a c * tE S 0 c a) f).re ≤ (∑ i, m_i * (m_i + 2*i + 1 - n)) * (star f ⬝ᵥ f).re` | yes |
| matrix unit, G, P_pq | `eAt`, `tE`, `pm`, KTypeData.lean:17–27 | `eAt p a b f I = if I p = a then f (Function.update I p b) else 0` is the displayed formula for E^(p)_{ii'} (line 323); `tE S 0 a b = ∑ p ∈ S, eAt p a b`; `pm σ f I = f (I ∘ σ)` | yes |
| Prop. 1 | `pair_apply`, Expand.lean:32–55 | `∑ a, ∑ c, eAt p a c (eAt q c a f) I = if p = q then n * f I else f (I ∘ swap p q)` | yes |
| Prop. 2 | `cas_expand'`, Expand.lean:66–92 | `K = (n * S.card) • 1 + ∑ p ∈ S, ∑ q ∈ S.erase p, pm (swap p q)` | yes |
| Prop. 3 | `re_swapSum_le'`, ReSwapSumLe.lean:29–83 | hypotheses `p ∉ B` and alternation on B only; conclusion on the real part of the sum | yes |
| Prop. 4 | `count_up`, CountSame.lean:22–44 | needs `IsTab`, whole columns and `p ∈ S`; count is `n - 1 - b p` | yes |
| Prop. 5 | `count_eqb`, CountSame.lean:46–69 | needs `IsTab` and `p ∈ S` only, as the paper says after the proof | yes |
| Prop. 6 | `sum_sum_ite_col_ne_eq_sum_by_col` (private), CountCross.lean:59–83 | sums over `S.image col` with `d ≠ c` | yes |
| Prop. 7 | `sum_filter_col_le_sum_ite_of_bound` (private), CountCross.lean:28–57 | all `c ≠ d` in C, real N of any sign, one-box hypothesis over every `c ≠ col p` | yes |
| Prop. 8 | `count_cross`, CountCross.lean:85–102 | same hypotheses, equal-label count on the right | yes |
| Prop. 9 | `cas_count`, CountCross.lean:104–153 | adds `R p q = -N` for distinct boxes of one column | yes |

The proofs in Section 3 follow the Lean proofs step for step (I compared each: for example the two cases of Proposition 7 are CountCross.lean:35–39 and 40–57, and the identity ‖g‖² = (s+1)·Re⟨f,g⟩ is `hgg`/`hre` at ReSwapSumLe.lean:65–68 and 74–76). The proofs of version 2 are version 1's with commentary removed; no step changed.

As an attack on the transcription I also searched at random for counterexamples to Propositions 4 to 9 exactly as displayed (abstract symmetric kernel R, real N including negative values, a column set C that may contain a column with no boxes). `python3 /tmp/casbound-v2-verifier/check_props_abstract.py` (Appendix E):

```
statements as displayed (symmetric R, whole columns): {'tested': 2947, 'p4': 0, 'p5': 0, 'p6': 0, 'p7': 0, 'p8': 0, 'p9': 0, 'tight9': 2764, 'negN': 450}
control, R not symmetric:                              {'tested': 2973, 'p4': 0, 'p5': 0, 'p6': 0, 'p7': 696, 'p8': 696, 'p9': 696, 'tight9': 2105, 'negN': 490}
control, arbitrary partial selection (U dropped):      {'tested': 2963, 'p4': 1166, 'p5': 0, 'p6': 0, 'p7': 407, 'p8': 407, 'p9': 725, 'tight9': 1985, 'negN': 462}
```

The entries p4 to p9 count violations. None occurred in 2,947 feasible instances (450 with N < 0), and Proposition 9 held with equality in 2,764 of them, so the search was pressing on the bound. Both controls fail as they should: without symmetry of R Propositions 7 to 9 break, and without whole-column selection Proposition 4 breaks while Propositions 5 and 6 still hold, as the paper says.

The Lean files were not recompiled for this delta review. The root file supplied for review is byte-identical to the one in the tree (`cmp` exit 0), and nothing in version 2 changes what the two version 1 verifiers compiled.

### 2. OK. Theorem B(a), the form by heights

Proof. By the Observation, m_i = #{c : h_c ≥ n−i}. Then Σ_i m_i² = Σ_{c,c'} #{i : n−i ≤ min(h_c,h_c')} = Σ_c h_c + 2 Σ_{{c,c'}} min(h_c,h_c'), and Σ_i m_i(2i+1−n) = Σ_c Σ_{i=n−h_c}^{n−1} (2i+1−n) = Σ_c h_c(n−h_c). Adding gives Σ_c h_c(n+1−h_c) + 2 Σ min. The paper's proof (lines 911–923) reaches the same result through the per-box count and is correct.

Check: all 6,435 multisets of at most six heights with n ≤ 8 agree; the control (pair sum without the factor 2) disagrees in 231 cases. See the first two lines of the output under finding 3.

### 3. OK. Theorem B(b), the sum-of-squares identity

Proof, from two facts that are in the Lean. Put N = ‖f‖² and R(p,q) = Re⟨f, P_pq f⟩.

1. Proposition 2 (`cas_expand'`): Re⟨f,Kf⟩ = ndN + Σ_{p∈S} Σ_{q∈S, q≠p} R(p,q).
2. Alternation gives R(p,q) = −N for distinct boxes of one column. There are Σ_c h_c(h_c−1) such ordered pairs.
3. The other ordered pairs split by ordered pairs of distinct active columns (Proposition 6). With X(c,c') = Σ_{p∈S_c} Σ_{q∈S_c'} R(p,q), symmetry of R gives X(c,c') = X(c',c), so they contribute 2 Σ_{{c,c'}} X(c,c').
4. One-box identity. For p ∉ B and f alternating on B, with Y = Σ_{q∈B} P_pq: N − Σ_{q∈B} R(p,q) = ‖f − Yf‖²/(|B|+1). The Lean proves exactly these two lines inside `re_swapSum_le'`: `hre` (‖g‖² = (1+|B|)·Re⟨f,g⟩ for g = f − Yf, lines 74–76) and `hfg` (⟨f,g⟩ = ⟨f,f⟩ − Σ_q ⟨f, P_pq f⟩, lines 80–81). Take B = S_c' and p ∈ S_c, and sum over p: h_c N − X(c,c') = (1/(h_c'+1)) Σ_{p∈S_c} ‖f − Y_p f‖².
5. Substitute step 4 into step 3 with c the shorter column of each pair: Re⟨f,Kf⟩ = [nd − Σ_c h_c(h_c−1) + 2 Σ min(h_c,h_c')]·N − 2 Σ_{{c,c'}} (1/(h_c'+1)) Σ_{p∈S_c} ‖f − Y_p f‖². Since nd − Σ h_c(h_c−1) = Σ h_c(n+1−h_c), part (a) turns the bracket into the label coefficient. That is (b).

In a tie both namings give the same h_c N, so either may be used. With the taller column as source the identity of step 4 still holds, but it produces h_c' N in place of min(h_c,h_c') N, so the formula of (b) is then false; this is the first control below.

Smallest case by hand: n = 2, two one-box columns, f = |01⟩. N = 1, K = 4·Id + 2P, ⟨f,Kf⟩ = 4, coefficient 6, left side 2. Right side: 2 · (1/2) · ‖|01⟩ − |10⟩‖² = 2.

Exact check. `python3 /tmp/casbound-v2-verifier/repro_thmB.py` is standalone (Appendix A). It uses integer tensors and rational arithmetic, so equality is exact. Output:

```
B(a): mismatches over all height multisets, n<=8, <=6 columns: 0
Figure 1 (n=4, heights 3,2,2,1): coefficient by labels, by heights = (40, 40)
Running example (n=2, heights 2,1): coefficient by labels, by heights = (6, 6)
B(b): 78 configurations in exact arithmetic, failures: 0
control, taller column as source: rejected 53 of 53
control, divisor h_c+1 instead of h_c'+1: rejected 30 of 30
one instance, n=3, heights (2,1): (coef_labels, coef_heights, ||f||^2, LHS, RHS) = (9, 9, 152, Fraction(36, 1), Fraction(36, 1))
```

Both controls are rejected in every applicable configuration. (The divisor control is applied only where an unequal pair has taller height below n and the deficit is not zero, since for a taller column of height n every f − Y_p f vanishes and the divisor cannot matter.)

A wider floating-point run with complex f, unselected columns of several heights and the matrix-unit definition of K (`python3 /tmp/casbound-v2-verifier/check_core.py`, Appendix C):

```
[B(a)] exhaustive n<=8, <=6 columns: 6435 height multisets, mismatches = 0
[B(a)] control (pair sum without factor 2): mismatches = 231 (must be > 0)
[Fig1] m = [0, 1, 3, 4]  per-label terms = [0, 0, 12, 28]  coef_labels = 40  heights terms = [6, 6, 6, 4]  pair-min sum = 9  coef_heights = 40
[Example] labels = [0, 1, 1]  m = [1, 2]  coef_labels = 6  coef_heights = 6
[Example] ||f||^2 = 0.9999999999999998  P12 f = -f: True
[Example] <f,P13 f> = 0.4999999999999999  <f,P23 f> = 0.4999999999999999  Yf = f: True
[Example] K from matrix units vs 6 Id + 2(P12+P13+P23): True  Re<f,Kf> = 5.999999999999999
[B(b)] configurations with nonzero column-alternating f: 293 (Prop 2 checked from the matrix-unit definition in 166)
[Prop2] max |K_def f - (nd f + sum swaps f)|: alternating f 4.28e-14, arbitrary f 2.11e-13
[ThmA] min over configs of (coef*N - Re<f,Kf>)/N = -2.485e-13 (must be >= -1e-9);  max |Im<f,Kf>|/N = 3.16e-14
[B(b)] max relative error of the identity = 2.48e-13;  with the other naming in ties = 2.48e-13
[B(b)] control, taller column as source, on 116 configs with unequal heights: min error = 2.000e+00 (must be clearly > 0)
[B(b)] control, divisor h_c+1 (source height), on 81 configs where an unequal pair has taller height < n: min error = 8.827e-02 (must be clearly > 0)
[B(b)] control, non-alternating f at n=3 heights (2,1): identity error/N = 3.967e+00; (coef*N - Re<f,Kf>)/N = -2.427e+00
[Fig1 config n=4, heights 3,2,2,1] slack/N = 6.4769, B(b) err = 4.70e-14, ctl taller-source err = 12.000, ctl wrong-divisor err = 2.125
```

Reading the two control lines: with the taller column as source the error is at least 2 (in units of ‖f‖²) in all 116 configurations with unequal heights, and with the wrong divisor it is at least 0.088 in all 81 configurations where the divisor can matter. The last control line shows that the identity fails for a tensor that is not column-alternating. A larger exact run, `check_exact.py` in the same folder, gives 239 configurations with no failure, with 134 of 134 and 74 of 74 controls rejected.

The paper does not attribute the identity inside Theorem B. Section 10 says one reviewer checked it in 13 configurations and the consolidating model checked it algebraically; both statements match the record (finding 18).

### 4. OK. Theorem B(c) and the equality statement of Section 5.1

(c) follows from (b): the right side is a sum of squared norms with positive weights, so it vanishes exactly when every Y_p f = f.

Section 5.1 (lines 1116–1126) says equality holds exactly on the constituent of highest weight λ tensored with V'. That needs Γ_n(μ) < Γ_n(λ) strictly for μ ≠ λ (Proposition 10(ii)) and multiplicity one of the weight λ, which holds because the only way to reach the partial sums Σ_c min(k,h_c) for every k is the highest wedge in every column.

I tested the two descriptions against each other and against the Weyl dimension formula. For 19 configurations, `check_classical.py` builds an orthonormal basis of the column-alternating tensors, restricts K to it, and reports the largest eigenvalue, its multiplicity, dim V_λ times the dimension of the alternating tensors on unselected columns, and the dimension of the common solution space of Y_p f = f. All four agree in every configuration, and every eigenvalue of K is a value Γ_n(μ) with μ dominated by λ. In 13 of the 19 the equality space is a proper subspace of the column-alternating tensors, so the match of dimensions is not automatic:

```
=== Equality case (Thm B(c), Section 5.1) and spectrum of K on the column-alternating space ===
n=2 cols(H,selected)=[(2, 2), (1, 1)]: dim alt=2, max eig K=6.000000, coef=6, Gamma(lambda=[2, 1])=6, top mult=2, predicted dimV_lambda*unsel=2, dim{Y_p f=f}=2, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=2 cols(H,selected)=[(1, 1), (1, 1)]: dim alt=4, max eig K=6.000000, coef=6, Gamma(lambda=[2, 0])=6, top mult=3, predicted dimV_lambda*unsel=3, dim{Y_p f=f}=3, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(2, 2), (1, 1)]: dim alt=9, max eig K=9.000000, coef=9, Gamma(lambda=[2, 1, 0])=9, top mult=8, predicted dimV_lambda*unsel=8, dim{Y_p f=f}=8, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(2, 2), (2, 2)]: dim alt=9, max eig K=12.000000, coef=12, Gamma(lambda=[2, 2, 0])=12, top mult=6, predicted dimV_lambda*unsel=6, dim{Y_p f=f}=6, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(1, 1), (1, 1), (1, 1)]: dim alt=27, max eig K=15.000000, coef=15, Gamma(lambda=[3, 0, 0])=15, top mult=10, predicted dimV_lambda*unsel=10, dim{Y_p f=f}=10, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(3, 3), (1, 1)]: dim alt=3, max eig K=8.000000, coef=8, Gamma(lambda=[2, 1, 1])=8, top mult=3, predicted dimV_lambda*unsel=3, dim{Y_p f=f}=3, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(2, 2), (1, 1), (1, 1)]: dim alt=27, max eig K=16.000000, coef=16, Gamma(lambda=[3, 1, 0])=16, top mult=15, predicted dimV_lambda*unsel=15, dim{Y_p f=f}=15, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=4 cols(H,selected)=[(2, 2), (1, 1)]: dim alt=24, max eig K=12.000000, coef=12, Gamma(lambda=[2, 1, 0, 0])=12, top mult=20, predicted dimV_lambda*unsel=20, dim{Y_p f=f}=20, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=4 cols(H,selected)=[(3, 3), (2, 2)]: dim alt=24, max eig K=16.000000, coef=16, Gamma(lambda=[2, 2, 1, 0])=16, top mult=20, predicted dimV_lambda*unsel=20, dim{Y_p f=f}=20, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=4 cols(H,selected)=[(2, 2), (2, 2)]: dim alt=36, max eig K=16.000000, coef=16, Gamma(lambda=[2, 2, 0, 0])=16, top mult=20, predicted dimV_lambda*unsel=20, dim{Y_p f=f}=20, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(2, 2), (1, 1), (2, 0)]: dim alt=27, max eig K=9.000000, coef=9, Gamma(lambda=[2, 1, 0])=9, top mult=24, predicted dimV_lambda*unsel=24, dim{Y_p f=f}=24, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(2, 2), (2, 2), (1, 1)]: dim alt=27, max eig K=19.000000, coef=19, Gamma(lambda=[3, 2, 0])=19, top mult=15, predicted dimV_lambda*unsel=15, dim{Y_p f=f}=15, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=4 cols(H,selected)=[(3, 3), (1, 1), (1, 1)]: dim alt=64, max eig K=20.000000, coef=20, Gamma(lambda=[3, 1, 1, 0])=20, top mult=36, predicted dimV_lambda*unsel=36, dim{Y_p f=f}=36, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(2, 2), (1, 1), (1, 0)]: dim alt=27, max eig K=9.000000, coef=9, Gamma(lambda=[2, 1, 0])=9, top mult=24, predicted dimV_lambda*unsel=24, dim{Y_p f=f}=24, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=4 cols(H,selected)=[(2, 2), (1, 1), (1, 1)]: dim alt=96, max eig K=20.000000, coef=20, Gamma(lambda=[3, 1, 0, 0])=20, top mult=45, predicted dimV_lambda*unsel=45, dim{Y_p f=f}=45, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=2 cols(H,selected)=[(2, 2), (2, 2), (1, 1)]: dim alt=2, max eig K=14.000000, coef=14, Gamma(lambda=[3, 2])=14, top mult=2, predicted dimV_lambda*unsel=2, dim{Y_p f=f}=2, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(3, 3), (3, 3)]: dim alt=1, max eig K=12.000000, coef=12, Gamma(lambda=[2, 2, 2])=12, top mult=1, predicted dimV_lambda*unsel=1, dim{Y_p f=f}=1, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(1, 1)]: dim alt=3, max eig K=3.000000, coef=3, Gamma(lambda=[1, 0, 0])=3, top mult=3, predicted dimV_lambda*unsel=3, dim{Y_p f=f}=3, all eigs are Gamma(mu), mu<=lambda: True, OK=True
n=3 cols(H,selected)=[(2, 0)]: dim alt=3, max eig K=0.000000, coef=0, Gamma(lambda=[0, 0, 0])=0, top mult=3, predicted dimV_lambda*unsel=3, dim{Y_p f=f}=3, all eigs are Gamma(mu), mu<=lambda: True, OK=True
ALL OK: True
```

### 5. OK. The Observation (lines 252–267)

The proof is complete: distinctness gives injectivity of b on S_c, upward closure from the box of least label gives every higher label in column c, and whole-column selection puts those boxes in S because c is active. The three consequences follow. The label-to-height reading it supports is used correctly in Remark (1) after Proposition 7 and in Section 5.1 (λ_j = m_{n−j} = number of active columns of height at least j).

### 6. OK. Running example and Figure 1

Example (n = 2, column {p_1,p_2} with labels 0,1, column {p_3} with label 1, f = (|010⟩ − |100⟩)/√2): labels 0,1,1 satisfy the tableau condition; m = (1,2); coefficient 1·0 + 2·3 = 6 by labels and 2 + 2 + 2·1 = 6 by heights; P_{p_1p_2} f = −f; ⟨f, P_{p_1p_3} f⟩ = ⟨f, P_{p_2p_3} f⟩ = 1/2; Yf = f; K = 6·Id + 2(P_12 + P_13 + P_23), confirmed from the matrix-unit definition; ⟨f,Kf⟩ = 6 − 2 + 2 = 6. See the `[Example]` lines of the output under finding 3.

Figure 1 (n = 4, heights 3,2,2,1): m = (0,1,3,4); label terms 0, 0, 12, 28, sum 40; height terms 6, 6, 6, 4 and Σ min = 2+2+1+2+1+1 = 9, so 22 + 18 = 40. See the `[Fig1]` line. In the PDF (page 4) the figure renders as intended: c_1 holds labels 1,2,3, c_2 and c_3 hold 2,3, c_4 holds 3. For a random column-alternating tensor in this configuration (dimension 4^8) the identity of Theorem B(b) holds to 5·10⁻¹⁴.

### 7. OK. Proposition 10 (dominance comparison)

(i) A weight of the product is a sum of 0/1 vectors with h_c ones, so its first k coordinates sum to at most Σ_c min(k,h_c) = Σ_{j≤k} λ_j, with equality at k = n. (ii) Γ_n(λ) − Γ_n(μ) = Σ_j (λ_j−μ_j)v_j = Σ_{k<n} D_k (v_k − v_{k+1}) + D_n v_n, D_n = 0, and v_k − v_{k+1} = (λ_k−λ_{k+1}) + (μ_k−μ_{k+1}) + 2 ≥ 2. Equality forces every D_k = 0. Both parts are right, including for dominant weights with negative entries.

```
=== Proposition 10: dominance (i) and Casimir comparison (ii) ===
(i)  dominant weights of products of exterior powers checked: 881, dominance violations: 0
(ii) Gamma(mu) > Gamma(lambda): 0;  Gamma(mu) == Gamma(lambda) with mu != lambda: 0
(ii) random dominant integer weights with mu dominated by lambda: 3836 pairs, violations 0, equality with mu!=lambda 0; summation-by-parts formula asserted on all
(ii) control (dominance dropped): 656 pairs with Gamma(mu) > Gamma(lambda)  (must be > 0)
```

### 8. OK. Proposition 11 (transfer squares) and its link to the pair deficit

T†T = Σ_{i,j} A_i†A_j ⊗ A_iA_j† and A_iA_j† = δ_ij − A_j†A_i give h_c·Id − Σ_{i,j} A_i†A_j ⊗ A_j†A_i; under normalized alternation A_i†A_j is Σ_{p∈S_c} E^(p)_{ij}, and Proposition 1 turns the double sum into X_cc'. For T' the same computation gives h_c'. I built the exterior-algebra operators and the normalized-alternation isometry and compared matrices for every pair of heights with n ≤ 4, including h_c = 0 and h_c' = n where T = 0:

```
=== Proposition 11: transfer squares in the exterior realization ===
n=2 h_c=1 h_c'=0: |T^dag T-(h_c-X)|=0.0e+00, |T'^dag T'-(h_c'-X)|=0.0e+00, |diag(T^dag T)-deficit/(h_c'+1)|=0.0e+00, control |T^dag T-(h_c'-X)|=1.00
n=2 h_c=2 h_c'=2: |T^dag T-(h_c-X)|=8.9e-16, |T'^dag T'-(h_c'-X)|=8.9e-16, |diag(T^dag T)-deficit/(h_c'+1)|=0.0e+00, control |T^dag T-(h_c'-X)|=0.00
n=3 h_c=1 h_c'=2: |T^dag T-(h_c-X)|=2.2e-16, |T'^dag T'-(h_c'-X)|=2.2e-16, |diag(T^dag T)-deficit/(h_c'+1)|=3.3e-16, control |T^dag T-(h_c'-X)|=1.00
n=3 h_c=2 h_c'=1: |T^dag T-(h_c-X)|=2.2e-16, |T'^dag T'-(h_c'-X)|=2.2e-16, |diag(T^dag T)-deficit/(h_c'+1)|=4.4e-16, control |T^dag T-(h_c'-X)|=1.00
n=3 h_c=3 h_c'=1: |T^dag T-(h_c-X)|=2.2e-16, |T'^dag T'-(h_c'-X)|=2.2e-16, |diag(T^dag T)-deficit/(h_c'+1)|=4.4e-16, control |T^dag T-(h_c'-X)|=2.00
n=4 h_c=2 h_c'=2: |T^dag T-(h_c-X)|=8.9e-16, |T'^dag T'-(h_c'-X)|=8.9e-16, |diag(T^dag T)-deficit/(h_c'+1)|=8.9e-16, control |T^dag T-(h_c'-X)|=0.00
Prop 11 all (n<=4) OK: True
A_i^dag A_j vs sum_p E^(p)_ij under normalized alternation (n=4,h=2): max error 2.2e-16
```

The third column is the statement ‖Tf‖² = (1/(h_c'+1)) Σ_{p∈S_c} ‖f − Y_p f‖² of lines 1182–1185, checked with either column as the source. The control (the wrong height) is off by |h_c − h_c'|, which is zero only when the two heights are equal.

### 9. OK. Remaining new or rewritten mathematics

- Projector paragraph before Proposition 3 (lines 521–542): Af = (f − Yf)/(s+1), the coset count, and the contents 1 and −s. Remarks (1) to (4) after Proposition 3: Y² f = s f − (s−1)Yf, (Y − Id)(Y + s·Id) = 0 on tensors alternating on B, (Id−Y)² f = (s+1)(Id−Y) f, the norm ratio s on fully alternating tensors, and Yf = (2−s)f when p ∈ B.
- Content route (Section 5.3): K = nd·Id + 2Z, twice the content sum is Σ_j μ_j(μ_j+1−2j), so nd plus it is Γ_n(μ); conjugation step μ' ⊵ α ⟹ μ ⊴ α' = λ.
- Section 4: largest eigenvalue nd + d(d−1) on the whole space; coefficients 6 (two one-box columns at n = 2) and 8 (two full columns at n = 2); 2h_ch_c'N against (h_c+h_c')N against 2min·N, with 4N and 2N at heights 3 and 1; the partly selected column (m = (1,0), coefficient 0, K = 2·Id); and the terminal-subcolumn variant.
- Remarks after Propositions 7, 8 and 9, including 2·C(m_i,2)·N = m_i(m_i−1)N and n·h − h(h−1) = n at h = n.
- Section 6: the twist changes the Casimir by −2t|S| + nt² (`cas_shift`, SumFinVal.lean:33–37, whose right side is K f − (2s|S| − n s²) f); ν_τ(i) = t − l_τ(w_τ(i)) − i is nonnegative and nondecreasing (`sort_data`, PKTypeA.lean:207–257); the added pairs contribute i occurrences of the label i (`cnt1`, `cnt2`, `cntF`, PKTypeA.lean:135–182); m_i = ν_τ(i) on the fibre (CoefGlueHolds.lean:97).

```
=== Content formula: nd + 2*content(mu) == Gamma_n(mu) ===
partition/rank pairs checked: 555, mismatches: 0

=== Projector formula Af=(f-Yf)/(s+1), spectrum of Y, remark (4) ===
max error of Af=(f-Yf)/(s+1) and of ||f||^2-Re<f,Yf>=||f-Yf||^2/(s+1): 3.6e-15;  of Y^2 f = s f-(s-1)Yf: 1.4e-15
remark (4), s=2, p in B: Yf = (2-s)f = 0: True ; so Y^2 f = 0 while s f-(s-1)Yf = 2f != 0

=== Section 4 claims ===
n=2, d=2: largest eigenvalue of K on the whole space = 6.000000, nd+d(d-1) = 6
n=2, d=3: largest eigenvalue of K on the whole space = 12.000000, nd+d(d-1) = 12
n=3, d=2: largest eigenvalue of K on the whole space = 8.000000, nd+d(d-1) = 8
n=3, d=3: largest eigenvalue of K on the whole space = 15.000000, nd+d(d-1) = 15
two full columns at n=2: coefficient = 8 (paper: 8)
two one-box columns at n=2: coefficient = 6 (paper: 6)
partly selected column: m = [1, 0]  coefficient = 0  Re<f,Kf>/||f||^2 = 2.0

=== Terminal-subcolumn variant (Section 4.3) and a non-terminal control ===
terminal subcolumns: 789 cases, min slack/N = -2.667e-14 (>= -1e-9 means the bound held), max error of the sum-of-squares identity = 7.9e-14
control, non-terminal selections in one column: 6 of 6 violate the bound (must be > 0)
```

The terminal-subcolumn variant holds in all 789 cases tried, and so does the identity of Theorem B(b) with the heights of the selected parts. The control (a selection that is not closed upward in the labels) breaks the bound in 6 of 6 cases.

### 10. MATH-GAP (fixable, minor). The abstract's inequality has no labels, and no sentence derives it from Theorems A and B

The abstract (lines 72–80) and inequality (1) (lines 103–116) are stated for any boxes in columns, any column-alternating f and any union of whole columns with heights h_c ≤ n. No label map appears. Theorem B(a) gives the heights coefficient "under the hypotheses of Theorem A", which include a label map b satisfying the tableau condition on all of Q. The Observation goes from labels to heights only. Nothing in the paper says that a label map always exists.

Evidence: `grep -n -i -E "assign|labelling|labeling" paper.tex` returns only lines 305, 308, 329, 422, 465, 466 and 813, all about the coordinate assignment x. The closest sentence is lines 271–273 ("on S, the data (γ,b) amount to the heights h_c"), which again starts from given labels.

The statement is true, and the missing argument is two sentences: give the boxes of each column of height H ≤ n the labels n−H,…,n−1, which satisfies both parts of the tableau condition, and apply Theorems A and B(a); if some column has more than n boxes then f = 0 and (1) is trivial. Numerical support: the runs under finding 3 choose configurations by heights alone (labels are derived), include unselected columns, and never violate the bound. The classical proof of Section 5.1 also yields the label-free statement for n ≥ 1.

Suggested fix: add those two sentences after the Observation, or in the comments after Theorem B.

### 11. EXPOSITION (concordance). The sub-ranges quoted for Theorem A in Table 1 are shifted by one line

Line 1363 says: "Expansion at lines 11–19, symmetry 22–23, same-column value 24–25, one-box bound 26–32." The file reads:

```
  CasBoundHolds.lean:19:   rw [key]
  CasBoundHolds.lean:20:   refine cas_count hT hS (fun p q => (star f ⬝ᵥ pm (Equiv.swap p q) f).re) _ ?_ ?_ ?_
  CasBoundHolds.lean:21:   · intro p q
  CasBoundHolds.lean:22:     simp only [Equiv.swap_comm]
  CasBoundHolds.lean:23:   · intro p q hpq hne
  CasBoundHolds.lean:24:     simp [hf p q hpq hne]
  CasBoundHolds.lean:25:   · intro p _ c hc
  CasBoundHolds.lean:26:     have h1 := re_swapSum_le' f (S.filter fun q => col q = c) p
```

Symmetry is lines 21–22, the same-column value is 23–24, and the one-box bound is 25–32. "Expansion 11–19" is right. All other sub-ranges in Table 1 (Propositions 3, 7 and 9) are right.

### 12. EXPOSITION (concordance). "All declarations below are in the namespace PositivityTheory.Rg.Cz" is not true of Table 3

Line 1337. It holds for Tables 1 and 2. In Table 3, `cas_shift` and `arith` are in `PositivityTheory.Rg.Cz.CGlue` (SumFinVal.lean:10), the PKTypeA.lean items are in `...Cz.KTy` (line 9), `om_ne` is in `...Cz.Coch` (CochainHolds.lean:9), `exists_min` and `Jm` are in `...Cz.J` (Summand.lean:11), and the definition at ClozelCohomologicalModel.lean:10–12 is in `GlobalTheory.Published` (line 8 of that file). Reproduce with `grep -n "^namespace" <file>`. Suggested fix: restrict the sentence to Tables 1 and 2, or say "in or below that namespace, except the statement `GlobalTheory.Published.ClozelCohomological`".

### 13. EXPOSITION (concordance). One location in Table 3 does not fit its row

Line 1433: "The Lie-action formula on the fiber" cites IsStarRep.lean:75–80 and 95–98. Lines 75–80 are `BigCx`, which is that formula. Lines 95–98 are `CasVal`: the trace and the Casimir scalar of a family with a given characteristic polynomial. That is the source of the scalar κ_τ, not a Lie-action formula. The pairing is inherited from a grouped citation in version 1 (v1 lines 149–155), where the sentence also covered the Casimir scalar. Suggested fix: move 95–98 to the row for the identity `arith` or give `CasVal` its own row.

Every other row of the three tables is right. `python3 /tmp/casbound-v2-verifier/check_concordance.py` (Appendix F) tests, for 40 file-and-range entries, that the first line opens the named declaration and the last line closes it, and that the same range shifted by one line is rejected:

```
rows: 40 failures: 0
(40 lines "OK <file>:<range> <declaration> (shifted-by-one control rejected: True)" precede this line)
```

Where the paper cites only a first line or a statement (KTypeHolds.lean:27, SumFinVal.lean:111–114, ClozelCohomologicalOf.lean:39–43) the script checks the opening line against the whole declaration and I read the cited lines by eye, as I did for the Table 2 row `TV`, `eAt`, `tE`, `pm` (KTypeData.lean:12–27, which also contains `lift` and `Om`). I read the remaining Table 3 ranges, which cite parts of proofs, by eye: ClozelCohomologicalOfThree.lean:11 (the one caller; `rg casBound_holds` over the tree finds only this use), ClozelCohomologicalOfRest.lean:19–21, CoefGlueHolds.lean:120–150 with the call at 144, SumFinVal.lean:33–37, KugaGlueHolds.lean:15–21 and 80–100, PKTypeA.lean:135–182 and 207–220, PKType.lean:26–47, ClozelCohomologicalOf.lean:37–49 and 39–43. Each contains what its row says. The counts of Section 1.2 also hold: ten files in the import closure outside Mathlib, 975 lines, 466 of them in the five proof files (34+96+87+92+157), and no `sorry`, `admit` or `axiom` token.

### 14. EXPOSITION (labels and Limitations). Marking is complete for results; three small statements are unmarked and unlisted

Every theorem-like item that is not in the Lean carries the mark: Theorem B, Propositions 10 and 11, the Observation, the running example, all six Remarks blocks, the figure caption, the comments after Theorem A (line 372), the projector paragraphs (line 519), Section 3.6 (line 909), Section 4 (line 953) and Section 5 (line 1015). The list in Section 10 (lines 1604–1625) covers all of these.

Not marked and not listed, each minor:
- the label-free reading of the abstract and of (1) (finding 10);
- lines 274–276, "the m_i read from i = n−1 downward form the partition conjugate to the sorted heights" (true, cited to Macdonald, but it sits in unmarked text after the Observation's proof);
- lines 337–339, the identification of K with the quadratic Casimir of gl_n for the trace form (true and classical, no citation at that place, although Section 1.3 says classical facts are cited where used).

Section 1.3 (lines 206–211) gives a shorter list of non-Lean material than Section 10: it omits Figure 1, the comments after Theorem A and the projector paragraphs. Both lists should say the same thing.

### 15. CITATION. Etingof's Theorem 18.9 is about semisimple Lie algebras

Line 1036 cites it for complete reducibility of the U(n) action on the product of exterior powers. The theorem reads, in the cited notes (fetched from the URL in the bibliography, text extracted with pdftotext):

```
Theorem 18.9. Every finite dimensional representation of a semisim-
ple Lie algebra g over a field of characteristic zero is completely re-
ducible, i.e., isomorphic to a direct sum of irreducible representations.
```

gl_n is reductive, not semisimple, so the theorem does not apply as cited. The mathematics is unaffected: the same sentence gives the correct reason (a unitary action, invariant orthogonal complements). Suggested fix: drop the citation, or cite it for sl_n and note that the centre acts by scalars. The same caveat applies in a weaker form to Lemma 26.6 (stated for semisimple g), where the paper already adds Yang's gl_N formula and the remark on the scalar direction.

### 16. EXPOSITION. Three wording points

- Lines 963–965: "has excess 2d(d−1), which is 6 against 2 at n = d = 2". The excess at d = 2 is 4; 6 and 2 are the two coefficients. Version 1 said "giving 6 versus 2" (v1 line 502).
- Theorem B(b), lines 395–397: Y_p depends on the pair, not only on p, since a box of the shortest column is paired with several taller columns. Writing Y_p^{c'} or saying "for the pair in question" removes the ambiguity.
- Remark (2) after Proposition 7, lines 768–771, uses ℓ_c' when S_c' may be empty. Version 1 set the least label of an empty column to n (v1 line 788); version 2 dropped the convention.

### 17. OK. New pinpoints and quotations in version 2, checked against fetched sources

Version 2 says its writer did not fetch the literature again, so I checked what is new relative to version 1 (found by diffing the `\cite` keys and optional arguments of the two files). Sources were downloaded to `/tmp/casbound-v2-verifier/dl/` and searched as text.

| New in version 2 | Result |
|---|---|
| Etingof, Theorem 18.9 | exists and is complete reducibility, but for semisimple g (finding 15) |
| Etingof, Lemma 26.6 | "If V is a highest weight representation with highest weight λ then C\|V = (λ, λ + 2ρ)". Correct |
| Gross–Taylor (2.1), "written with that subtraction" | (2.1) is C_2(R) = nN + C̃(R) − n²/N and (2.2) is the row and column formula. Correct |
| Okounkov–Vershik (2.1), Proposition 6.2, Theorem 6.4 | (2.1) defines the Jucys–Murphy elements, 6.2 is the content map on tableaux, 6.4 is Spec(n) = Cont(n). Correct |
| Hazewinkel–Martin §6.10 | heading "The Implication κ < λ ⇒ ρ(κ) is a subrepresentation of ρ(λ)" (the scan reads "K < A. => p(K) is a subrepresentation of p(A.)"), the converse the paper says it does not need; 6.5 (Young's rule) and 6.9 (necessity) are as cited. Correct |
| Joint statement [JointStatement] | dated 2026-11-21; contains "On November 20, 2026, Levent Alpöge released a proof of the Riemann Hypothesis as a Lean library" and "We hereby certify that both the statement and the proof of the Riemann Hypothesis are correct"; names Mathlib's RiemannHypothesis; the words "generalized Riemann hypothesis" and "GRH" do not occur in its text (one linked URL has `grh` in its path). Correct |
| Quotations from Alpöge's remark (lines 159–161) | both sentences are in remark.pdf; the second continues "without assumptions". Footnote 1 of the remark links the fourteen parts. Correct |

Not re-fetched: the citations carried over from version 1 with unchanged pinpoints (Baur, Baur's thesis, Jucys, Molev, Lévy, Cautis–Kamnitzer–Morrison, Howe, Cesi, Macdonald, Etingof's GL_n notes, Yang, Perelomov–Popov, Gleizer–Postnikov, Gross, Hazewinkel–Vorst), the nine write-ups, the Rodgers title and DOI, the Zenodo and Hexagon identifiers of version 1, and the SHA-256 of part 01.

### 18. OK. Numbers the paper quotes about its own process

Checked against the files in this folder by search, after the mathematical review was finished.

| Claim in version 2 | Record |
|---|---|
| seven reports; 55 findings; eight defects | seven report files; ADJUDICATION.md line 3: "55 findings: 8 DEFECT, 16 IMPRECISION, 31 STYLE" |
| Theorem B(b) checked numerically in 13 configurations by one reviewer and algebraically by the consolidating model | referee-fable.md line 85; CONSOLIDATED.md line 57 (S6) |
| terminal-subcolumn variant checked in 74 two-column cases | verifier-fable.md line 116 |
| two reviewers recompiled with Lean 4.33.1, one against Mathlib 0df444a3; both report propext, Classical.choice, Quot.sound | verifier-fable.md lines 24 and 381; adversarial-astra.md line 16 |
| running-example totals 6 − 2 + 2 = 6 and Yf = f | proposed and checked by reviewers: CONSOLIDATED.md line 61 (S10); verifier-fable.md line 97; referee-fable.md line 131 |
| the four references removed are two physics papers, an unrefereed preprint and a historical paper | version 1 bibliography: Navrátil–Kamuntavičius–Barrett and Navrátil–Barrett (Phys. Rev. C), Szőke ("author-uploaded preprint"), Frobenius 1900 |

## What I attacked, and why each attack failed

1. Drift between the versions in the ten Lean-backed statements or in the definitions under them: none (finding 1).
2. A displayed statement that the Lean does not prove: the symbol-by-symbol comparison finds none, and a random search with negative N and empty columns finds no counterexample while both controls do (finding 1).
3. Theorem B(b) with the wrong source column, the wrong divisor, ties, unselected columns, columns of full height n, n = 1, complex f: the identity holds exactly; the two wrong variants are rejected (finding 3).
4. Theorem B(c) against the Cartan-component description of equality: the two solution spaces have the same dimension, equal to the Weyl dimension, in 19 configurations (finding 4).
5. Proposition 10 with weights that are not partitions, and without dominance: holds in the first case, fails in the second as it should (finding 7).
6. Proposition 11 at the edges (h_c = 0, h_c' = n) and with the roles of the columns exchanged: holds; the wrong height is rejected (finding 8).
7. Every number in the running example, Figure 1 and Section 4: all recomputed (findings 6 and 9).
8. The concordance tables, line by line, with a shifted-range control: three slips, all minor (findings 11 to 13).
9. Pinpoints and quotations that are new in version 2 and were written without fetching: all exist and say what the paper says, with one scope problem (findings 15 and 17).
10. The open-problem test: the result is the classical Cartan-component bound; no specialization of any statement here would settle an open question.

## Confidence

High that the mathematics of version 2 is right. Theorem A and Propositions 1 to 9 are unchanged text whose match to a compiled Lean proof was established for version 1 and re-read here. Theorem B has a five-step proof from two facts the Lean proves, exact checks on 78 and on 239 configurations, and controls that fail. The equality statements, Propositions 10 and 11 and the content route each passed a check that could have failed, and for Propositions 10 and 11 a deliberately wrong variant was rejected. The residual risk is outside the mathematics: I did not recompile the Lean, I did not re-fetch the citations inherited from version 1, and Section 6 was compared with the Lean only at the locations Table 3 names, not along the whole chain it paraphrases (Whittaker transfer, spherical descent and the Young contraction are named there, not explained, and I did not read their proofs).

## Appendices: scripts

All scripts are in `/tmp/casbound-v2-verifier/`, which may be cleared. To rerun after that, save each listing under its file name in that folder (the scripts import `check_core.py` from that path). Environment: Python 3 with numpy 2.4.2. Run times are a few seconds each.

### Appendix A. `repro_thmB.py` (standalone)

```python
# repro_thmB.py -- standalone exact check of Theorem B(a),(b) of casBound v2, with negative controls.
# Needs only numpy. Integer tensors suffice: every operator is real, so the identity for complex f is the
# sum of the identities for Re f and Im f.
import numpy as np, itertools
from fractions import Fraction
rng = np.random.default_rng(1)

def sign(perm):
    perm = list(perm); s = 1
    for i in range(len(perm)):
        while perm[i] != i:
            j = perm[i]; perm[i], perm[j] = perm[j], perm[i]; s = -s
    return s

def alt(f, axes):                      # unnormalised antisymmetriser on the given slots (keeps integers)
    out = np.zeros_like(f)
    for perm in itertools.permutations(range(len(axes))):
        order = list(range(f.ndim))
        for k, a in enumerate(axes): order[a] = axes[perm[k]]
        out = out + sign(perm) * np.transpose(f, order)
    return out

def P(f, p, q): return np.swapaxes(f, p, q)          # (P_pq f)(x) = f(x o (p q))
def dot(f, g): return int(np.sum(f.astype(object) * g.astype(object)))

def check(n, heights, mode="paper"):
    cols, k = [], 0                                    # all columns selected; column c = consecutive slots
    for h in heights: cols.append(list(range(k, k + h))); k += h
    labels = [n - h + r for h in heights for r in range(h)]          # a column of height h carries n-h..n-1
    m = [labels.count(i) for i in range(n)]
    coef_labels = sum(m[i] * (m[i] + 2 * i + 1 - n) for i in range(n))
    coef_heights = sum(h * (n + 1 - h) for h in heights) + 2 * sum(min(a, b) for a, b in itertools.combinations(heights, 2))
    f = rng.integers(-3, 4, size=(n,) * k).astype(np.int64)
    for c in cols: f = alt(f, c)
    N = dot(f, f)
    Kf = n * k * f + sum(P(f, p, q) for p in range(k) for q in range(k) if p != q)   # Proposition 2
    lhs = Fraction(coef_labels * N - dot(f, Kf))
    rhs = Fraction(0)
    for a, b in itertools.combinations(range(len(cols)), 2):
        if len(cols[a]) > len(cols[b]): a, b = b, a                  # a = shorter (source), b = taller (target)
        if mode == "taller_source": a, b = b, a
        div = len(cols[b]) + 1 if mode != "wrong_divisor" else len(cols[a]) + 1
        s = 0
        for p in cols[a]:
            g = f - sum(P(f, p, q) for q in cols[b])
            s += dot(g, g)
        rhs += Fraction(2 * s, div)
    return coef_labels, coef_heights, N, lhs, rhs

bad_a = 0
for n in range(0, 9):
    for k in range(0, 7):
        for hs in itertools.combinations_with_replacement(range(1, n + 1), k):
            m = [sum(1 for h in hs if h >= n - i) for i in range(n)]        # m_i = number of columns of height >= n-i
            by_labels = sum(m[i] * (m[i] + 2 * i + 1 - n) for i in range(n))
            by_heights = sum(h * (n + 1 - h) for h in hs) + 2 * sum(min(a, b) for a, b in itertools.combinations(hs, 2))
            bad_a += (by_labels != by_heights)
print("B(a): mismatches over all height multisets, n<=8, <=6 columns:", bad_a)
print("Figure 1 (n=4, heights 3,2,2,1): coefficient by labels, by heights =", check(4, [3, 2, 2, 1])[:2])
print("Running example (n=2, heights 2,1): coefficient by labels, by heights =", check(2, [2, 1])[:2])
tot = fail = c1 = c1r = c2 = c2r = 0
for n in range(1, 5):
    for k in range(2, 5):
        for hs in itertools.combinations_with_replacement(range(1, n + 1), k):
            if n ** sum(hs) > 70000: continue
            state = rng.bit_generator.state
            cl, ch, N, lhs, rhs = check(n, list(hs))
            if N == 0: continue
            tot += 1; fail += (lhs != rhs) or (cl != ch)
            if len(set(hs)) > 1:
                rng.bit_generator.state = state; r1 = check(n, list(hs), "taller_source")[4]; c1 += 1; c1r += (r1 != lhs)
                if rhs != 0 and any(a != b and max(a, b) < n for a, b in itertools.combinations(hs, 2)):
                    rng.bit_generator.state = state; r2 = check(n, list(hs), "wrong_divisor")[4]; c2 += 1; c2r += (r2 != lhs)
print(f"B(b): {tot} configurations in exact arithmetic, failures: {fail}")
print(f"control, taller column as source: rejected {c1r} of {c1}")
print(f"control, divisor h_c+1 instead of h_c'+1: rejected {c2r} of {c2}")
rng = np.random.default_rng(3); print("one instance, n=3, heights (2,1): (coef_labels, coef_heights, ||f||^2, LHS, RHS) =", check(3, [2, 1]))
```

### Appendix B. `compare_statements.py`

```python
# compare the displayed statements of the main theorem and Propositions 1-9 in v1 and v2 (whitespace-normalised)
import re
v1 = open('local-source/_Scratch/mathematics-codex/vance-casbound-review/in/paper.tex', encoding='utf-8').read()
v2 = open('local-source/_Scratch/mathematics-codex/vance-casbound-v2/v2/paper/paper.tex', encoding='utf-8').read()
def envs(t, names):
    out = {}
    for m in re.finditer(r'\\begin\{(' + '|'.join(names) + r')\}(\[[^\n]*\])?\\label\{([^}]*)\}(.*?)\\end\{\1\}', t, re.S):
        out[m.group(3)] = re.sub(r'\s+', ' ', m.group(4)).strip()
    return out
e1 = envs(v1, ['theorem', 'proposition']); e2 = envs(v2, ['maintheorem', 'proposition'])
pairs = [('thm:bound', 'thm:A')] + [(f'prop:{i}', f'prop:{i}') for i in range(1, 10)]
for a, b in pairs:
    print(f"{a:10s} -> {b:7s} identical: {e1[a] == e2[b]}   ({len(e1[a])} chars)")
# negative control: one changed character must be detected
print("control (m_i+2i+1-n changed to m_i+2i-1-n in v2's Theorem A):", e1['thm:bound'] == e2['thm:A'].replace('2i+1-n', '2i-1-n'))
```

### Appendix C. `check_core.py`

```python
import numpy as np, itertools, math, sys
from fractions import Fraction
rng = np.random.default_rng(20261127)

def perm_sign(perm):
    s = 1
    perm = list(perm)
    for i in range(len(perm)):
        while perm[i] != i:
            j = perm[i]
            perm[i], perm[j] = perm[j], perm[i]
            s = -s
    return s

def swap(f, p, q):
    # (P_pq f)(x) = f(x o (p q))
    return f if p == q else np.swapaxes(f, p, q)

def antisym(f, axes):
    h = len(axes)
    if h <= 1: return f
    out = np.zeros_like(f)
    for perm in itertools.permutations(range(h)):
        order = list(range(f.ndim))
        for k, a in enumerate(axes):
            order[a] = axes[perm[k]]
        out = out + perm_sign(perm) * np.transpose(f, order)
    return out / math.factorial(h)

def Eunit(f, p, i, ip, n):
    # (E^{(p)}_{i i'} f)(x) = f(x[p<-i']) if x(p)=i else 0
    g = np.zeros_like(f)
    idx_i = [slice(None)]*f.ndim; idx_i[p] = i
    idx_ip = [slice(None)]*f.ndim; idx_ip[p] = ip
    g[tuple(idx_i)] = f[tuple(idx_ip)]
    return g

def G(f, S, i, ip, n):
    out = np.zeros_like(f)
    for p in S: out = out + Eunit(f, p, i, ip, n)
    return out

def K_def(f, S, n):
    out = np.zeros_like(f)
    for i in range(n):
        for ip in range(n):
            out = out + G(G(f, S, ip, i, n), S, i, ip, n)
    return out

def K_swaps(f, S, n):
    out = n*len(S)*f
    for p in S:
        for q in S:
            if q != p: out = out + swap(f, p, q)
    return out

def inner(f, g): return np.vdot(f, g)   # conj-linear in first

class Cfg:
    """columns: list of (H, t): column has H boxes with labels n-H..n-1; the t boxes of highest labels are selected
       (t==H: whole column selected; t==0: unselected). sel_override lets a test select an arbitrary subset."""
    def __init__(self, n, cols, sel_override=None):
        self.n = n; self.cols = cols
        self.col_of = []; self.label = []; self.S = []
        self.colboxes = []
        k = 0
        for c,(H,t) in enumerate(cols):
            boxes = []
            for r in range(H):
                lab = n-H+r
                self.col_of.append(c); self.label.append(lab)
                if sel_override is None:
                    if lab >= n-t: self.S.append(k)
                boxes.append(k); k += 1
            self.colboxes.append(boxes)
        if sel_override is not None: self.S = list(sel_override)
        self.Q = k
        self.Sc = {c:[p for p in self.S if self.col_of[p]==c] for c in range(len(cols))}
        self.active = [c for c in range(len(cols)) if self.Sc[c]]
        self.h = {c: len(self.Sc[c]) for c in self.active}
        self.m = [sum(1 for p in self.S if self.label[p]==i) for i in range(n)]
    def coef_labels(self):
        n=self.n; return sum(self.m[i]*(self.m[i]+2*i+1-n) for i in range(n))
    def coef_heights(self):
        n=self.n; hs=[self.h[c] for c in self.active]
        return sum(h*(n+1-h) for h in hs) + 2*sum(min(a,b) for a,b in itertools.combinations(hs,2))
    def random_alt(self, complex_=True):
        shape=(self.n,)*self.Q
        f = rng.standard_normal(shape)
        if complex_: f = f + 1j*rng.standard_normal(shape)
        for boxes in self.colboxes: f = antisym(f, boxes)
        return f

def Yp(f, p, target):
    out = np.zeros_like(f)
    for q in target: out = out + swap(f, p, q)
    return out

def rhs_B(cfg, f, mode='paper'):
    tot = 0.0
    for c, cp in itertools.combinations(cfg.active, 2):
        a, b = (c, cp) if cfg.h[c] <= cfg.h[cp] else (cp, c)   # a shorter (source), b taller (target)
        if mode == 'taller_source': a, b = b, a
        div = cfg.h[b] + 1
        if mode == 'wrong_divisor': div = cfg.h[a] + 1
        if mode == 'tie_other' and cfg.h[a]==cfg.h[b]: a, b = b, a; div = cfg.h[b]+1
        s = 0.0
        for p in cfg.Sc[a]:
            g = f - Yp(f, p, cfg.Sc[b])
            s += np.vdot(g, g).real
        tot += s/div
    return 2*tot

def check_cfg(cfg, use_def=False, verbose=False):
    f = cfg.random_alt()
    N = np.vdot(f,f).real
    if N == 0: return None
    Kf = K_swaps(f, cfg.S, cfg.n)
    res = {}
    if use_def:
        Kd = K_def(f, cfg.S, cfg.n)
        res['prop2_err'] = float(np.max(np.abs(Kd-Kf)))
        g = rng.standard_normal(f.shape)+1j*rng.standard_normal(f.shape)   # arbitrary tensor: Prop 2 has no hypotheses
        res['prop2_err_generic'] = float(np.max(np.abs(K_def(g, cfg.S, cfg.n)-K_swaps(g, cfg.S, cfg.n))))
    q = np.vdot(f, Kf)
    res['imag'] = abs(q.imag)/N
    cl, ch = cfg.coef_labels(), cfg.coef_heights()
    res['coef_labels'] = cl; res['coef_heights'] = ch
    lhs = cl*N - q.real
    res['slack_over_N'] = lhs/N
    res['B_b_err'] = abs(lhs - rhs_B(cfg, f))/N
    res['B_b_tie_other_err'] = abs(lhs - rhs_B(cfg, f, 'tie_other'))/N
    res['ctl_taller_source'] = abs(lhs - rhs_B(cfg, f, 'taller_source'))/N
    res['ctl_wrong_divisor'] = abs(lhs - rhs_B(cfg, f, 'wrong_divisor'))/N
    return res

if __name__ == '__main__':
    # ---------- (a) labels form == heights form, exhaustive ----------
    cnt = 0; bad = 0
    for n in range(0, 9):
        for k in range(0, 7):
            for hs in itertools.combinations_with_replacement(range(1, n+1), k):
                cfg_m = [sum(1 for h in hs if h >= n-i) for i in range(n)]
                cl = sum(cfg_m[i]*(cfg_m[i]+2*i+1-n) for i in range(n))
                ch = sum(h*(n+1-h) for h in hs) + 2*sum(min(a,b) for a,b in itertools.combinations(hs,2))
                cnt += 1
                if cl != ch: bad += 1
    print(f"[B(a)] exhaustive n<=8, <=6 columns: {cnt} height multisets, mismatches = {bad}")
    # negative control for (a): drop the factor 2 on the pair sum
    bad2 = 0
    for n in range(1,6):
        for k in range(2,5):
            for hs in itertools.combinations_with_replacement(range(1, n+1), k):
                m = [sum(1 for h in hs if h >= n-i) for i in range(n)]
                cl = sum(m[i]*(m[i]+2*i+1-n) for i in range(n))
                ch = sum(h*(n+1-h) for h in hs) + 1*sum(min(a,b) for a,b in itertools.combinations(hs,2))
                if cl != ch: bad2 += 1
    print(f"[B(a)] control (pair sum without factor 2): mismatches = {bad2} (must be > 0)")

    # ---------- Figure 1 and running example numbers ----------
    fig = Cfg(4, [(3,3),(2,2),(2,2),(1,1)])
    print("[Fig1] m =", fig.m, " per-label terms =", [fig.m[i]*(fig.m[i]+2*i+1-4) for i in range(4)],
          " coef_labels =", fig.coef_labels(), " heights terms =", [h*(5-h) for h in (3,2,2,1)],
          " pair-min sum =", sum(min(a,b) for a,b in itertools.combinations((3,2,2,1),2)), " coef_heights =", fig.coef_heights())
    ex = Cfg(2, [(2,2),(1,1)])
    f = np.zeros((2,2,2), dtype=complex); f[0,1,0] = 1/math.sqrt(2); f[1,0,0] = -1/math.sqrt(2)
    print("[Example] labels =", ex.label, " m =", ex.m, " coef_labels =", ex.coef_labels(), " coef_heights =", ex.coef_heights())
    print("[Example] ||f||^2 =", np.vdot(f,f).real, " P12 f = -f:", np.allclose(swap(f,0,1), -f))
    print("[Example] <f,P13 f> =", np.vdot(f, swap(f,0,2)).real, " <f,P23 f> =", np.vdot(f, swap(f,1,2)).real,
          " Yf = f:", np.allclose(Yp(f,2,[0,1]), f))
    Kf = K_def(f, ex.S, 2)
    print("[Example] K from matrix units vs 6 Id + 2(P12+P13+P23):", np.allclose(Kf, 6*f+2*(swap(f,0,1)+swap(f,0,2)+swap(f,1,2))),
          " Re<f,Kf> =", np.vdot(f,Kf).real)

    # ---------- Theorem B(b) numerically, with controls ----------
    configs = []
    for n in range(1, 5):
        for k in range(0, 5):
            for hs in itertools.combinations_with_replacement(range(1, n+1), k):
                for extra in ([], [(1,0)], [(min(2,n),0)], [(n,0),(1,0)]):
                    Qn = sum(hs) + sum(H for H,_ in extra)
                    if n**Qn > 70000: continue
                    configs.append((n, [(h,h) for h in hs] + extra))
    worst = dict(prop2=0.0, prop2g=0.0, Bb=0.0, tie=0.0, imag=0.0, minslack=1e9)
    ctl_ts_min_when_applicable = 1e9; ctl_wd_min_when_applicable = 1e9; napp = 0; napp_wd = 0
    ncfg = 0; ndef = 0
    for n, cols in configs:
        cfg = Cfg(n, cols)
        use_def = (n**cfg.Q <= 1100)
        r = check_cfg(cfg, use_def=use_def)
        if r is None: continue
        ncfg += 1
        assert r['coef_labels'] == r['coef_heights']
        if use_def:
            ndef += 1
            worst['prop2'] = max(worst['prop2'], r['prop2_err']); worst['prop2g'] = max(worst['prop2g'], r['prop2_err_generic'])
        worst['Bb'] = max(worst['Bb'], r['B_b_err']); worst['tie'] = max(worst['tie'], r['B_b_tie_other_err'])
        worst['imag'] = max(worst['imag'], r['imag']); worst['minslack'] = min(worst['minslack'], r['slack_over_N'])
        hs = [cfg.h[c] for c in cfg.active]
        if len(set(hs)) > 1 and r['slack_over_N'] > 1e-6:      # controls only meaningful with unequal heights and generic f
            napp += 1
            ctl_ts_min_when_applicable = min(ctl_ts_min_when_applicable, r['ctl_taller_source'])
            # the divisor can only matter if some unequal pair has taller height < n (at height n every f - Y_p f is 0)
            if any(a != b and max(a, b) < n for a, b in itertools.combinations(hs, 2)):
                napp_wd += 1
                ctl_wd_min_when_applicable = min(ctl_wd_min_when_applicable, r['ctl_wrong_divisor'])
    print(f"[B(b)] configurations with nonzero column-alternating f: {ncfg} (Prop 2 checked from the matrix-unit definition in {ndef})")
    print(f"[Prop2] max |K_def f - (nd f + sum swaps f)|: alternating f {worst['prop2']:.2e}, arbitrary f {worst['prop2g']:.2e}")
    print(f"[ThmA] min over configs of (coef*N - Re<f,Kf>)/N = {worst['minslack']:.3e} (must be >= -1e-9);  max |Im<f,Kf>|/N = {worst['imag']:.2e}")
    print(f"[B(b)] max relative error of the identity = {worst['Bb']:.2e};  with the other naming in ties = {worst['tie']:.2e}")
    print(f"[B(b)] control, taller column as source, on {napp} configs with unequal heights: min error = {ctl_ts_min_when_applicable:.3e} (must be clearly > 0)")
    print(f"[B(b)] control, divisor h_c+1 (source height), on {napp_wd} configs where an unequal pair has taller height < n: min error = {ctl_wd_min_when_applicable:.3e} (must be clearly > 0)")

    # control: f NOT column-alternating -> identity fails
    cfg = Cfg(3, [(2,2),(1,1)])
    g = rng.standard_normal((3,)*cfg.Q) + 1j*rng.standard_normal((3,)*cfg.Q)
    N = np.vdot(g,g).real; q = np.vdot(g, K_swaps(g, cfg.S, 3)).real
    print(f"[B(b)] control, non-alternating f at n=3 heights (2,1): identity error/N = {abs(cfg.coef_labels()*N - q - rhs_B(cfg,g))/N:.3e}; "
          f"(coef*N - Re<f,Kf>)/N = {(cfg.coef_labels()*N-q)/N:.3e}")

    # Figure-1 configuration itself (dimension 4^8)
    r = check_cfg(fig)
    print("[Fig1 config n=4, heights 3,2,2,1] slack/N = %.4f, B(b) err = %.2e, ctl taller-source err = %.3f, ctl wrong-divisor err = %.3f"
          % (r['slack_over_N'], r['B_b_err'], r['ctl_taller_source'], r['ctl_wrong_divisor']))
```

### Appendix D. `check_classical.py` (needs `check_core.py`)

```python
import numpy as np, itertools, math, sys
sys.path.insert(0, '/tmp/casbound-v2-verifier')
from check_core import *
rng = np.random.default_rng(7)

def Gamma(mu, n):   # Gamma_n(mu) = sum_j mu_j (mu_j + n + 1 - 2j), j = 1..n
    return sum(mu[j-1]*(mu[j-1] + n + 1 - 2*j) for j in range(1, n+1))

def weyl_dim(lam):
    n = len(lam); num = 1; den = 1
    for i in range(n):
        for j in range(i+1, n):
            num *= (lam[i]-lam[j] + j-i); den *= (j-i)
    return num//den

def alt_basis(cfg):
    """orthonormal basis of the column-alternating tensors (all columns of Q): one vector per tuple of H_c-subsets"""
    n = cfg.n; vecs = []; keys = []
    per_col = [list(itertools.combinations(range(n), len(b))) for b in cfg.colboxes]
    for choice in itertools.product(*per_col):
        v = np.zeros((n,)*cfg.Q)
        # product of normalized alternations
        terms = [((), 1.0)]
        assign = {}
        def rec(ci, idx, coeff):
            if ci == len(cfg.colboxes):
                x = [0]*cfg.Q
                for b, val in idx.items(): x[b] = val
                v[tuple(x)] += coeff; return
            boxes = cfg.colboxes[ci]; sub = choice[ci]; H = len(boxes)
            for perm in itertools.permutations(range(H)):
                d = dict(idx)
                for k, b in enumerate(boxes): d[b] = sub[perm[k]]
                rec(ci+1, d, coeff*perm_sign(perm)/math.sqrt(math.factorial(H)))
        rec(0, {}, 1.0)
        vecs.append(v.reshape(-1)); keys.append(choice)
    return np.array(vecs).T, keys      # columns

def op_matrix_on_alt(cfg, B, op):
    cols = []
    for k in range(B.shape[1]):
        f = B[:,k].reshape((cfg.n,)*cfg.Q)
        cols.append(op(f).reshape(-1))
    return B.T @ np.array(cols).T

def lam_of(cfg):
    n = cfg.n; hs = [cfg.h[c] for c in cfg.active]
    return [sum(1 for h in hs if h >= j) for j in range(1, n+1)]

print("=== Equality case (Thm B(c), Section 5.1) and spectrum of K on the column-alternating space ===")
tests = [(2,[(2,2),(1,1)]), (2,[(1,1),(1,1)]), (3,[(2,2),(1,1)]), (3,[(2,2),(2,2)]), (3,[(1,1),(1,1),(1,1)]), (3,[(3,3),(1,1)]),
         (3,[(2,2),(1,1),(1,1)]), (4,[(2,2),(1,1)]), (4,[(3,3),(2,2)]), (4,[(2,2),(2,2)]), (3,[(2,2),(1,1),(2,0)]), (3,[(2,2),(2,2),(1,1)]),
         (4,[(3,3),(1,1),(1,1)]), (3,[(2,2),(1,1),(1,0)]), (4,[(2,2),(1,1),(1,1)]), (2,[(2,2),(2,2),(1,1)]), (3, [(3,3),(3,3)]), (3,[(1,1)]), (3,[(2,0)])]
allok = True
for n, cols in tests:
    cfg = Cfg(n, cols)
    B, keys = alt_basis(cfg)
    assert np.allclose(B.T @ B, np.eye(B.shape[1]))
    # image of K stays in the alt space?
    KB = np.array([K_swaps(B[:,k].reshape((n,)*cfg.Q), cfg.S, n).reshape(-1) for k in range(B.shape[1])]).T
    leak = np.max(np.abs(KB - B @ (B.T @ KB)))
    Kalt = B.T @ KB
    ev = np.linalg.eigvalsh((Kalt+Kalt.T)/2)
    coef = cfg.coef_labels(); lam = lam_of(cfg)
    top_mult = int(np.sum(np.abs(ev - coef) < 1e-8))
    # predicted: dim V_lambda * dim(alt tensors on unselected columns)
    unsel = 1
    for c, boxes in enumerate(cfg.colboxes):
        if c not in cfg.active: unsel *= math.comb(n, len(boxes))
    pred = weyl_dim(lam) * unsel
    # equality space via Thm B(c): common kernel of (1 - Y_p) over pairs, p in shorter column
    Dm = np.zeros_like(Kalt)
    for c, cp in itertools.combinations(cfg.active, 2):
        a, b = (c, cp) if cfg.h[c] <= cfg.h[cp] else (cp, c)
        for p in cfg.Sc[a]:
            cols_ = np.array([(B[:,k].reshape((n,)*cfg.Q) - Yp(B[:,k].reshape((n,)*cfg.Q), p, cfg.Sc[b])).reshape(-1) for k in range(B.shape[1])]).T
            Dm += cols_.T @ cols_
    evD = np.linalg.eigvalsh((Dm+Dm.T)/2)
    kerdim = int(np.sum(evD < 1e-8))
    # are all eigenvalues of K Casimir scalars Gamma(mu) with mu dominated by lambda?
    hs = [cfg.h[c] for c in cfg.active]
    d = sum(hs)
    cand = set()
    def parts(total, maxpart, length):
        if length == 0:
            if total == 0: yield []
            return
        for first in range(min(total, maxpart), -1, -1):
            for rest in parts(total-first, first, length-1): yield [first]+rest
    for mu in parts(d, d, n):
        if all(sum(mu[:k]) <= sum(lam[:k]) for k in range(1, n+1)): cand.add(Gamma(mu, n))
    in_cand = all(any(abs(e - g) < 1e-8 for g in cand) for e in ev)
    ok = (leak < 1e-10 and abs(ev.max()-coef) < 1e-8 and top_mult == pred and kerdim == top_mult and in_cand and Gamma(lam, n) == coef)
    allok &= ok
    print(f"n={n} cols(H,selected)={cols}: dim alt={B.shape[1]}, max eig K={ev.max():.6f}, coef={coef}, Gamma(lambda={lam})={Gamma(lam,n)}, "
          f"top mult={top_mult}, predicted dimV_lambda*unsel={pred}, dim{{Y_p f=f}}={kerdim}, all eigs are Gamma(mu), mu<=lambda: {in_cand}, OK={ok}")
print("ALL OK:", allok)

print("\n=== Proposition 10: dominance (i) and Casimir comparison (ii) ===")
cnt_i = 0; viol_i = 0; cnt_ii = 0; viol_ii = 0; eq_nonlam = 0
for n in range(1, 6):
    for k in range(0, 5):
        for hs in itertools.combinations_with_replacement(range(1, n+1), k):
            lam = [sum(1 for h in hs if h >= j) for j in range(1, n+1)]
            # all weights of the product: sums of indicator vectors of h_c-subsets
            wts = {tuple([0]*n)}
            for h in hs:
                new = set()
                for w in wts:
                    for sub in itertools.combinations(range(n), h):
                        v = list(w)
                        for i in sub: v[i] += 1
                        new.add(tuple(v))
                wts = new
            for w in wts:
                if all(w[i] >= w[i+1] for i in range(n-1)):      # dominant weights (superset of the highest weights of constituents)
                    cnt_i += 1
                    if not (all(sum(w[:kk]) <= sum(lam[:kk]) for kk in range(1, n+1)) and sum(w) == sum(lam)): viol_i += 1
                    cnt_ii += 1
                    if Gamma(w, n) > Gamma(lam, n): viol_ii += 1
                    if Gamma(w, n) == Gamma(lam, n) and list(w) != lam: eq_nonlam += 1
print(f"(i)  dominant weights of products of exterior powers checked: {cnt_i}, dominance violations: {viol_i}")
print(f"(ii) Gamma(mu) > Gamma(lambda): {viol_ii};  Gamma(mu) == Gamma(lambda) with mu != lambda: {eq_nonlam}")
# (ii) for arbitrary dominant integer weights (negative entries allowed) dominated by lambda
viol = 0; tot = 0; eqc = 0
for n in range(1, 6):
    for _ in range(20000):
        lam = sorted(rng.integers(-4, 7, size=n).tolist(), reverse=True)
        mu = sorted(rng.integers(-4, 7, size=n).tolist(), reverse=True)
        if sum(mu) != sum(lam): continue
        if not all(sum(mu[:k]) <= sum(lam[:k]) for k in range(1, n)): continue
        tot += 1
        if Gamma(mu, n) > Gamma(lam, n): viol += 1
        if Gamma(mu, n) == Gamma(lam, n) and mu != lam: eqc += 1
        # summation-by-parts formula
        D = [sum(lam[:k]) - sum(mu[:k]) for k in range(1, n+1)]
        v = [lam[j-1] + mu[j-1] + n + 1 - 2*j for j in range(1, n+1)]
        assert Gamma(lam, n) - Gamma(mu, n) == sum(D[k-1]*(v[k-1]-v[k]) for k in range(1, n))
        assert all(v[k-1]-v[k] >= 2 for k in range(1, n))
print(f"(ii) random dominant integer weights with mu dominated by lambda: {tot} pairs, violations {viol}, equality with mu!=lambda {eqc}; summation-by-parts formula asserted on all")
# control: without dominance, Gamma(mu) <= Gamma(lambda) fails
ctl = 0
for _ in range(20000):
    n = 3
    lam = sorted(rng.integers(0, 6, size=n).tolist(), reverse=True); mu = sorted(rng.integers(0, 6, size=n).tolist(), reverse=True)
    if sum(mu) == sum(lam) and not all(sum(mu[:k]) <= sum(lam[:k]) for k in range(1, n)) and Gamma(mu, n) > Gamma(lam, n): ctl += 1
print(f"(ii) control (dominance dropped): {ctl} pairs with Gamma(mu) > Gamma(lambda)  (must be > 0)")

print("\n=== Content formula: nd + 2*content(mu) == Gamma_n(mu) ===")
def partitions(d, maxpart=None):
    if maxpart is None: maxpart = d
    if d == 0: yield []; return
    for first in range(min(d, maxpart), 0, -1):
        for rest in partitions(d-first, first): yield [first]+rest
bad = 0; tot = 0
for d in range(0, 11):
    for mu in partitions(d):
        for n in range(len(mu), len(mu)+4):
            if n == 0: continue
            content = sum((c - r) for r, row in enumerate(mu) for c in range(row))
            tot += 1
            if n*d + 2*content != Gamma(mu + [0]*(n-len(mu)), n): bad += 1
print(f"partition/rank pairs checked: {tot}, mismatches: {bad}")

print("\n=== Proposition 11: transfer squares in the exterior realization ===")
def wedge_ops(n, h):
    """creation operators a_i^dagger : Lambda^h -> Lambda^{h+1} in the orthonormal bases of sorted subsets"""
    src = list(itertools.combinations(range(n), h)); dst = list(itertools.combinations(range(n), h+1))
    di = {s:k for k,s in enumerate(dst)}
    ops = []
    for i in range(n):
        M = np.zeros((len(dst), len(src)))
        for k, s in enumerate(src):
            if i in s: continue
            pos = sum(1 for x in s if x < i)     # e_i ^ e_s : move e_i past pos vectors
            t = tuple(sorted(s + (i,)))
            M[di[t], k] = (-1)**pos
        ops.append(M)
    return ops
def norm_alt(n, h):
    """isometry Lambda^h -> (C^n)^{tensor h}: unit wedge -> signed sum of h! orderings / sqrt(h!)"""
    src = list(itertools.combinations(range(n), h))
    J = np.zeros((n**h, len(src)))
    for k, s in enumerate(src):
        for perm in itertools.permutations(range(h)):
            x = [s[perm[a]] for a in range(h)]
            idx = 0
            for val in x: idx = idx*n + val
            J[idx, k] += perm_sign(perm)/math.sqrt(math.factorial(h))
    return J
p11ok = True
for n in range(1, 5):
    for h in range(0, n+1):
        for hp in range(0, n+1):
            if n**(h+hp) > 5000: continue
            J = np.kron(norm_alt(n, h), norm_alt(n, hp))
            assert np.allclose(J.T @ J, np.eye(J.shape[1]))                       # normalized alternation is isometric
            # X_{cc'} on the tensor space
            def X(f):
                out = np.zeros_like(f)
                for p in range(h):
                    for q in range(h, h+hp): out = out + swap(f, p, q)
                return out
            Xm = np.array([X(J[:,k].reshape((n,)*(h+hp)) if h+hp>0 else J[:,k]).reshape(-1) for k in range(J.shape[1])]).T
            Xw = J.T @ Xm
            dw = math.comb(n,h); dwp = math.comb(n,hp)
            # T = sum_i A_i (x) A_i^dagger : Lambda^h (x) Lambda^hp -> Lambda^{h-1} (x) Lambda^{hp+1}
            if h >= 1 and hp+1 <= n:
                cr_lo = wedge_ops(n, h-1); cr_hi = wedge_ops(n, hp)
                T = sum(np.kron(cr_lo[i].T, cr_hi[i]) for i in range(n))
                TT = T.T @ T
            else:
                TT = np.zeros((dw*dwp, dw*dwp))        # T = 0: nothing to remove, or the target wedge is full
            if hp >= 1 and h+1 <= n:
                cr_lo = wedge_ops(n, hp-1); cr_hi = wedge_ops(n, h)
                Tp = sum(np.kron(cr_hi[i], cr_lo[i].T) for i in range(n))
                TpTp = Tp.T @ Tp
            else:
                TpTp = np.zeros((dw*dwp, dw*dwp))
            e1 = np.max(np.abs(TT - (h*np.eye(dw*dwp) - Xw))) if dw*dwp else 0.0
            e2 = np.max(np.abs(TpTp - (hp*np.eye(dw*dwp) - Xw))) if dw*dwp else 0.0
            # control: wrong height in the first identity
            e_ctl = np.max(np.abs(TT - (hp*np.eye(dw*dwp) - Xw))) if dw*dwp else 0.0
            # ||Tf||^2 = (1/(hp+1)) sum_{p in S_c} ||f - Y_p f||^2 on wedge basis vectors
            e3 = 0.0
            for k in range(J.shape[1]):
                f = J[:,k].reshape((n,)*(h+hp)) if h+hp>0 else J[:,k]
                s = sum(np.sum((f - Yp(f, p, list(range(h, h+hp))))**2) for p in range(h))/(hp+1)
                e3 = max(e3, abs(TT[k,k] - s))
            ok = e1 < 1e-10 and e2 < 1e-10 and e3 < 1e-10
            p11ok &= ok
            if not ok or (n,h,hp) in [(3,2,1),(3,1,2),(4,2,2),(2,2,2),(2,1,0),(3,3,1)]:
                print(f"n={n} h_c={h} h_c'={hp}: |T^dag T-(h_c-X)|={e1:.1e}, |T'^dag T'-(h_c'-X)|={e2:.1e}, |diag(T^dag T)-deficit/(h_c'+1)|={e3:.1e}, control |T^dag T-(h_c'-X)|={e_ctl:.2f}")
print("Prop 11 all (n<=4) OK:", p11ok)
# A_i^dagger A_j = action of E_ij on the wedge (sum of slot matrix units under normalized alternation)
n, h = 4, 2
cr = wedge_ops(n, h-1); Jh = norm_alt(n, h); worst = 0.0
for i in range(n):
    for j in range(n):
        W = cr[i] @ cr[j].T
        M = np.array([sum(Eunit(Jh[:,k].reshape((n,)*h), p, i, j, n) for p in range(h)).reshape(-1) for k in range(Jh.shape[1])]).T
        worst = max(worst, np.max(np.abs(Jh.T @ M - W)), np.max(np.abs(M - Jh @ W)))
print(f"A_i^dag A_j vs sum_p E^(p)_ij under normalized alternation (n=4,h=2): max error {worst:.1e}")

print("\n=== Projector formula Af=(f-Yf)/(s+1), spectrum of Y, remark (4) ===")
worst = 0.0; worstY2 = 0.0; spec_ok = True
for n in range(1, 5):
    for s in range(0, 4):
        if n**(s+1) > 5000: continue
        Bset = list(range(s)); p = s
        f = rng.standard_normal((n,)*(s+1)) + 1j*rng.standard_normal((n,)*(s+1))
        f = antisym(f, Bset)
        Af = antisym(f, Bset+[p]); Yf = Yp(f, p, Bset)
        worst = max(worst, np.max(np.abs(Af - (f - Yf)/(s+1))))
        worstY2 = max(worstY2, np.max(np.abs(Yp(Yf, p, Bset) - (s*f - (s-1)*Yf))))
        lhs = np.vdot(f,f).real - np.vdot(f,Yf).real; rhs = np.vdot(f-Yf, f-Yf).real/(s+1)
        worst = max(worst, abs(lhs-rhs))
print(f"max error of Af=(f-Yf)/(s+1) and of ||f||^2-Re<f,Yf>=||f-Yf||^2/(s+1): {worst:.1e};  of Y^2 f = s f-(s-1)Yf: {worstY2:.1e}")
# remark (4): p in B
n, s = 3, 2
f = antisym(rng.standard_normal((n,)*3), [0,1])
Yf = f + swap(f, 0, 1)          # p = slot 0 in B={0,1}: self-swap is Id, other swap negates
print("remark (4), s=2, p in B: Yf = (2-s)f = 0:", np.allclose(Yf, 0), "; so Y^2 f = 0 while s f-(s-1)Yf = 2f != 0")

print("\n=== Section 4 claims ===")
for n, d in [(2,2),(2,3),(3,2),(3,3)]:
    D = n**d
    Kmat = np.array([K_swaps(np.eye(D)[:,k].reshape((n,)*d), list(range(d)), n).reshape(-1) for k in range(D)]).T
    print(f"n={n}, d={d}: largest eigenvalue of K on the whole space = {np.linalg.eigvalsh(Kmat).max():.6f}, nd+d(d-1) = {n*d+d*(d-1)}")
# two full columns at n=2
cfg = Cfg(2, [(2,2),(2,2)]); print("two full columns at n=2: coefficient =", cfg.coef_labels(), "(paper: 8)")
cfg = Cfg(2, [(1,1),(1,1)]); print("two one-box columns at n=2: coefficient =", cfg.coef_labels(), "(paper: 6)")
# partly selected column counterexample
cfg = Cfg(2, [(2,2)], sel_override=[0])   # select only the box of label 0
f = np.zeros((2,2)); f[0,1] = 1; f[1,0] = -1
print("partly selected column: m =", cfg.m, " coefficient =", cfg.coef_labels(), " Re<f,Kf>/||f||^2 =", np.vdot(f, K_def(f, cfg.S, 2)).real/np.vdot(f,f).real)

print("\n=== Terminal-subcolumn variant (Section 4.3) and a non-terminal control ===")
worst_slack = 1e9; ncase = 0; worst_id = 0.0
for n in range(1, 5):
    for k in range(1, 4):
        for Hs in itertools.combinations_with_replacement(range(1, n+1), k):
            if n**sum(Hs) > 20000: continue
            for ts in itertools.product(*[range(0, H+1) for H in Hs]):
                cfg = Cfg(n, list(zip(Hs, ts)))
                f = cfg.random_alt(); N = np.vdot(f,f).real
                if N < 1e-12: continue
                q = np.vdot(f, K_swaps(f, cfg.S, n)).real
                ncase += 1
                worst_slack = min(worst_slack, (cfg.coef_labels()*N - q)/N)
                assert cfg.coef_labels() == cfg.coef_heights()
                worst_id = max(worst_id, abs(cfg.coef_labels()*N - q - rhs_B(cfg, f))/N)
print(f"terminal subcolumns: {ncase} cases, min slack/N = {worst_slack:.3e} (>= -1e-9 means the bound held), max error of the sum-of-squares identity = {worst_id:.1e}")
viol = 0; tot = 0
for n in range(2, 4):
    for H in range(2, n+1):
        for sel in itertools.chain.from_iterable(itertools.combinations(range(H), r) for r in range(1, H)):
            labs = [n-H+r for r in sel]
            if set(labs) == set(range(min(labs), n)): continue     # terminal: skip
            cfg = Cfg(n, [(H,H)], sel_override=list(sel))
            f = cfg.random_alt(); N = np.vdot(f,f).real
            q = np.vdot(f, K_swaps(f, cfg.S, n)).real
            tot += 1
            if cfg.coef_labels()*N - q < -1e-9*N: viol += 1
print(f"control, non-terminal selections in one column: {viol} of {tot} violate the bound (must be > 0)")
```

### Appendix E. `check_props_abstract.py` (needs `check_core.py`)

```python
# Random search for counterexamples to the displayed statements of Propositions 4-9 (abstract kernel R, real N),
# transcribed from v2 (identical to v1). Controls: asymmetric R, and partial (non-whole-column) selection.
import itertools, random, sys
sys.path.insert(0, '/tmp/casbound-v2-verifier')
from check_core import Cfg
random.seed(5)

def feasible_kernel(cfg, Ccols, N, symmetric=True, same_col=True, climb=True):
    Q = cfg.Q; S = cfg.S
    R = [[random.randint(-3, 3) for _ in range(Q)] for _ in range(Q)]
    if symmetric:
        for p in range(Q):
            for q in range(p): R[p][q] = R[q][p]
    if same_col:
        for p in range(Q):
            for q in range(Q):
                if p != q and cfg.col_of[p] == cfg.col_of[q]: R[p][q] = -N
    def viol():
        out = []
        for p in S:
            for c in Ccols:
                if c != cfg.col_of[p]:
                    if sum(R[p][q] for q in cfg.Sc.get(c, [])) > N: out.append((p, c))
        return out
    for _ in range(10000):
        v = viol()
        if not v: break
        p, c = random.choice(v)
        tgt = cfg.Sc.get(c, [])
        if not tgt: return None          # 0 <= N fails: hypotheses unsatisfiable
        q = random.choice(tgt)
        R[p][q] -= 1
        if symmetric: R[q][p] -= 1
    else:
        return None
    if climb:                              # push cross-column entries up while the hypotheses still hold
        pairs = [(p, q) for p in S for q in S if cfg.col_of[p] != cfg.col_of[q]]
        for _ in range(400):
            if not pairs: break
            p, q = random.choice(pairs)
            R[p][q] += 1
            if symmetric: R[q][p] += 1
            if viol():
                R[p][q] -= 1
                if symmetric: R[q][p] -= 1
    return R

def run(symmetric=True, trials=4000, partial=False):
    stats = dict(tested=0, p4=0, p5=0, p6=0, p7=0, p8=0, p9=0, tight9=0, negN=0)
    for _ in range(trials):
        n = random.randint(1, 4)
        k = random.randint(1, 4)
        cols = []
        for _c in range(k):
            H = random.randint(1, n)
            if partial: t = random.randint(0, H)
            else: t = random.choice([H, H, H, 0])
            cols.append((H, t))
        if partial:
            # arbitrary subset of each column
            cfg0 = Cfg(n, [(H, H) for H, _ in cols])
            sel = [p for p in range(cfg0.Q) if random.random() < 0.6]
            cfg = Cfg(n, [(H, H) for H, _ in cols], sel_override=sel)
        else:
            cfg = Cfg(n, cols)
        if not cfg.S: continue
        Ccols = list(range(k)) + ([k] if random.random() < 0.3 else [])     # C may contain a column with no boxes
        N = random.choice([-2, -1, 0, 1, 2, 3])
        R = feasible_kernel(cfg, Ccols, N, symmetric=symmetric)
        if R is None: continue
        stats['tested'] += 1; stats['negN'] += (N < 0)
        S = cfg.S; col = cfg.col_of; b = cfg.label; m = cfg.m
        # Prop 4, Prop 5
        for p in S:
            if sum(1 for q in S if col[q] == col[p] and b[q] > b[p]) != n - 1 - b[p]: stats['p4'] += 1; break
        for p in S:
            if m[b[p]] != 1 + sum(1 for q in S if col[q] != col[p] and b[q] == b[p]): stats['p5'] += 1; break
        # Prop 6 with F = R
        lhs6 = sum(R[p][q] for p in S for q in S if col[q] != col[p])
        rhs6 = sum(R[p][q] for c in cfg.active for cp in cfg.active if cp != c for p in cfg.Sc[c] for q in cfg.Sc[cp])
        if lhs6 != rhs6: stats['p6'] += 1
        # Prop 7 for all c != c' in C
        bad7 = False
        for c in Ccols:
            for cp in Ccols:
                if c == cp: continue
                l = sum(R[p][q] for p in cfg.Sc.get(c, []) for q in cfg.Sc.get(cp, []))
                r = sum(N for p in cfg.Sc.get(c, []) for q in cfg.Sc.get(cp, []) if b[p] == b[q])
                if l > r: bad7 = True
        stats['p7'] += bad7
        # Prop 8
        r8 = sum(N for p in S for q in S if col[q] != col[p] and b[q] == b[p])
        if lhs6 > r8: stats['p8'] += 1
        # Prop 9
        l9 = n*len(S)*N + sum(R[p][q] for p in S for q in S if q != p)
        r9 = sum(m[i]*(m[i] + 2*i + 1 - n) for i in range(n)) * N
        if l9 > r9: stats['p9'] += 1
        if l9 == r9: stats['tight9'] += 1
    return stats

print("statements as displayed (symmetric R, whole columns):", run())
print("control, R not symmetric:                             ", run(symmetric=False))
print("control, arbitrary partial selection (U dropped):     ", run(partial=True))
```

### Appendix F. `check_concordance.py`

```python
import re, os, sys
tree = 'local-source/_Scratch/mathematics-lean-exposition/targets/alpoge/lean/src'
CB = tree + '/Development/WeilBound/RepresentationTheoryGL/CasimirAlgebra/KugaCoordinates/CasimirBounds/'
TR = tree + '/Development/WeilBound/RepresentationTheoryGL/CasimirAlgebra/TensorRelationsGL/'
KC = tree + '/Development/WeilBound/RepresentationTheoryGL/CasimirAlgebra/KugaCoordinates/'
P = {
 'CasBoundHolds': CB+'CasBoundHolds.lean', 'Expand': CB+'Expand.lean', 'ReSwapSumLe': CB+'ReSwapSumLe.lean',
 'CountSame': CB+'CountSame.lean', 'CountCross': CB+'CountCross.lean', 'KTypeData': TR+'KTypeData.lean', 'StepFormula': TR+'StepFormula.lean',
 'SumFinVal': KC+'CoefficientGluing/SumFinVal.lean', 'CoefGlueHolds': KC+'CoefficientGluing/CoefGlueHolds.lean',
 'ClozelCohomologicalOf': TR+'ClozelCohomologicalOf.lean', 'PKTypeA': TR+'PKTypeA.lean', 'PKType': TR+'PKType.lean',
 'KTypeHolds': TR+'KTypeHolds.lean', 'KgCasDiff': KC+'KugaGluing/KgCasDiff.lean', 'KugaAbsHolds': KC+'KugaAbsoluteValues/KugaAbsHolds.lean',
 'CochainHolds': KC+'CochainExpansions/CochainHolds.lean', 'Summand': KC+'MatrixConjugateSums/Summand.lean',
 'ClozelCohomological': KC+'ClozelCohomological.lean', 'IsStarRep': KC+'IsStarRep.lean',
}
L = {k: open(v, encoding='utf-8').read().split('\n') for k, v in P.items()}
def check(f, a, b, decl, whole=True):
    """line a must start the declaration 'decl'; if whole, line b must be its last line (next line blank or a new declaration/end)"""
    first = L[f][a-1]
    ok_start = re.search(r'\b(theorem|def|abbrev|structure)\s+' + re.escape(decl) + r"(?![\w'])", first) is not None
    ok_end = True
    if whole:
        last = L[f][b-1]; nxt = L[f][b] if b < len(L[f]) else ''
        inner_blank = any(L[f][i].strip() == '' for i in range(a-1, b))
        ok_end = last.strip() != '' and nxt.strip() == '' and not inner_blank
    return ok_start and ok_end
rows = [
 # Table 1
 ('CasBoundHolds', 9, 32, 'casBound_holds'), ('StepFormula', 88, 94, 'CasBound'), ('Expand', 32, 55, 'pair_apply'), ('Expand', 66, 92, "cas_expand'"),
 ('ReSwapSumLe', 29, 83, "re_swapSum_le'"), ('CountSame', 22, 44, 'count_up'), ('CountSame', 46, 69, 'count_eqb'),
 ('CountCross', 59, 83, 'sum_sum_ite_col_ne_eq_sum_by_col'), ('CountCross', 28, 57, 'sum_filter_col_le_sum_ite_of_bound'),
 ('CountCross', 85, 102, 'count_cross'), ('CountCross', 104, 153, 'cas_count'),
 # Table 2
 ('KTypeData', 51, 52, 'IsTab'), ('Expand', 12, 15, 'eAt_applyC'), ('Expand', 17, 20, 'tE_zero_apply'), ('Expand', 22, 30, 'sum4'),
 ('ReSwapSumLe', 15, 16, 'pm_pm'), ('ReSwapSumLe', 18, 27, 'dot_pm_swap'), ('CountSame', 11, 20, 'count_rhs'), ('CountSame', 71, 88, 'count_same'),
 ('CountCross', 13, 26, 'isWH_coeff_one_polynomial'),
 # Table 3 (those that name a declaration)
 ('KTypeData', 60, 60, 'fib'), ('KTypeHolds', 27, 49, 'kType_holds'), ('SumFinVal', 111, 130, 'arith'), ('KgCasDiff', 37, 52, 'kg_casDiff'),
 ('KugaAbsHolds', 137, 181, 'kugaAbs_holds'), ('ClozelCohomologicalOf', 55, 63, 'clozelCohomological_of'), ('ClozelCohomological', 8, 9, 'clozelCohomological'),
 ('PKTypeA', 13, 13, 'Bx'), ('PKTypeA', 38, 38, 'colQ'), ('PKTypeA', 15, 15, 'Pr'), ('PKTypeA', 259, 264, 'half'), ('CochainHolds', 49, 105, 'om_ne'),
 ('Summand', 44, 56, 'exists_min'), ('Summand', 79, 80, 'Jm'), ('IsStarRep', 102, 102, 'CoefGlue'), ('IsStarRep', 67, 70, 'Harmonic'),
 ('IsStarRep', 88, 93, 'Cochain'), ('IsStarRep', 75, 80, 'BigCx'), ('IsStarRep', 95, 98, 'CasVal'), ('ClozelCohomologicalOf', 37, 43, 'IsSmall'),
]
bad = 0
for f, a, b, d in rows:
    ok = check(f, a, b, d)
    ctl = check(f, a+1, b+1, d)      # negative control: the same range shifted by one line must be rejected
    if not ok or ctl: bad += 1
    print(f"{'OK ' if ok else 'BAD'} {f}.lean:{a}-{b} {d}   (shifted-by-one control rejected: {not ctl})")
print('rows:', len(rows), 'failures:', bad)
# statement-only ranges cited in Table 3
for f, a, b, d in [('SumFinVal', 33, 37, 'cas_shift'), ('PKTypeA', 207, 220, 'sort_data'), ('PKTypeA', 135, 182, 'cnt1'), ('PKType', 26, 47, None), ('ClozelCohomologicalOf', 39, 43, None)]:
    print(f"--- {f}.lean:{a}: {L[f][a-1].strip()[:110]}")
    print(f"    {f}.lean:{b}: {L[f][b-1].strip()[:110]}")
# sub-ranges quoted for Theorem A in Table 1
print("\nSub-ranges quoted for Theorem A (paper: expansion 11-19, symmetry 22-23, same-column value 24-25, one-box bound 26-32):")
for i in range(19, 27):
    print(f"  CasBoundHolds.lean:{i}: {L['CasBoundHolds'][i-1]}")
```
