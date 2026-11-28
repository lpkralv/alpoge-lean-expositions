# Adversarial review of the casBound exposition paper (verifier, Fable)

Reviewed 2026-11-27. Manuscript: `local-source/_Scratch/mathematics-codex/vance-casbound-review/in/paper.pdf` and `paper.tex` (18 pages). Lean tree: `local-source/_Scratch/mathematics-lean-exposition/targets/alpoge/lean/src`.

## Verdict

**PROOF CORRECT.** I tried to break the theorem, each of the nine propositions, every hand computation and the unlabelled side arguments, and none broke. The paper's statements match the Lean declarations it names, all ten concordance line ranges and all 26 Lean line ranges cited in section 2.1 are right, and the 975-line closure re-elaborates from the reviewed sources with only the three standard axioms.

No finding is MATH-FATAL or MATH-GAP. The defects are in what surrounds the mathematics: one unsupported citation (finding 9), one validation statistic that the published record does not reproduce (finding 10), and expository faults, one of them systematic and mechanical (finding 11).

In the verifier's own terms: SURVIVED for the mathematics, FLAG for findings 9 and 10.

## How to read the references

- `pN lM` is line M of page N in the output of `pdftotext -layout paper.pdf`. `tex L` is a line of `paper.tex`.
- Lean references are `File.lean:lines` in the tree above. The five proof files are in `Development/WeilBound/RepresentationTheoryGL/CasimirAlgebra/KugaCoordinates/CasimirBounds/`.
- Scratch is in `/tmp/casbound-verifier-fable/`. Nothing in the repository or the Lean tree was changed. Because `/tmp` can be cleared, Appendix A gives a self-contained script and Appendix B the Lean check file.

## What I ran

| Evidence | Command | Result |
|---|---|---|
| Closure size and text scan | `python3 /tmp/casbound-verifier-fable/closure.py <src> Development.WeilBound.RepresentationTheoryGL.CasimirAlgebra.KugaCoordinates.CasimirBounds.CasBoundHolds` | 10 modules, 975 lines (`wc -l`), only external import is Mathlib, no line contains any of the words sorry, admit, axiom, native_decide, unsafe, implemented_by, opaque |
| Independent Lean re-elaboration | `/tmp/casbound-verifier-fable/leanbuild/build.sh` (Lean 4.33.1; the ten closure files copied from the reviewed tree and compiled in dependency order; Mathlib oleans, rev 0df444a3, read from the prebuilt workspace `tool-win/targets/alpoge-casbound/.lake/packages`) | every module `exit=0 errors=0 sorry_warnings=0`; `casBound_holds` and the seven public lemmas depend on `[propext, Classical.choice, Quot.sound]`; negative control `theorem neg_control : (1 : ℕ) = 2 := by sorry` reports `[sorryAx]` |
| Paper statements as Lean terms | `leanbuild/Check.lean` (Appendix B) | Theorem 10 with the tableau condition unfolded as on p4, Proposition 3 as a sum of real parts, and Proposition 9 all typecheck as instances of `casBound_holds`, `re_swapSum_le'`, `cas_count` |
| Operators, theorem, propositions 1 to 3, hand computations | `python3 /tmp/casbound-verifier-fable/verify_casbound.py` | `SUMMARY: 36 checks, 0 failed` |
| Transfer squares, propositions 4 to 9 for abstract kernels | `python3 /tmp/casbound-verifier-fable/verify_casbound2.py` | `SUMMARY: 12 checks, 0 failed` |
| Product identity, extremal vector, pair deficit | `python3 /tmp/casbound-verifier-fable/verify_casbound3.py` | `SUMMARY: 7 checks, 0 failed` |
| Self-contained re-check | `python3 mini_check.py` (Appendix A) | 140 configurations, 0 violations, supremum equal to the coefficient to 2.5e-14, and three negative controls detected (full output in Appendix A) |

The numerical operators are built from the Lean definitions, not from the paper: `eAt p a b f I = if I p = a then f (update I p b) else 0`, `tE S 0 a b = Σ_{p∈S} eAt p a b`, `pm σ f I = f (I ∘ σ)` (KTypeData.lean:17–27).

Script hashes (first 12 hex digits of SHA-256): verify_casbound.py 834d95ae2cbd, verify_casbound2.py 61a0391c94f3, verify_casbound3.py 2d6841629626, mini_check.py e148f78db523, closure.py 8ab33bddd5d9, build.sh d29500feeb64, Check.lean cd732707c362.

## Findings

### 1. OK. Theorem 10 is the Lean statement

Paper p4 l10–l21 (tex 240–261) against `CasBound`, StepFormula.lean:88–94, with `IsTab` at KTypeData.lean:51–52, proved at CasBoundHolds.lean:9–32.

Symbol by symbol: `n : ℕ`; `Q` finite with decidable equality; `C` with decidable equality; `col = γ`; `b : Q → Fin n`; `S : Finset Q`; the four hypotheses in the paper's order are `IsTab.1`, `IsTab.2`, the whole-column condition (StepFormula.lean:89) and alternation (StepFormula.lean:90); the left side is `(star f ⬝ᵥ (Σ_a Σ_c tE S 0 a c * tE S 0 c a) f).re`, so the inner product is conjugate-linear in the first slot as the notation table says; the right side is `(Σ_i m_i (m_i + 2 i + 1 − n)) * (star f ⬝ᵥ f).re`. The matrix-unit convention "e_{i'} ↦ e_i" (p4 l2) agrees with `eAt`: applied to the indicator of an assignment y it gives the indicator of y[p←a] when y(p)=c.

Mechanical confirmation: Appendix B, item (2), compiles with no error.

Numerical attack: over 384 configurations (n ≤ 4, up to 4 columns, every choice of selected columns) the supremum of Re⟨f,Kf⟩/‖f‖² over column-alternating f never exceeds the coefficient; largest excess 7.8e-14. The same checker rejects three false variants (finding 4).

"Does this settle something open?" No. The statement is a finite-dimensional inequality equivalent to a classical fact: among the constituents of a tensor product of exterior powers, the Cartan component has the largest gl_n Casimir. RH enters nowhere in the paper's mathematics; the bound holds whether or not the rest of the archive is right.

### 2. OK. Propositions 1 to 9 against Lean

| Paper | Lean declaration | Lines | Statement matches | Numerical check | Negative control |
|---|---|---|---|---|---|
| Prop 1 (p7 l27) | `pair_apply` | Expand.lean:32–55 | yes | operator identity, 5 sizes of (n, #Q) | swapped index order is rejected |
| Prop 2 (p7 l46) | `cas_expand'` | Expand.lean:66–92 | yes | all S for (n, #Q) in {(1,3),(2,3),(2,4),(3,3)} | n/a |
| Prop 3 (p8 l28) | `re_swapSum_le'` | ReSwapSumLe.lean:29–83 | yes (Lean has Re of the sum; equal by `Complex.re_sum`, Appendix B item 3) | identity ‖f‖² − ΣRe⟨f,P_{pq}f⟩ = ‖f−Yf‖²/(s+1) on 10 shapes including s=0 and s>n | without alternation the ratio is 2 > 1 |
| Prop 4 (p9 l32) | `count_up` | CountSame.lean:22–44 | yes | 4000 random tableaux | paper's own n=2 example |
| Prop 5 (p10 l9) | `count_eqb` | CountSame.lean:46–69 | yes | 4000 random tableaux | n/a |
| Prop 6 (p10 l20) | `sum_sum_ite_col_ne_eq_sum_by_col` (private) | CountCross.lean:59–83 | yes | random kernels | n/a |
| Prop 7 (p10 l35) | `sum_filter_col_le_sum_ite_of_bound` (private) | CountCross.lean:28–57 | yes | 3063 kernels, 78 with N<0; right side equals min(h_c,h_{c'})·N | violations found when upward closure, whole-column selection or symmetry is dropped |
| Prop 8 (p11 l30) | `count_cross` | CountCross.lean:85–102 | yes | same kernels | n/a |
| Prop 9 (p12 l16) | `cas_count` | CountCross.lean:104–153 | yes (Appendix B item 4) | same kernels with R = −N inside columns | n/a |

The smallest Proposition 7 counterexample when upward closure fails: n=2, two singleton columns with labels 0 and 1, R(p,q)=N=1. The row hypothesis holds and the left side is 1 > 0 (`verify_casbound3.py`, last two lines; the valid twin with labels 1 and 1 gives 1 ≤ 1).

### 3. OK. The prose proofs follow the Lean proofs step for step

- Prop 3 (p9 l10–l26): product identity `swap p q * swap p q' = swap p q' * swap q q'` (ReSwapSumLe.lean:47–50); P_{pq}(Yf) = f − Yf + P_{pq}f (37–55); Y²f = sf − sYf + Yf, which is the paper's sf − (s−1)Yf (56–60); Yg = −sg (62–64); ⟨g,g⟩ = (1+s)⟨f,g⟩ (65–68); conclusion (74–83). Self-adjointness is `dot_pm_swap` (18–27).
- Prop 7 (p11 l11–l24): branch "every label of S_c has a match" is CountCross.lean:35–39; the missing-label branch with the trichotomy on b(q) against i_* is 40–49, the interchange of sums and use of symmetry 50–57. The paper's three cases (equal, smaller, larger label) are the Lean's `lt_trichotomy` cases in a different order.
- Prop 9 (p12 l41–p13 l5): split into same-column and cross-column parts (CountCross.lean:112–124); "charge both orders to the lower label" is `count_same` (CountSame.lean:71–88, used at CountCross.lean:126); Proposition 4 at 127–131; Proposition 5 at 132–137; Proposition 8 at 138; per-box sum at 146–153 with `count_rhs` (CountSame.lean:11–20) for "summing by label".
- Theorem 10 (p13 l31–l47): expansion (CasBoundHolds.lean:11–19), symmetry (22–23), same-column value −N (24–25), row bound from Proposition 3 with B = S_c and c ≠ γ(p) (26–32).

### 4. OK. Negative controls for the theorem checker

The checker that passes the theorem rejects each false variant:

- Partial-column selection (the paper's example, p9 l44–l49): n=2, column with labels 0 and 1, S = the label-0 box. Left 2, right 0.
- Upward closure violated: n=2, one box labelled 0. Left 2, right 0.
- Alternation dropped: n=2, one full column, any f. Left 6, right 2.

Reproduce with Appendix A (three `NEG` lines).

### 5. OK. Hand computations recomputed

All agree with the paper.

1. p7 l53–p8 l4: n=1, singleton, background z: square (1+z)², value 1 at z=0 and 4 at z=1.
2. p8 l7–l8: adding P_{pp} adds d·Id; replacing the scalar term by ΣP_{pp} loses (n−1)d·Id.
3. p8 l13–l17: largest eigenvalue of the ordered transposition sum is d(d−1) (checked for n ≤ 3, d ≤ 4); nd+d(d−1) and nd−d(d−1); excess 2d(d−1); 6 against 2 at n=d=2.
4. p8 l21–l22: 2·(content sum) + nd = Γ_n(μ), all partitions with d ≤ 7, n ≤ 5.
5. p8 l37–l42: s‖f‖² from Cauchy–Schwarz, loss (s−1)‖f‖²; 2h_ch_{c'} against 2min(h_c,h_{c'}); 2h_c² against 2h_c.
6. p8 l56–l61: on tensors fully alternating on B∪{p}, Yf = −sf and g = (s+1)f.
7. p9 l13 (display): Y²f = sf − (s−1)Yf. p9 l14–l17: for p ∈ B, Yf = (2−s)f, and at s=2 the identity would give 2f where the truth is 0.
8. p9 l18–l24: Yg = −sg; ‖g‖² = (s+1)Re⟨f,g⟩; the final identity.
9. p9 l35–l38: counts n−1 at label 0 and 0 at label n−1.
10. p9 l44–p10 l4: singleton Casimir 2·Id; m_0=1, m_1=0 gives coefficient 0; height expression 1·(2+1−1) = 2.
11. p11 l3: heights 3 and 1 give 2N against 4N.
12. p11 l42–l48: f = (|010⟩ − |100⟩)/√2 alternates in p_1,p_2, has norm 1, ⟨f,P_{13}f⟩ = 1/2, ⟨f,P_{23}f⟩ = 1/2, total 1 = N; here Yf = f, the equality case of Proposition 3.
13. p12 l6–l13: rows charged to label i total 2·C(m_i,2)·N, and Σ_i m_i(m_i−1) = Σ_p (m_{b(p)}−1).
14. p12 l34–l40 and l52–l56: single column gives nh − h(h−1); at h=n this is n.
15. p12 l57–p13 l4: n − 2(n−1−b) + (m−1) = m + 2b + 1 − n.
16. p13 l11–l13: n=2, two singleton columns, K = 4·Id + 2P, eigenvalues 6 and 2; the coefficient is 6.
17. p13 l37–l41: two full columns at n=2: diagonal 8N, internal −4N, individual estimates +8N (total 12N), grouped +4N (total 8N); the multiplicity formula gives 8.
18. p13 l48–l54: Σ h_c(n+1−h_c) + 2Σ min(h_c,h_{c'}) equals the multiplicity coefficient in all 384 configurations.
19. p4 l30–l37: with λ_j = m_{n−j}, λ is a partition and Γ_n(λ) equals the coefficient; Σ_a G_{aa} = d·Id, so the sl_n operator is K − d²/n.
20. p2 l41 and l52, p3 l27–l36: twist contributes −2s|S| + ns² (matches `cas_shift`, SumFinVal.lean:33–37); ν_τ(i) = s − l_τ(w_τ(i)) − i is nonnegative and nondecreasing; the corrected sum equals Σ_k((l_k+(n−1)/2)² − ((n−1)/2−k)²) (matches `arith`, SumFinVal.lean:111–114).

### 6. OK. Mathematics that is not in the Lean

All of it holds.

- Highest-weight proof (p13 l14–l29). Partial sums of any constituent weight are at most Σ_c min(k,h_c) = Σ_{j≤k} λ_j; the telescoping identity Γ_n(λ) − Γ_n(μ) = Σ_{k<n} D_k(v_k − v_{k+1}) and v_k − v_{k+1} ≥ 2 hold for all pairs of partitions with d ≤ 7, n ≤ 5. In all 384 configurations every eigenvalue of K on the alternating space is Γ_n(μ) for some μ dominated by λ. The argument needs K self-adjoint and commuting with the column antisymmetrizers; both hold because G_{ii'}† = G_{i'i} and S is a union of columns.
- Transfer squares (p8 l47–l55). T†T = h_c·Id − Σ_{i,j} A_i†A_j ⊗ A_j†A_i and the reversed identity with h_{c'}, checked in the fermionic realisation for 70 triples (n, h_c, h_{c'}) with n ≤ 5, including the degenerate case h_{c'} = n. The normalised alternation map is an isometry and carries Σ_{i,j} to the sum of swaps Σ_{p∈S_c,q∈S_{c'}} P_{pq}; its largest eigenvalue is min(h_c,h_{c'}).
- Pair deficit (p3 l17–l19). h_c‖f‖² − Re⟨f,X_{cc'}f⟩ = (1/(k+1))Σ_{p∈S_c}‖f − Y_pf‖², checked on 7 shapes.
- Antisymmetrizer remark (p9 l28–l31). Antisym_{B∪{p}} f = (f − Yf)/(s+1) for f alternating on B.
- Sharpness (p13 l54–l56). The basis tensor at the assignment x = b, antisymmetrised in each column, is nonzero and is an eigenvector of K with eigenvalue equal to the coefficient, in all 328 cases tried.
- Terminal-subcolumn variant (p10 l6–l8). The bound still holds in the 74 two-column cases tried. It is not always attained there, which the paper does not claim.

### 7. OK. Closure and provenance claims on p1 and p15

- "975 lines excluding Mathlib ... no sorry, admit or axiom" (p1 l39–l40): confirmed, 10 modules.
- "Its only caller, ClozelCohomologicalOfThree.lean" (p1 l35): the only use of `casBound_holds` outside its own file is ClozelCohomologicalOfThree.lean:11.
- "Lean 4.33.1" (p15 l30): `lean-toolchain` reads `leanprover/lean4:v4.33.1`.
- `typePrimesN` closure "1,194 lines" (p16 l8): confirmed, 11 modules, namespace `UpperTheory.T3`.
- Coverage survey "38 ... 25 ... 11 ... no coverage of the Casimir bound or of one bookkeeping result" (p1 l41–l44): `coverage-map/coverage.json` (dated 2026-11-24) has 38 theorems; best status per theorem is 25 explains, 11 outlines, 2 absent (`casBound_holds` and `exists_deep`).
- Reference [1]: the SHA-256 of `https://alpo.ge/lean.tar.gz.part01` fetched today is 86974b1c…a3de77 (18,000,000 bytes), as printed.

### 8. OK. The application narrative (sections 2.1 and 2.2) against Lean

Section 2.1 gives 23 Lean citations covering 26 line ranges. All point at what the text says: StepFormula.lean:88–90 and 91–94; KTypeData.lean:51–52, 60, 104–111; KTypeHolds.lean:27; IsStarRep.lean:67–70, 75–80, 88–93, 95–98, 102; SumFinVal.lean:33–37, 111–114; CoefGlueHolds.lean:120–150 (the call is at line 144: slots `Fin q`, columns ℕ, S = `fib lab τ`, f = `J *ᵥ v`); ClozelCohomologicalOf.lean:37–49, 39–43, 55–63; ClozelCohomologicalOfThree.lean:11; ClozelCohomologicalOfRest.lean:19–21; ClozelCohomological.lean:8–9; ClozelCohomologicalModel.lean:10–12; KgCasDiff.lean:37–52; KugaGlueHolds.lean:15–21, 80–100; KugaAbsHolds.lean:137–181.

Section 2.2 has no line citations. Its claims check against PKTypeA.lean: s = Σ_{τ,k}|l_τ(k)| (line 210); sorting in decreasing order (220); ν monotone (207–209); slots (τ,i,c) with c < ν_τ(i) (13); column code `Nat.pair` (38); pairs c < i over one embedding from each conjugate pair (15, 259–264); i extra occurrences of label i at each embedding (`cnt1`, `cnt2`, `cntF`, 135–182); eigenvalue (u+s)^n (PKType.lean:26–47). "Stable subspace of least dimension ... orthonormal basis" is `exists_min` and `Jm` in MatrixConjugateSums/Summand.lean:44–56, 79–80. The Hermitian-matrix tests are `om_ne` in CochainExpansions/CochainHolds.lean:49–105.

### 9. CITATION. The certification sentence rests on sources that do not say it

p1 l36–l40 (tex 85–91): "Alpöge published the Lean archive ... on 20 November 2026. The Lean community certified the archive's statement and proof on 21 November 2026. ... [1, 2]". The title states "Alpöge's Lean proof of the Riemann hypothesis" as fact.

Evidence, fetched 2026-11-27:

- `curl -sL https://alpo.ge/remark.pdf | pdftotext - - | grep -ciE "certif|communit|comparator|november|2026"` prints 0. Reference [2] has no date and no statement about certification. Its own wording is "I believe I have, working with Claude, discovered a proof" (line 6 of the extracted text).
- `curl -sL https://alpo.ge/ | grep -ciE "sha256|lean\.tar|riemann"` prints 0. Reference [1] says "Archive links and SHA256SUMS at https://alpo.ge" (p16 l34), but the home page links neither, and `https://alpo.ge/SHA256SUMS` returns the home page (the site answers 200 with the home page for unknown paths). The part files themselves exist and the printed hash is right (finding 7).

I do not claim the certification sentence is false. I claim the paper gives a reader no way to check it. This project's own store entry `_SME_store/mathematics/alpoge-riemann-hypothesis-proof/` refers to a Lean and Mathlib joint statement of 2026-11-21 and to Sutherland's table of checks; that is the kind of source the sentence needs. The mathematics of the paper does not depend on it.

Needed to close: a citation for the certification and the release date, and a corrected description of where the checksums are published.

### 10. FLAG. The validation headline is not reproducible from the published record

Abstract p1 l26–l28 and section 4, p16 l14–l19 (tex 1112–1119): two graders "found seven insights captured, one missed and zero wrong before review, and eight captured, zero missed and zero wrong after revision".

What the release package holds (`docs/publications/casbound-release/validation-typeprimes/`):

- `grade-astra.md:1`: "The exposition captures **all eight keyed insights**. The digest captures **seven of eight**." `grade-astra.md:16`: "Counts: 8 captured, 0 buried, 0 missed, 0 wrong." `grade-astra.md:35`: digest recall 7/8, "No item earns key 8".
- `grade-sol.md:16`: "Counts: 8 captured, 0 buried, 0 missed, 0 wrong". `grade-sol.md:35`: digest recall 7/8, "The digest omits key 8 altogether."
- `grep -rnE "before review|7 captured|one missed|1 missed" docs/publications/casbound-release --include='*.md'` finds no grade of a before-review version.

So the two published grade files grade one version of the exposition (`assembled-v10.md`) at 8 of 8, and their only "seven of eight" is the score of a different artifact, the digest, which misses the same insight (key 8) that the paper names as missing before review. Either the before-review grades exist and were not published, or the before-and-after comparison was read off the digest-and-exposition comparison. I could not tell which.

A second point, from the internal log `_Scratch/mathematics-lean-exposition/pipeline-work/alpoge-typeprimes-pipeline-log.md` (not part of the published record): the two graders ran five times on 2026-11-24, at 17:07, 18:12, 18:39 and 19:10 UTC before the review step (19:13) and once after the revision (19:20). The steps scope, supply and audit were re-run between those rounds (log lines 25–26, 38–40, 52–54), and each round overwrote the same `report.md`. The paper reports one before figure and one after figure. I did not establish what the first three rounds scored or why the steps were re-run.

Needed to close: the before-review reports from both graders, the number of grading rounds run against the key, and what changed between them. With n = 1 theorem and AI graders, which the paper states, the result is an anecdote either way; the point is that the stated design should be the design that was run.

### 11. EXPOSITION, systematic. Trailing citation lists were fused into the last sentence of the paragraph

In `exposition.md` every paragraph ends its prose with a full stop and then lists its sources. In `paper.tex` the full stop before the list is gone, so the last sentence now carries the citations. This happens 21 times. In at least eight places the last sentence is about Alpöge's proof or the Lean proof, so the paper now attributes those statements to unrelated literature.

Worst case, p13 l29–l30 (tex 943–945): "Alpöge's coordinate proof follows [18, Proposition 2.1], [12, lectures 18 and 25–26], [13, Example 5.4], [14, §2], [20, Proposition 3.2]." The source text (`exposition.md:361`) reads "Alpöge's coordinate proof follows." as a transition, then lists references for the highest-weight argument. As printed, the paper says the Lean proof follows Gleizer–Postnikov, Etingof, Yang, Perelomov–Popov and Baur. It does not; none of them is used.

Others of the same kind: p3 l19–l24 (tex 194–196, "The Lean proof uses this normalization ... [15], [16], [17]"); p4 l51–l53 (tex 299–301, "Column alternation alone gives these signs in Alpöge's proof [15, Proposition 2.2] and [26, ...]"); p5 l8–l10 (tex 312–315); p5 l12–l15 (tex 319–321); p8 l44–l46 (tex 548–550); p11 l4–l6 (tex 757–759); p14 l2–l4 (tex 978–981, "n = 0 forces Q = S = ∅ [13, Example 5.4], [18, Proposition 2.1], [33, Appendix A.1], ...").

Reproduce: `grep -n "coordinate proof follows" exposition.md paper.tex`; compare the character before the first citation.

Fix: restore the sentence break, or move each list into a sentence of its own ("For the classical background see ...").

### 12. EXPOSITION. Results are attributed to "Proposition 3" that it does not state, and non-Lean mathematics inside proofs is unlabelled

Proposition 3 is the one-box inequality, and the concordance maps it to `re_swapSum_le'`. The paper cites "the calculation in Proposition 3" or "the transfer-square calculation in Proposition 3" six times for a different result, the two-column bound X_{cc'} ≤ min(h_c,h_{c'}) from exterior transfers: p3 l15, p4 l46, p5 l11, p11 l4, p11 l50, p14 l43. That computation is an aside in the proof of Proposition 3 (p8 l47–l55). It is not a numbered result and it is not in the Lean: `grep -ciE "wedge|exterior|contraction|⋀|antisymm|projector|highest|dominan|content" *.lean` in the CasimirBounds folder prints 0 for all five files.

The Limitations section (p16 l26–l27) says the non-Lean content is "the highest-weight proof and the two remarks". There is more, all inside proof environments of propositions that the concordance ties to Lean lemmas: the transfer squares (p8 l43–l55), the content-formula route (p8 l13–l25), the antisymmetrizer remark (p9 l28–l31), the heights formula (p13 l48–l54) and the pair-deficit formula (p3 l17–l19). I checked all of it and it is correct (finding 6), but a reader cannot tell from the text which sentences the Lean certifies.

Fix: state the two-column transfer bound as its own lemma, labelled as not in the Lean, and cite that; extend the Limitations sentence.

### 13. EXPOSITION. Overloaded symbols, and a notation table that omits section 2

- s is |B| in the table (p6 l48) and in Proposition 3, and the diagonal twist in p2 l41, p2 l52, p3 l27, p3 l36.
- k is "length of a weight prefix" in the table (p7 l16), a column height at p2 l20, p3 l17 and p4 l55, and a summation index at p3 l27.
- c is a column index in the table, the third coordinate of a slot (τ,i,c) at p3 l30 and l33, and c_τ is a Casimir scalar at p2 l52.
- q is a box in the table and the number of slots in Fin(q) at p2 l48 and p3 l30.
- Not in the table: τ, l_τ, w_τ, ν_τ, a, u, J, C_b, c_τ, fib, Y_p, A_i, A_i†, T.

### 14. EXPOSITION. Each proof mixes the argument with commentary on arguments that fail

A reader looking for the proof has to find it. Where each one starts:

- Prop 2: p8 l5–l12 only (tex 490–496). The paragraph before it (scalar backgrounds) and the one after (content formula) prove nothing about Proposition 2.
- Prop 3: p9 l10–l26 (tex 576–603). The first four paragraphs are motivation.
- Prop 4: p9 l39–l43 (tex 637–642).
- Prop 7: p11 l11–l24 (tex 766–784).
- Prop 8: p12 l3–l5 (tex 834–837).
- Prop 9: p12 l41 onward (tex 891–912).
- Theorem 10: p13 l31–l36 and l42–l47 (tex 947–953 and 960–966). The proof environment opens with an example, then a complete alternative proof that is not in the Lean, then the actual proof, interrupted at l37–l41 by another counterfactual.

The commentary is accurate and some of it is the most useful part of the paper (the n=2 counterexamples). It belongs in remarks, not inside the proofs.

### 15. EXPOSITION, minor. The concordance omits four closure lemmas that carry steps of the paper's proofs

`count_rhs` (CountSame.lean:11–20, "summing by label"), `count_same` (CountSame.lean:71–88, "one increasing ordering per pair"), `dot_pm_swap` (ReSwapSumLe.lean:18–27, self-adjointness of a swap) and `isWH_coeff_one_polynomial` (CountCross.lean:13–26, "the unique match gives exactly N"; the name has nothing to do with the content). The paper files these under routine facts with no Lean pointer.

### 16. EXPOSITION, minor. "Checked by hand" in a document no human checked

The label "(not in the Lean; checked by hand)" appears at p2 l18, p4 l27, p10 l6, p13 l14 and p13 l55. The notice on p1 says no human checked the text. The reconciliation ("checked by an AI model") comes only at p16 l26–l27. Say "checked outside Lean by an AI model" at the point of use.

### 17. CITATION, sampled: 19 of 20 pinpoints accurate

I downloaded 12 of the 23 mathematical sources and matched 20 pinpoints against the extracted text. Nineteen are accurate and one is weak (below). The accurate ones: Yang, Example 5.4 (projection of C_2 = ΣE_{ij}E_{ji}); Lévy, Proposition 2.2; Cautis–Kamnitzer–Morrison, section 4.2 and Lemma 4.2.3; Cesi, (4.1), Proposition 4.1, (4.2), Theorem 5.3, (5.9); Molev, (7)–(9); Gross–Taylor, (2.1)–(2.2); Gross, Appendix A.1 (the indicator-pairing count); Gleizer–Postnikov, Proposition 2.1 and section 2; Etingof 18.745, lectures 18, 25, 26 (Lemma 26.6 gives C = (λ, λ+2ρ)); Etingof 18.755, Theorem 27.3; Navrátil–Kamuntavičius–Barrett, (30) and (35), where (35) is the one-box projector formula with s+1 = A; Navrátil–Barrett, (15). Titles and authors match the bibliography.

The weak one: p14 l25–l29 (tex 1007–1009) cites [18, §2] for "Normalized alternation identifies Λ^{h_c}ℂ^n isometrically with the alternating tensors ... divided by √(h_c!)". Section 2 of Gleizer–Postnikov says only that the fundamental representation V_{ω_k} is the k-th exterior power; the extracted text of the whole paper has no occurrence of "alternat", "antisymm", "sqrt" or "√" in that sense (`grep -ciE "antisymm|sqrt|√"` on the pdftotext output prints 0). The fact is true (finding 6 checks it); the source does not state it.

Not fetched: Perelomov–Popov, Howe, both Baur items, Hazewinkel–Vorst, Hazewinkel–Martin, Okounkov–Vershik, Frobenius, Szőke, Jucys, Macdonald, and the nine write-ups [3]–[11] with Rodgers's section 3.18.

## Attacks that failed

- Degenerate sizes: n = 0, n = 1, S empty, f = 0, s = 0, s > n (no alternating tensors), a full column of height n (the transfer target vanishes and X = h_c·Id exactly).
- Convention errors: the matrix-unit direction, the order of indices in Proposition 1, the side on which permutations compose in P_{pq}P_{pq'} = P_{pq'}P_{qq'} (true under either composition order; the wrong relation P_{pq}P_{pq'} = P_{pq}P_{qq'} is rejected), conjugate-linearity of the inner product.
- Hidden hypotheses: decidable equality on C, finiteness of C (not assumed and not needed), empty column indices in the row hypothesis of Propositions 7 to 9 (forces 0 ≤ N, which the paper's remark at p11 l28–l29 states).
- Negative scale N in Propositions 7 to 9: 78 random instances with N < 0 pass.
- The quantity computed against the quantity claimed: the coefficient written by labels, by heights and as Γ_n(λ) agree in every configuration, and the supremum equals it.
- Stale oleans: I recompiled the ten closure files from the reviewed tree instead of loading the prebuilt ones; the ten sources are byte-identical to those in the prebuilt workspace, and the review copy of CasBoundHolds.lean is identical to the tree's.

## Not checked

- Whether the Lean community certification happened, and the release date.
- The sources listed as not fetched in finding 17.
- Process counts in section 3 (22 findings, three further edits, 12 hand computations, about 50 citations of which 31 were corrected or removed) and the model names.
- Whether the answer key for `typePrimesN` was hidden from every step of the pipeline.
- Mathlib itself and the Lean kernel; I rebuilt only the 975 project lines against prebuilt Mathlib oleans.
- The rest of the archive.

## Confidence

High that the mathematics is right, for four independent reasons that agree: the statements in the paper typecheck as instances of the named Lean theorems after I recompiled the closure myself; the Lean proofs use only propext, Classical.choice and Quot.sound, and the same axiom report exposes a deliberate sorry; a numerical implementation built from the Lean definitions finds the inequality true and sharp on 384 configurations and false on each of three variants with a hypothesis removed; and a second, classical proof (highest weights) gives the same coefficient. The residual risk is in my transcription of statements into the checks, and the exhaustive numerics stop at n = 4 and six or seven slots. Medium on finding 10: the gap in the published record is certain, the explanation is not. Finding 9 is certain as stated (the cited sources do not contain the claim) and says nothing about whether the claim is true.

verifier (Fable), subagent of the mathematics agent

## Appendix A. Self-contained check (numpy only)

```python
# mini_check.py -- self-contained re-check of Theorem 10 (casBound_holds) on small cases, with negative controls.
# Operators follow KTypeData.lean:17-27:  eAt p a b f I = [I p = a] f(update I p b);  pm s f I = f(I o s).
import itertools, math, numpy as np
def asg(n, m): return list(itertools.product(range(n), repeat=m))
def eAt(n, m, p, a, b):
    A = asg(n, m); ix = {x: k for k, x in enumerate(A)}; M = np.zeros((len(A),) * 2)
    for I in A:
        if I[p] == a: M[ix[I], ix[I[:p] + (b,) + I[p+1:]]] = 1
    return M
def pm(n, m, s):
    A = asg(n, m); ix = {x: k for k, x in enumerate(A)}; M = np.zeros((len(A),) * 2)
    for I in A: M[ix[I], ix[tuple(I[s[x]] for x in range(m))]] = 1
    return M
def casimir(n, m, S):       # K = sum_{a,c} G_ac G_ca,  G_ac = sum_{p in S} eAt p a c   (StepFormula.lean:91-92)
    G = {(a, c): sum((eAt(n, m, p, a, c) for p in S), np.zeros((n**m,) * 2)) for a in range(n) for c in range(n)}
    return sum(G[a, c] @ G[c, a] for a in range(n) for c in range(n))
def sgn(q):
    q = list(q); s = 1
    for i in range(len(q)):
        while q[i] != i: j = q[i]; q[i], q[j] = q[j], q[i]; s = -s
    return s
def alt(n, m, B):           # orthogonal projector onto tensors alternating in the slots B
    P = np.zeros((n**m,) * 2)
    for q in itertools.permutations(range(len(B))):
        s = list(range(m))
        for k, b in enumerate(B): s[b] = B[q[k]]
        P += sgn(q) * pm(n, m, tuple(s))
    return P / math.factorial(len(B))
def sup_ratio(n, labels, col, S, alternate=True):   # sup of Re<f,Kf>/||f||^2 over admissible f
    m = len(labels); P = np.eye(n**m)
    if alternate:
        for c in set(col):
            B = [p for p in range(m) if col[p] == c]
            if len(B) > 1: P = P @ alt(n, m, B)
    w, V = np.linalg.eigh((P + P.T) / 2); U = V[:, w > .5]
    return None if U.shape[1] == 0 else np.linalg.eigvalsh(U.T @ casimir(n, m, S) @ U)[-1]
def coeff(n, labels, S):
    mi = [sum(labels[p] == i for p in S) for i in range(n)]
    return sum(mi[i] * (mi[i] + 2 * i + 1 - n) for i in range(n))
bad = 0; cases = 0; gap = 0.0
for n in (1, 2, 3):
    for k in range(1, 4):
        for hs in itertools.combinations_with_replacement(range(1, n + 1), k):
            if sum(hs) > 6: continue
            labels = [i for h in hs for i in range(n - h, n)]; col = [c for c, h in enumerate(hs) for _ in range(h)]
            for r in range(k + 1):
                for sel in itertools.combinations(range(k), r):
                    S = [p for p in range(len(col)) if col[p] in sel]
                    lam = sup_ratio(n, labels, col, S); cases += 1
                    bad += lam > coeff(n, labels, S) + 1e-8; gap = max(gap, abs(lam - coeff(n, labels, S)))
print(f"theorem: {cases} configurations, violations = {bad}, max |sup - coefficient| = {gap:.1e}")
print("NEG partial column  (n=2, column {0,1}, S = label-0 box):", sup_ratio(2, [0, 1], [0, 0], [0]), ">", coeff(2, [0, 1], [0]))
print("NEG no upward closure (n=2, single box labelled 0):      ", sup_ratio(2, [0], [0], [0]), ">", coeff(2, [0], [0]))
print("NEG no alternation  (n=2, full column, any f):           ", sup_ratio(2, [0, 1], [0, 0], [0, 1], alternate=False), ">", coeff(2, [0, 1], [0, 1]))
```

Output on 2026-11-27:

```
theorem: 140 configurations, violations = 0, max |sup - coefficient| = 2.5e-14
NEG partial column  (n=2, column {0,1}, S = label-0 box): 1.9999999999999996 > 0
NEG no upward closure (n=2, single box labelled 0):       2.0 > 0
NEG no alternation  (n=2, full column, any f):            6.0 > 2
```

## Appendix B. Lean check file and its output

Compile after the ten closure modules, with `LEAN_PATH` set to the scratch output folder followed by the Mathlib package library folders, Lean 4.33.1, options `-D autoImplicit=false -D relaxedAutoImplicit=false -D maxSynthPendingDepth=3 -D maxHeartbeats=4000000`.

```lean
import Development.WeilBound.RepresentationTheoryGL.CasimirAlgebra.KugaCoordinates.CasimirBounds.CasBoundHolds

open Matrix Finset
open PositivityTheory.Rg.Cz

-- (1) axioms of the target theorem and of the seven public lemmas in the concordance
#print axioms PositivityTheory.Rg.Cz.casBound_holds
#print axioms PositivityTheory.Rg.Cz.pair_apply
#print axioms PositivityTheory.Rg.Cz.cas_expand'
#print axioms PositivityTheory.Rg.Cz.re_swapSum_le'
#print axioms PositivityTheory.Rg.Cz.count_up
#print axioms PositivityTheory.Rg.Cz.count_eqb
#print axioms PositivityTheory.Rg.Cz.count_cross
#print axioms PositivityTheory.Rg.Cz.cas_count

-- (2) the paper's Theorem 10, with the tableau condition unfolded as displayed in the paper
example (n : ℕ) (Q : Type) [Fintype Q] [DecidableEq Q] (C : Type) [DecidableEq C] (γ : Q → C)
    (b : Q → Fin n) (S : Finset Q) (f : TV n ℂ Q)
    (h1 : ∀ p q, γ p = γ q → b p = b q → p = q)
    (h2 : ∀ p i, b p < i → ∃ q, γ q = γ p ∧ b q = i)
    (h3 : ∀ p q, γ p = γ q → (p ∈ S ↔ q ∈ S))
    (h4 : ∀ p q, γ p = γ q → p ≠ q → pm (Equiv.swap p q) f = -f) :
    (star f ⬝ᵥ (∑ i, ∑ i', tE S (0 : Fin n → Fin n → Module.End ℂ ℂ) i i' * tE S 0 i' i :
      Module.End ℂ (TV n ℂ Q)) f).re ≤
      (∑ i : Fin n, ((S.filter fun p => b p = i).card : ℝ) *
        (((S.filter fun p => b p = i).card : ℝ) + 2 * (i : ℕ) + 1 - n)) * (star f ⬝ᵥ f).re :=
  casBound_holds n Q C γ b S ⟨h1, h2⟩ h3 f h4

-- (3) Proposition 3 as displayed (sum of real parts, p outside B, f alternating on B)
example (n : ℕ) (Q : Type) [Fintype Q] [DecidableEq Q] (B : Finset Q) (p : Q) (hp : p ∉ B) (f : TV n ℂ Q)
    (hf : ∀ q ∈ B, ∀ q' ∈ B, q ≠ q' → pm (Equiv.swap q q') f = -f) :
    ∑ q ∈ B, (star f ⬝ᵥ pm (Equiv.swap p q) f).re ≤ (star f ⬝ᵥ f).re := by
  have h := re_swapSum_le' f B p hp hf
  simpa only [Complex.re_sum] using h

-- (4) Proposition 9 as displayed (sum over q ≠ p written with erase)
example (n : ℕ) (Q : Type) [Fintype Q] [DecidableEq Q] (C : Type) [DecidableEq C] (γ : Q → C)
    (b : Q → Fin n) (S : Finset Q) (R : Q → Q → ℝ) (N : ℝ)
    (hT : IsTab γ b) (hS : ∀ p q, γ p = γ q → (p ∈ S ↔ q ∈ S))
    (hsymm : ∀ p q, R p q = R q p) (hsame : ∀ p q, γ p = γ q → p ≠ q → R p q = -N)
    (hcross : ∀ p ∈ S, ∀ c, c ≠ γ p → ∑ q ∈ S.filter (fun q => γ q = c), R p q ≤ N) :
    ((n * S.card : ℕ) : ℝ) * N + ∑ p ∈ S, ∑ q ∈ S.erase p, R p q ≤
      (∑ i : Fin n, ((S.filter fun p => b p = i).card : ℝ) *
        (((S.filter fun p => b p = i).card : ℝ) + 2 * (i : ℕ) + 1 - n)) * N :=
  cas_count hT hS R N hsymm hsame hcross

-- (5) known-negative control: the axiom report must expose an unproved statement
theorem neg_control : (1 : ℕ) = 2 := by sorry
#print axioms neg_control
```

Output:

```
MODULE StatementA exit=0 secs=42 errors=0 sorry_warnings=0
MODULE StatementB exit=0 secs=13 errors=0 sorry_warnings=0
MODULE StatementE exit=0 secs=12 errors=0 sorry_warnings=0
MODULE KTypeData exit=0 secs=15 errors=0 sorry_warnings=0
MODULE StepFormula exit=0 secs=13 errors=0 sorry_warnings=0
MODULE ReSwapSumLe exit=0 secs=18 errors=0 sorry_warnings=0
MODULE CountSame exit=0 secs=13 errors=0 sorry_warnings=0
MODULE Expand exit=0 secs=13 errors=0 sorry_warnings=0
MODULE CountCross exit=0 secs=14 errors=0 sorry_warnings=0
MODULE CasBoundHolds exit=0 secs=13 errors=0 sorry_warnings=0
'PositivityTheory.Rg.Cz.casBound_holds' depends on axioms: [propext, Classical.choice, Quot.sound]
'PositivityTheory.Rg.Cz.pair_apply' depends on axioms: [propext, Classical.choice, Quot.sound]
'PositivityTheory.Rg.Cz.cas_expand'' depends on axioms: [propext, Classical.choice, Quot.sound]
'PositivityTheory.Rg.Cz.re_swapSum_le'' depends on axioms: [propext, Classical.choice, Quot.sound]
'PositivityTheory.Rg.Cz.count_up' depends on axioms: [propext, Classical.choice, Quot.sound]
'PositivityTheory.Rg.Cz.count_eqb' depends on axioms: [propext, Classical.choice, Quot.sound]
'PositivityTheory.Rg.Cz.count_cross' depends on axioms: [propext, Classical.choice, Quot.sound]
'PositivityTheory.Rg.Cz.cas_count' depends on axioms: [propext, Classical.choice, Quot.sound]
Check.lean:48:8: warning: declaration uses `sorry`
'neg_control' depends on axioms: [sorryAx]
```
