# Evidence-checked revision, pass 2

Line numbers refer to assembled-v12.md. Old and new blocks give the exact replaced excerpts.

Base SHA-256 `78818e9342c4872fb82e33993dbb4fb8a0a01310e54416c7ea19cb68c06a4fda`.

## O1 — applied

Quoted fragment at v12 line 9. A later sentence on that line already gives the exact scalar equality. `ClozelCohomologicalOf.lean:37–43` uses the same \(c\) in the scalar identity for the automorphic Casimir and in the coefficient quadratic-form ceiling. `CoefGlueHolds.lean:97–104,120–150` identifies \(\sum_i\nu_i=|S|\), transfers the form by the isometry, adds the twist, and closes with the tableau bound and `arith`. By the equality in `SumFinVal.lean:111–114`, increasing the tableau coefficient by \(\varepsilon>0\) adds exactly \(\varepsilon\|v\|^2\) to the resulting upper estimate. Dropping the internal debit adds \(h_c(h_c-1)\) per column. Estimating cross-column swaps separately charges \(h_ch_{c'}\) per order, where the grouped charge is \(\min(h_c,h_{c'})\) (`CountCross.lean:28–57,104–153` and v12 lines 349, 366). Either loss, when positive, leaves this deduction of `IsSmall` short of its required ceiling.

### Line 9

Old

```text
Adding the twist correction \((-2s|S|+as^2)\|v\|^2\) to the zero-background bound makes the right-hand side \(c_\tau\|v\|^2\), where \(c_\tau\) is the automorphic Casimir scalar (`CoefGlueHolds.lean:120–150`, `SumFinVal.lean:111–114`).
```

New

```text
Adding the twist correction \((-2s|S|+as^2)\|v\|^2\) to the zero-background bound makes the right-hand side \(c_\tau\|v\|^2\), where \(c_\tau\) is the automorphic Casimir scalar (`CoefGlueHolds.lean:120–150`, `SumFinVal.lean:111–114`). The `IsSmall` comparison uses this same \(c_\tau\) as its ceiling, and a positive excess in the tableau coefficient would survive the twist and leave the estimate too weak for nonzero \(v\) (`ClozelCohomologicalOf.lean:39–43`).
```

## O2 — already fixed

The exact review quotation is absent. The corresponding opening at v12 line 11 reads “The exterior-transfer derivation below combines Lévy’s slot expansion with Howe’s exterior-algebra action.” Proposition 3 supplies the calculation at line 182. For \(T=\sum_i A_i\otimes A_i^\dagger\), the wedge–contraction identity reduces \(T^\dagger T\) to \(h_c\mathrm{Id}-\sum_{i,j} A_i^\dagger A_j\otimes A_j^\dagger A_i\). The matrix-unit contraction is the cross-column swap sum by `Expand.lean:32–55` (`pair_apply`). Summing the one-box identities from `ReSwapSumLe.lean:61–83` over source boxes also gives the deficit \(h_c\|f\|^2-\operatorname{Re}\langle f,X_{cc'}f\rangle\). The current text presents the pairwise argument as its own derivation from those ingredients.

## O3 — already fixed

The exact review quotation is absent. Its counterpart at v12 line 311 limits the pointwise comparison to “replacing each cross-column entry by its own equal-label charge.” Line 315 explicitly counts whole rows by label, charging \(2\binom{m_i}{2}N\) for label \(i\). In `CountCross.lean:13–57` (units4 slice 1-12), `hcross` bounds each row, with symmetry used after interchanging the sums in the second branch. The unique equal-label target makes the comparison row sum exactly \(N\). The displayed tensor example gives expectation \(1/2\) for each of the two cross-column swaps, including the unequal-label one.

## O4 — applied

Exact quotation at v12 line 58. In `count_up` (units4 slice 1-8, `CountSame.lean:22–39`), `hT.2 p i hi` supplies the higher-label witness \(q\) in the same column, and `(hS q p hq1).2 hp` puts \(q\) in \(S\). At \(n=2\), selecting all of a column with only label \(0\) gives zero higher labels, although \(n-1-b(p)=1\). Proposition 4 already assigns the hypotheses their respective roles at v12 line 223.

### Line 58

Old

```text
Here selecting whole columns ensures that each higher label charged to a box actually occurs in its column.
```

New

```text
Here upward closure supplies a box in the same column for each higher label, and whole-column selection puts each such box in \(S\).
```

## O5 — already fixed

The exact review quotation is absent. Decision 2 at v12 line 63 explicitly requires “an active column of height at least two” for the exclusion. For a nonempty selection of singleton columns, every active label is \(n-1\) by `KTypeData.lean:51–52`, and the alternation hypothesis of `StepFormula.lean:88–94` imposes no restriction on active slots. With \(d\) singleton columns the coefficient is \(d(d+n-1)=nd+d(d-1)\), the ambient maximum from `cas_expand'` (units4 slice 1-1). V12 line 357 gives the example with two singleton columns at \(n=2\).

## O6 — applied

Exact quotation at v12 line 164, with the parallel summary at line 48. For a partition \(\mu\) of \(d\) with at most \(n\) rows, the content sum is \(\sum_j\sum_{k=1}^{\mu_j}(k-j)\). Doubling and adding \(nd\) gives \(\sum_j\mu_j(\mu_j+n+1-2j)=\Gamma_n(\mu)\). For \(\mu\) dominated by \(\lambda\), set \(D_k=\sum_{j\le k}(\lambda_j-\mu_j)\) and \(v_j=\lambda_j+\mu_j+n+1-2j\). Then \(D_n=0\), and summation by parts gives \(\Gamma_n(\lambda)-\Gamma_n(\mu)=\sum_{k=1}^{n-1}D_k(v_k-v_{k+1})\ge0\), since \(D_k\ge0\) and \(v_k-v_{k+1}\ge2\). This is the comparison already proved at v12 line 359. Both content-route passages now point to it.

### Line 48

Old

```text
The converse, established in the literature on Young permutation modules, gives a full occurrence criterion.
```

New

```text
The converse, established in the literature on Young permutation modules, gives a full occurrence criterion. Proposition 2 converts the content sums to trace-form eigenvalues, which the dominance comparison in Theorem 10 bounds by \(\Gamma_n(\lambda)\).
```

### Line 164

Old

```text
On each such shape the content scalar, doubled and added to \(nd\), gives the corresponding trace-form eigenvalue. A full occurrence criterion is unnecessary for this bound.
```

New

```text
On each such shape \(\mu\), doubling the content sum and adding \(nd\) gives the trace-form eigenvalue \(\Gamma_n(\mu)\). The dominance comparison in Theorem 10 gives \(\Gamma_n(\mu)\le\Gamma_n(\lambda)\), so a full occurrence criterion is unnecessary.
```

## Verification

A Python script replayed the four excerpt replacements from this log and compared the result byte for byte with assembled-v13.md. Of the 403 lines, only 9, 48, 58 and 164 differ. Each of the other 399 lines remains byte-identical at its original position.
