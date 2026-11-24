# Revision log for assembled-v12.md

Locations refer to v11. All four audit quotations and all 19 reviewer quotations were found at their reported lines. The decisions below cover the findings in the two JSON reports and the four numbered findings in the local audit. Edit IDs refer to the exact text changes recorded below.

## Local logic audit

- Line 63, quantifiers — `applied`. E04 also resolves Astra R05 and Sol R0-06. The sign premise in `StepFormula.lean:88–94` is vacuous for two selected singleton columns labeled 1 at rank 2. By `Expand.lean:66–69`, the Casimir there is \(4\,\mathrm{Id}+2P\), so the entire symmetric maximum eigenspace is admissible. When an active column has two distinct slots, their swap fixes fully symmetric tensors and negates admissible tensors, excluding every nonzero vector of that symmetric subspace.
- Line 280, signs — `applied`. E07 also resolves Astra R07 and Sol R0-07. Summing the row bound in `CountCross.lean:28–34` in the two fixed orientations gives \((h_c+h_{c'})N\). Its change per unit increase in one height is \(N\). With two terminal-label columns of heights \(h\) and \(1\), \(N=-1\), and all cross entries \(-1\), the source row sums are \(-1\) and \(-h\), both at most \(-1\). The fixed-orientation total is \(-(h+1)\).
- Line 309, necessity — `applied`. E08 and E09 also resolve Astra R08 and Sol R0-08. The row hypothesis and symmetry are used in `CountCross.lean:28–57,85–102`. An unordered column pair can be oriented from the shorter column. Its terminal labels are exactly the intersection of the two columns’ labels. A chosen source row at label \(i\) costs at most \(N\) in each order. Since each of the \(m_i\) slots at label \(i\) is in a different column, there are \(\binom{m_i}{2}\) such rows, giving \(2\binom{m_i}{2}N\) for both orders.
- Line 337, signs — `applied`. E10 also resolves Astra R09 and Sol R0-09. `CountCross.lean:104–114` gives \(-N\) per distinct ordered same-column pair. A column of height \(h_c\) has \(h_c(h_c-1)\) such pairs. The contribution is \(-h_c(h_c-1)N\), with magnitude \(h_c(h_c-1)|N|\). A single column with \(C\) consisting of its index, \(N=-1\), and all distinct-slot entries equal to 1 gives a positive internal contribution.

## gpt-6.2-astra

- R01 (line 9) — `applied`. E01 also resolves R02 and Sol R0-01 through R0-03. V11 line 15 already identifies the slot instantiation. `CoefGlueHolds.lean:120–150` verifies the compression, the whole-column argument, the explicit call at line 144, and the use of its two sides in the twisted quadratic-form inequality.
- R02 (line 9) — `applied`. See E01 and Sol R0-03. `ClozelCohomologicalOf.lean:37–43` supplies the opposite trace and the upper bound by the automorphic scalar. `KugaGlueHolds.lean:80–100` passes the nonpositive Casimir-difference form to the vanishing argument, and line 17 uses that vanishing in the harmonic implication.
- R03 (line 11) — `applied`. E02 identifies the exterior-transfer argument as a derivation from the cited ingredients. E06 shows the computation: expanding \(T^\dagger T\) and using the contraction–wedge anticommutator leaves the source height times the identity minus the matrix-unit contraction. The contraction is the cross-column swap sum by `pair_apply` in `units4.json` (slice 1-4). This establishes the identity used in the exposition without making a claim about who first combined the ingredients.
- R04 (line 15) — `applied`. E03 also resolves Sol R0-04. `PKTypeA.lean:135–182` counts \(\nu_\tau(i)+i\) enlarged slots. `StepFormula.lean:42–50` gives the product of transferred factors, and `PKType.lean:26–49` reduces it to \((u+s)^n\) and passes it to spherical descent. `PKType.lean:70–80` returns the original slots with counts from `cntQ`.
- R05 (line 63) — `applied`. See E04 and audit line 63. `StepFormula.lean:90` requires distinct same-column slots, which the two singleton columns lack. Thus every ambient maximizing vector is admissible in that example.
- R06 (line 164) — `applied`. E05 follows `Expand.lean:66–69`, which adds \(nd\,\mathrm{Id}\) to the ordered swap sum. There are \(d(d-1)\) ordered swaps, each with operator norm 1, and a pure tensor with the same basis vector at every active slot attains their sum of \(d(d-1)\). For \(n=2,d=1\), the two maxima are 0 for the swap sum and 2 for the Casimir.
- R07 (line 280) — `applied`. See E07 and audit line 280. `CountCross.lean:28–34` allows real \(N\), and the fixed-orientation bounds have the signed slope \(N\).
- R08 (line 309) — `applied`. See E08, E09, and audit line 309. `CountCross.lean:35–57` compares whole rows in the orientation where each source label has a match. Grouping these rows across unordered column pairs gives \(2\binom{m_i}{2}N\), so the pointwise comparison is only relevant to entrywise replacement.
- R09 (line 337) — `applied`. See E10 and audit line 337. The hypothesis `hsame` in `CountCross.lean:104–114` yields signed contribution \(-h_c(h_c-1)N\), which is positive for \(N<0\) and \(h_c\ge2\).
- R10 (line 398) — `applied`. E11 follows the calls in `CountCross.lean:90,96,101`. The first two invoke the grouping helper, slice 1-11 in `units4.json`. The last invokes the two-column comparison helper, slice 1-12. The `count_cross` proof is the caller in all three cases.

## gpt-6.2-sol

- R0-01 (line 9) — `applied`. See E01 and Astra R01. `CoefGlueHolds.lean:121,142–144` verifies alternation of \(Jv\), whole-column membership of the embedding fiber, and the call with rank `a`, slots `Fin q`, column type `ℕ`, and the supplied maps `col` and `b`.
- R0-02 (line 9) — `applied`. See E01 and Astra R01. `CoefGlueHolds.lean:120–135` identifies the compressed quadratic form and preserves the norm. Lines 136–150 use the zero-background inequality and the correction \((-2s|S|+as^2)\|v\|^2\). `SumFinVal.lean:111–114` identifies the corrected coefficient with the automorphic scalar, supplying the upper bound in `ClozelCohomologicalOf.lean:43`. The opposite trace is proved separately in `CoefGlueHolds.lean:102–119`.
- R0-03 (line 9) — `applied`. See E01 and Astra R02. `KgCasDiff.lean:37–52` uses the opposite traces to obtain twice the sum of coefficient-minus-automorphic Casimir differences. `KugaGlueHolds.lean:80–100` uses the fiberwise inequalities to bound that form by zero and derive vanishing. `KugaAbsHolds.lean:152–181` proves the positivity step. The harmonic implication in `IsStarRep.lean:67–70` uses vanishing in all degrees and the nonzero cochain.
- R0-04 (line 15) — `applied`. See E03 and Astra R04. `PKTypeA.lean:171–182` gives the increase by \(i\) at each embedding. `PKType.lean:26–49,70–80` uses the enlarged character for descent and the original label counts for the returned slot data.
- R0-05 (line 52) — `rejected` as a basis for an edit under the evidence rule. The quotation occurs at line 52. The proof of `re_swapSum_le'` in `units4.json` (slice 1-14) and `ReSwapSumLe.lean:29–83` verify the swap calculation underlying the projector, while the coset computation in v11 line 205 gives the projector itself. This mathematical evidence cannot establish or disprove Murphy’s historical independence. The attribution remains unverified within the allowed sources.
- R0-06 (line 63) — `applied`. See E04 and audit line 63. `StepFormula.lean:90` is vacuous in the two-singleton example, and `Expand.lean:66–69` gives \(4\,\mathrm{Id}+2P\), with its whole maximal eigenspace admissible.
- R0-07 (line 280) — `applied`. See E07 and audit line 280. Under `CountCross.lean:28–34`, both fixed orientations are bounded by the number of source rows times the real \(N\), so the slope of their sum has the sign of \(N\).
- R0-08 (line 309) — `applied`. See E08, E09, and audit line 309. The row comparison and symmetry at `CountCross.lean:35–57` give the label-indexed row count. In the existing rank-two tensor example, the unequal-label swap has expectation \(1/2\), which still disproves the pointwise inequality.
- R0-09 (line 337) — `applied`. See E10 and audit line 337. `CountCross.lean:104–114,126–131` gives the internal contribution as the number of ordered distinct pairs times \(-N\). At \(N=-1\) a full active column of height \(n\ge2\) contributes \(n(n-1)>0\).

## Review summaries

The unnumbered “heart” entries also match the text and evidence. Astra’s first four entries and Sol’s first four entries describe the matrix-unit expansion, the negative off-diagonal terms in the defect square, the shorter-column orientation, and the exact internal count. These steps agree with `Expand.lean:26–69`, `ReSwapSumLe.lean:29–83`, and `CountCross.lean:28–57,104–137`. Sol’s final entry describes the per-slot sum and collection by label, verified by `CountCross.lean:138–150` and `count_rhs` in `units4.json`. Astra’s final entry identifies the implicit compression and Kuga sign, which E01 makes explicit through the findings cited there.

## Exact edits

The code blocks show exact replacement spans on the cited v11 lines. Each insertion is placed directly after its anchor line and starts with the displayed blank line.

### E01 — v11 line 9

Old text

```text
The separate Kuga argument uses the small coefficient, the cochain, and unitarity up to twist to obtain cohomology, and the assembled theorem gives cohomologicality for regular algebraic cuspidal representations of positive rank over totally complex number fields (`ClozelCohomologicalOf.lean:51–56`, `ClozelCohomological.lean:8–9`, `ClozelCohomologicalModel.lean:10–12`). The proof-level instantiation of the slot data and the use of the individual terms of the inequality in coefficient gluing are **not traced**.
```

New text

```text
At rank \(a\), coefficient gluing takes slots \(\mathrm{Fin}(q)\), column indices \(\mathbb N\), the supplied column and label maps, \(S=\mathrm{fib}(\mathrm{lab},\tau)\), and \(f=Jv\) for each coefficient vector \(v\). Intertwining expresses the coefficient Casimir as \(J^\dagger C_bJ\), where \(C_b\) is the twisted ambient Casimir at \(\tau\), and the isometry gives \(\|Jv\|^2=\|v\|^2\). The coefficient quadratic form on \(v\) is thus the ambient form on \(Jv\). Adding the twist correction \((-2s|S|+as^2)\|v\|^2\) to the zero-background bound makes the right-hand side \(c_\tau\|v\|^2\), where \(c_\tau\) is the automorphic Casimir scalar (`CoefGlueHolds.lean:120–150`, `SumFinVal.lean:111–114`). The separate Kuga argument uses unitarity up to twist and the opposite trace scalars to express its Casimir difference as twice the sum of the coefficient-minus-automorphic differences. The fiberwise upper bound makes this form nonpositive on the tensor product. Positivity then forces the cochain differential to vanish in every degree, and the nonzero cochain yields cohomology (`KgCasDiff.lean:37–52`, `KugaGlueHolds.lean:15–21,80–100`, `KugaAbsHolds.lean:137–181`, `IsStarRep.lean:67–70`). The assembled theorem gives cohomologicality for regular algebraic cuspidal representations of positive rank over totally complex number fields (`ClozelCohomologicalOf.lean:51–56`, `ClozelCohomological.lean:8–9`, `ClozelCohomologicalModel.lean:10–12`).
```

### E02 — v11 line 11

Old text

```text
The classical exterior-transfer argument expands the Casimir into slot transpositions and expresses the deficit for each pair of alternating columns as the squared norm of a transfer out of the shorter column. Howe’s exterior-algebra action supplies the transfers.
```

New text

```text
The exterior-transfer derivation below combines Lévy’s slot expansion with Howe’s exterior-algebra action. The calculation in Proposition 3 expresses the deficit for each pair of alternating columns as the squared norm of a transfer out of the shorter column.
```

### E03 — v11 line 15

Old text

```text
The archive adds two copies of the pairs \(c<i\) indexed by one embedding from each conjugate pair, obtains a compact-fixed tensor by spherical descent, and takes its signed column sum, whose terms a same-column transposition reindexes with opposite sign.
```

New text

```text
The archive adds two copies of the pairs \(c<i\) indexed by one embedding from each conjugate pair. The two copies together add \(i\) occurrences of label \(i\) at each embedding \(\tau\), giving the enlarged multiplicity \(\nu_\tau(i)+i=s-l_\tau(w_\tau(i))\). Each transferred quantum determinant factor \(u+l_\tau(w_\tau(i))+\nu_\tau(i)+i\) is therefore \(u+s\). Spherical descent uses the resulting eigenvalue \((u+s)^n\) to obtain a compact-fixed tensor. The archive takes its signed column sum, whose terms a same-column transposition reindexes with opposite sign. The slot data for the Casimir bound use the original multiplicities \(\nu_\tau(i)\).
```

### E04 — v11 line 63

Old text

```text
since the maximum on the entire tensor power includes directions excluded by alternation.
```

New text

```text
since an active column of height at least two excludes the fully symmetric active tensors that attain the ambient maximum.
```

### E05 — v11 line 164

Old text

```text
For decision 2, taking the largest eigenvalue of the transposition sum on the entire active tensor power gives the symmetric value \(nd+d(d-1)\) for \(n>0\).
```

New text

```text
For decision 2, the ordered transposition sum on the entire active tensor power has largest eigenvalue \(d(d-1)\) for \(n>0\), attained on fully symmetric tensors. Adding the diagonal term gives the ambient Casimir maximum \(nd+d(d-1)\).
```

### E06 — insertion after v11 line 180

Anchor

```text
**Proof.** For decision 3, estimating each matrix element by Cauchy–Schwarz, using that each swap is unitary, gives only \(s\|f\|^2\) for \(s=|B|\). This agrees with the desired bound at \(s=1\) and loses \((s-1)\|f\|^2\) for \(s>1\). For columns of heights \(h_c,h_{c'}\), summing those separate estimates costs \(2h_ch_{c'}\|f\|^2\) in the two orders. Grouping the swaps into a row costs one squared norm per source box and ultimately gives \(2\min(h_c,h_{c'})\|f\|^2\). At equal heights the separate and grouped coefficients are \(2h_c^2\) and \(2h_c\), respectively. The exterior approach also obtains this pair bound. It forms the full interaction \(X_{cc'}\) on two wedges and uses the positive transfer squares \(h_c\mathrm{Id}-X_{cc'}\) and \(h_{c'}\mathrm{Id}-X_{cc'}\). The present estimate uses only the target's alternation and applies to any set \(B\), a convenience since the application takes \(B=S_c\) for a column other than the source column. [Two-column exterior transfers, Theorem 4.2.1](https://arxiv.org/pdf/1210.6437), [Howe, Theorem 8 and the exterior-algebra example](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf).
```

Old text is empty.

New text

```text

To compute the first transfer square, write \(A_i\) for contraction by \(e_i\) and \(A_i^\dagger\) for exterior multiplication by \(e_i\). The transfer from \(c\) to \(c'\) is \(T=\sum_i A_i\otimes A_i^\dagger\). Using \(A_iA_j^\dagger=\delta_{ij}\mathrm{Id}-A_j^\dagger A_i\) and \(\sum_i A_i^\dagger A_i=h_c\mathrm{Id}\) on the source wedge gives \(T^\dagger T=h_c\mathrm{Id}-\sum_{i,j} A_i^\dagger A_j\otimes A_j^\dagger A_i\). The operator \(A_i^\dagger A_j\) is the matrix unit acting on the wedge, so the sum is \(X_{cc'}\) by the matrix-unit contraction of Proposition 1. Reversing the transfer gives the square with \(h_{c'}\).
```

### E07 — v11 line 280

Old text

```text
Heuristic: If one height grows and the other stays fixed, the sum of the fixed-orientation bounds grows linearly with the taller column, whereas the number of common labels stays at most the fixed height. Orienting both sums from the shorter column keeps the bound at that fixed scale.
```

New text

```text
If one height grows while the other stays fixed, the sum of the fixed-orientation bounds \((h_c+h_{c'})N\) increases for \(N>0\), stays zero for \(N=0\), and decreases for \(N<0\). Once the shorter height is fixed, the number of common labels is fixed as well, and orienting both sums from the shorter column gives \(2\min(h_c,h_{c'})N\) in total.
```

### E08 — v11 line 309

Old text

```text
For decision 6, a direct count by tableau label would require the pointwise comparison \(R(p,q)\le N\mathbf 1_{b(p)=b(q)}\) at cross-column pairs.
```

New text

```text
For decision 6, replacing each cross-column entry by its own equal-label charge would use the pointwise comparison \(R(p,q)\le N\mathbf 1_{b(p)=b(q)}\).
```

### E09 — insertion after v11 line 311

Anchor

```text
Use Proposition 6 on both sides, with \(R\) on the left and \(N\mathbf 1_{b(p)=b(q)}\) on the right. Each side then ranges over the same ordered pairs of distinct active columns. Proposition 7 gives the inequality for every such pair, and addition proves the result.
```

Old text is empty.

New text

```text

The same bound can be counted by label using whole rows. Orient each unordered pair of active columns from the shorter column, with one choice of orientation in a tie. Each source label \(i\) occurs once there and also occurs in the target column. Its row contributes at most \(N\), and symmetry lets that row bound account for both orders. Exactly \(\binom{m_i}{2}\) unordered column pairs contain \(i\) in both columns, so the total upper bound from rows charged to label \(i\) is \(2\binom{m_i}{2}N\).
```

### E10 — v11 line 337

Old text

```text
Heuristic: In a tall column the internal debit has leading magnitude \(h_c^2N\), compared with a diagonal charge \(nh_cN\).
```

New text

```text
The signed internal contribution from a column of height \(h_c\) is \(-h_c(h_c-1)N\), of magnitude \(h_c(h_c-1)|N|\). In the tensor application \(N=\|f\|^2\ge0\), so for a tall column the internal debit has leading magnitude \(h_c^2N\), compared with a diagonal charge \(nh_cN\).
```

### E11 — v11 line 398

Old text

```text
Absorbed statement in planner, with call sites in slices 1-11 and 1-12
```

New text

```text
Absorbed statement in planner. Its proof calls the helpers in slices 1-11 and 1-12.
```
