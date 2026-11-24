# Fix log

Line and citation numbers refer to assembled-v13.md. The blocks show the exact changed text. When a line has several edits, they are listed under the finding each edit addresses.

## 1. Done

Replaced planning labels with mathematical prose and source locations checked against the named Lean declarations. Kept the scope statement about the three omitted arguments in plain text.

### v13 line 15

Old

~~~text
**not traced**
~~~

New

~~~text
outside the scope of this exposition
~~~

### v13 line 62

Old

~~~text
1. Decision 1 proves the bound on the whole alternating space in Theorem 10, since evaluating on the highest wedges tests a single vector.
~~~

New

~~~text
- Theorem 10 bounds every column-alternating tensor. Evaluating the Casimir on the tensor of highest wedges tests a single vector.
~~~

### v13 line 63

Old

~~~text
2. Decision 2 expands the operator by Propositions 1 and 2 and retains the column signs in Proposition 9
~~~

New

~~~text
- Propositions 1 and 2 expand the operator, and Proposition 9 retains the column signs
~~~

### v13 line 64

Old

~~~text
3. Decision 3 groups swaps into one target column in Proposition 3
~~~

New

~~~text
- Proposition 3 groups swaps into one target column
~~~

### v13 line 65

Old

~~~text
4. Decision 4 proves Proposition 3 by squaring the defect
~~~

New

~~~text
- Proposition 3 squares the defect
~~~

### v13 line 66

Old

~~~text
5. Decision 5 uses symmetry and label inclusion in Proposition 7
~~~

New

~~~text
- Proposition 7 uses symmetry and label inclusion
~~~

### v13 line 67

Old

~~~text
6. Decision 6 uses Proposition 6 to group
~~~

New

~~~text
- Proposition 6 groups
~~~

### v13 line 68

Old

~~~text
7. Decision 7 uses whole columns in Proposition 4 and combines the counts in Propositions 5 and 9
~~~

New

~~~text
- Proposition 4 uses whole columns, and Proposition 9 combines its count with the count in Proposition 5
~~~

### v13 line 164

Old

~~~text
For decision 2, the ordered transposition
~~~

New

~~~text
The ordered transposition
~~~

### v13 line 180

Old

~~~text
For decision 3, estimating
~~~

New

~~~text
Estimating
~~~

### v13 line 184

Old

~~~text
For decision 4, a bound
~~~

New

~~~text
A bound
~~~

### v13 line 225

Old

~~~text
For decision 7, consider
~~~

New

~~~text
Consider
~~~

### v13 line 280

Old

~~~text
For decision 5, applying
~~~

New

~~~text
Applying
~~~

### v13 line 311

Old

~~~text
For decision 6, replacing
~~~

New

~~~text
Replacing
~~~

### v13 line 357

Old

~~~text
For decision 1, evaluating
~~~

New

~~~text
Evaluating
~~~

### v13 line 394

Old

~~~text
 (sole planner key result)
~~~

New

Removed.

### v13 line 394

Old

~~~text
Slice 1, including the definition of `CasBound`
~~~

New

~~~text
CasBoundHolds.lean:9–32. Statement in StepFormula.lean:88–94.
~~~

### v13 line 395

Old

~~~text
Slice 1-4
~~~

New

~~~text
Expand.lean:32–55
~~~

### v13 line 396

Old

~~~text
Slice 1-1
~~~

New

~~~text
Expand.lean:66–92
~~~

### v13 line 397

Old

~~~text
Slice 1-14
~~~

New

~~~text
ReSwapSumLe.lean:29–83
~~~

### v13 line 398

Old

~~~text
Slice 1-8
~~~

New

~~~text
CountSame.lean:22–44
~~~

### v13 line 399

Old

~~~text
Slice 1-9
~~~

New

~~~text
CountSame.lean:46–69
~~~

### v13 line 400

Old

~~~text
CountCross, slice 1-11
~~~

New

~~~text
CountCross.lean:59–83
~~~

### v13 line 401

Old

~~~text
CountCross, slice 1-12
~~~

New

~~~text
CountCross.lean:28–57
~~~

### v13 line 402

Old

~~~text
Absorbed statement in planner. Its proof calls the helpers in slices 1-11 and 1-12.
~~~

New

~~~text
CountCross.lean:85–102. Uses the lemmas for Propositions 6 and 7.
~~~

### v13 line 403

Old

~~~text
Slice 1-6
~~~

New

~~~text
CountCross.lean:104–153
~~~

## 2. Done

CountCross.lean:59 and :28 declare the helpers for Propositions 6 and 7, respectively, as private theorems.

### v13 line 400

Old

~~~text
`sum_sum_ite_col_ne_eq_sum_by_col`
~~~

New

~~~text
`sum_sum_ite_col_ne_eq_sum_by_col` (private)
~~~

### v13 line 401

Old

~~~text
`sum_filter_col_le_sum_ite_of_bound`
~~~

New

~~~text
`sum_filter_col_le_sum_ite_of_bound` (private)
~~~

## 3. Done

ClozelCohomologicalOf.lean:55–63 contains clozelCohomological_of. Lines 51–53 define Kuga.

### v13 line 9

Old

~~~text
ClozelCohomologicalOf.lean:51–56
~~~

New

~~~text
ClozelCohomologicalOf.lean:55–63
~~~

## 4. Done

The row-bound premise in CountCross.lean:30 requires a selected source box and a different column index. If that target column is empty, its sum is zero. With just one index in the column set the premise is vacuous.

### v13 line 290

Old

~~~text
An empty target column also forces \(N\ge0\) whenever there is a source box in \(S\).
~~~

New

~~~text
If \(p\in S\) and some column \(c\ne\gamma(p)\) has \(S_c=\varnothing\), the row bound for \(p\) and \(c\) reads \(0\le N\).
~~~

## 5. Done

StepFormula.lean:88–94 and CasBoundHolds.lean:9–32 establish the inequality with whole-column selection by the coordinate argument. The prefix bounds and telescoping verify the alternative highest-weight comparison by hand. The nested highest wedges have highest weight with coordinates m_{n-j}, so evaluation gives equality. A terminal subcolumn retains every higher label above each selected box, and terminal intervals are nested.

### v13 line 7

Old

~~~text
The highest-weight proof
~~~

New

~~~text
The highest-weight proof (not in the Lean; checked by hand)
~~~

### v13 line 46

Old

~~~text
The highest-weight proof
~~~

New

~~~text
The highest-weight proof (not in the Lean; checked by hand)
~~~

### v13 line 227

Old

~~~text
**Remarks.** Selecting terminal subcolumns
~~~

New

~~~text
**Remarks.** In a variant (not in the Lean; checked by hand), selecting terminal subcolumns
~~~

### v13 line 359

Old

~~~text
The full highest-weight argument supplies the missing comparison.
~~~

New

~~~text
**Highest-weight proof (not in the Lean; checked by hand).**
~~~

### v13 line 370

Old

~~~text
For \(n>0\), the tensor
~~~

New

~~~text
Sharpness (not in the Lean; checked by hand). For \(n>0\), the tensor
~~~

## 6. Done

Added the archive credit and publication date supplied in the findings. Replaced prior-art assessment labels and attributed the coordinate steps to Alpöge.

### After v13 line 2

Old

No text at this location.

New

~~~text
This is an exposition of the tableau Casimir bound in Levent Alpöge’s 2026 Lean archive, published on 2026-11-20. [Lean archive](https://alpo.ge/lean.tar.gz).
~~~

### v13 line 46

Old

~~~text
 — precedent found
~~~

New

Removed.

### v13 line 50

Old

~~~text
 — precedent found
~~~

New

Removed.

### v13 line 52

Old

~~~text
 — precedent found
~~~

New

Removed.

### v13 line 54

Old

~~~text
 — precedent found
~~~

New

Removed.

### v13 line 56

Old

~~~text
 — partial precedent
~~~

New

Removed.

### v13 line 58

Old

~~~text
 — partial precedent
~~~

New

Removed.

### v13 line 7

Old

~~~text
using a dominance bound on its highest weight, while the tableau hypotheses give no constituent decomposition. For one box outside an alternating column of size \(k\), the coordinate proof instead forms
~~~

New

~~~text
using dominance of highest weights. In Alpöge’s coordinate proof, for one box outside an alternating column of size \(k\), one forms
~~~

### v13 line 46

Old

~~~text
The coordinate proof bounds
~~~

New

~~~text
Alpöge’s coordinate proof bounds
~~~

### v13 line 50

Old

~~~text
Here those signs hold for every column-alternating tensor, even without row symmetrization.
~~~

New

~~~text
Column alternation alone gives these signs in Alpöge’s proof.
~~~

### v13 line 52

Old

~~~text
The proof here recovers its norm identity by multiplying swaps.
~~~

New

~~~text
Alpöge’s coordinate proof derives the norm identity by multiplying swaps.
~~~

### v13 line 54

Old

~~~text
Here the one-box inequality is summed in the original slots.
~~~

New

~~~text
Alpöge’s proof sums the one-box inequality in the original slots.
~~~

### v13 line 56

Old

~~~text
Here inclusion of the inherited label intervals chooses the source for both orders of the swap sum.
~~~

New

~~~text
Alpöge’s proof uses inclusion of the inherited label intervals to choose the source for both orders of the swap sum.
~~~

### v13 line 58

Old

~~~text
Here upward closure supplies
~~~

New

~~~text
In Alpöge’s proof, upward closure supplies
~~~

### v13 line 180

Old

~~~text
The present estimate uses only the target's alternation
~~~

New

~~~text
The one-box estimate uses only the target’s alternation
~~~

### v13 line 184

Old

~~~text
Here the square will certify it for one box and one target set before any source-column height enters.
~~~

New

~~~text
The one-box calculation below uses the square with just one source box and one target set.
~~~

### v13 line 280

Old

~~~text
Here symmetry permits both orientations, and label inclusion picks the orientation used for the count.
~~~

New

~~~text
In the coordinate proof, symmetry permits both orientations, and label inclusion picks the orientation used for the count.
~~~

### v13 line 359

Old

~~~text
The following argument obtains the bound in the original coordinates.
~~~

New

~~~text
Alpöge’s coordinate proof follows.
~~~

## 7. Done

The norm identity in ReSwapSumLe.lean:61–82 is \(\|g\|^2=(1+|B|)\operatorname{Re}\langle f,g\rangle\) for \(g=f-Yf\). Divide by \(1+|B|\) before summing over source boxes. The audit’s antisymmetric two-singleton example gives deficit 2 and squared defect 4. The two nearby summaries now specify that the upper bound follows from nonnegativity.

### v13 line 11

Old

~~~text
The Lean proof obtains the same deficits by summing squared one-box antisymmetrizer defects in tensor coordinates and uses the inherited labels of whole selected columns to express the bound in label multiplicities.
~~~

New

~~~text
In tensor coordinates, for a source column \(c\) and a target column \(c'\) of height \(k=h_{c'}\), the pair deficit is \(h_c\|f\|^2-\operatorname{Re}\langle f,X_{cc'}f\rangle=\frac{1}{k+1}\sum_{p\in S_c}\|f-Y_pf\|^2\), where \(Y_p=\sum_{q\in S_{c'}}P_{pq}\). The Lean proof uses this normalization for the one-box inequality and the inherited labels of whole selected columns to express the bound in label multiplicities.
~~~

### v13 line 5

Old

~~~text
bounds the entire sum by one squared norm
~~~

New

~~~text
bounds the entire sum using the nonnegativity of one squared norm
~~~

### v13 line 7

Old

~~~text
bounds the entire sum by one squared norm
~~~

New

~~~text
bounds the entire sum using the nonnegativity of one squared norm
~~~

## 8. Done

Applied all 31 non-confirmed citation findings from citation-check.md. Corrected or narrowed 28 occurrences and removed 3. The seven incorrect Theorem 4.2.1 references now cite the transfer actions in Lemma 4.2.3. Proposition 3 supplies the transfer-square calculation. Removed the two Han references because Yang already supplies the trace-form scalar. Removed Murphy’s §3 and its attribution because the report could not verify the section. Updated eight confirmed occurrences to alternate links supplied in the report. The report supplied no alternate URL for Baur’s confirmed article at 46.5, so its link was retained.

### v13 citation 48.4 (corrected)

Old

~~~text
[Exterior transfer operators, Theorem 4.2.1](https://arxiv.org/pdf/1210.6437)
~~~

New

~~~text
[Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437)
~~~

### v13 citation 54.2 (corrected)

Old

~~~text
[Cautis, Kamnitzer and Morrison, Thm. 4.2.1](https://arxiv.org/pdf/1210.6437)
~~~

New

~~~text
[Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437)
~~~

### v13 citation 56.1 (corrected)

Old

~~~text
[Cautis, Kamnitzer and Morrison, Thm. 4.2.1](https://arxiv.org/pdf/1210.6437)
~~~

New

~~~text
[Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437)
~~~

### v13 citation 180.1 (corrected)

Old

~~~text
[Two-column exterior transfers, Theorem 4.2.1](https://arxiv.org/pdf/1210.6437)
~~~

New

~~~text
[Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437)
~~~

### v13 citation 280.1 (corrected)

Old

~~~text
[Two-column exterior transfers, Theorem 4.2.1](https://arxiv.org/pdf/1210.6437)
~~~

New

~~~text
[Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437)
~~~

### v13 citation 311.1 (corrected)

Old

~~~text
[Two-column exterior transfers, Theorem 4.2.1](https://arxiv.org/pdf/1210.6437)
~~~

New

~~~text
[Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437)
~~~

### v13 citation 386.1 (corrected)

Old

~~~text
[Exterior transfers, Theorem 4.2.1](https://arxiv.org/pdf/1210.6437)
~~~

New

~~~text
[Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437)
~~~

### v13 citation 48.7 (corrected)

Old

~~~text
[Howe, Theorem 8 and the exterior-algebra example](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

New

~~~text
[Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

### v13 citation 54.4 (corrected)

Old

~~~text
[Howe, Theorem 8 and the exterior-algebra example](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

New

~~~text
[Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

### v13 citation 56.3 (corrected)

Old

~~~text
[Howe, Theorem 8 and the exterior-algebra example](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

New

~~~text
[Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

### v13 citation 180.2 (corrected)

Old

~~~text
[Howe, Theorem 8 and the exterior-algebra example](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

New

~~~text
[Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

### v13 citation 280.2 (corrected)

Old

~~~text
[Howe, Theorem 8 and the exterior-algebra example](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

New

~~~text
[Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

### v13 citation 311.2 (corrected)

Old

~~~text
[Howe, Theorem 8 and the exterior-algebra example](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

New

~~~text
[Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

### v13 citation 386.2 (corrected)

Old

~~~text
[Howe, Theorem 8 and the exterior-algebra example](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

New

~~~text
[Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf)
~~~

### v13 citation 48.3 (corrected)

Old

~~~text
[Transposition contents, §§3–6](https://www.esi.ac.at/preprints/esi333.pdf)
~~~

New

~~~text
[Transposition contents, Okounkov–Vershik, (2.1) and Proposition 6.2](https://www.esi.ac.at/preprints/esi333.pdf)
~~~

### v13 citation 164.3 (corrected)

Old

~~~text
[Transposition contents, §§3–6](https://www.esi.ac.at/preprints/esi333.pdf)
~~~

New

~~~text
[Transposition contents, Okounkov–Vershik, (2.1) and Proposition 6.2](https://www.esi.ac.at/preprints/esi333.pdf)
~~~

### v13 citation 384.2 (corrected)

Old

~~~text
[Transposition contents, §§3–6](https://www.esi.ac.at/preprints/esi333.pdf)
~~~

New

~~~text
[Transposition contents, Okounkov–Vershik, (2.1) and Proposition 6.2](https://www.esi.ac.at/preprints/esi333.pdf)
~~~

### v13 citation 48.5 (corrected)

Old

~~~text
[Frobenius, §2](https://faculty.fordham.edu/dswinarski/snchar/Frobenius1900.pdf)
~~~

New

~~~text
[Frobenius’s character formula, §2](https://faculty.fordham.edu/dswinarski/snchar/Frobenius1900.pdf)
~~~

### v13 citation 164.4 (corrected)

Old

~~~text
[Frobenius, §2](https://faculty.fordham.edu/dswinarski/snchar/Frobenius1900.pdf)
~~~

New

~~~text
[Frobenius’s character formula, §2](https://faculty.fordham.edu/dswinarski/snchar/Frobenius1900.pdf), [Cesi, transposition class-sum scalar, (4.1) and Proposition 4.1](https://arxiv.org/pdf/0902.0727)
~~~

### v13 citation 384.3 (corrected)

Old

~~~text
[Frobenius, §2](https://faculty.fordham.edu/dswinarski/snchar/Frobenius1900.pdf)
~~~

New

~~~text
[Frobenius’s character formula, §2](https://faculty.fordham.edu/dswinarski/snchar/Frobenius1900.pdf), [Cesi, transposition class-sum scalar, (4.1) and Proposition 4.1](https://arxiv.org/pdf/0902.0727)
~~~

### v13 citation 48.6 (corrected)

Old

~~~text
[Cesi, equation (4.2) and Proposition 5.3](https://arxiv.org/pdf/0902.0727)
~~~

New

~~~text
[Cesi, transposition class sum, (4.1) and Proposition 4.1, and cross-block spectrum, (4.2) and Theorem 5.3, (5.9)](https://arxiv.org/pdf/0902.0727)
~~~

### v13 citation 52.1 (corrected)

Old

~~~text
[Navrátil, Kamuntavičius and Barrett, eqs. (30), (35)](https://arxiv.org/pdf/nucl-th/9907054)
~~~

New

~~~text
[Navrátil, Kamuntavičius and Barrett, three-particle antisymmetrizer (30) and compressed matrix elements (35)](https://arxiv.org/pdf/nucl-th/9907054)
~~~

### v13 citation 54.1 (corrected)

Old

~~~text
[Navrátil, Kamuntavičius and Barrett, eqs. (30), (35)](https://arxiv.org/pdf/nucl-th/9907054)
~~~

New

~~~text
[Navrátil, Kamuntavičius and Barrett, three-particle antisymmetrizer (30) and compressed matrix elements (35)](https://arxiv.org/pdf/nucl-th/9907054)
~~~

### v13 citation 52.4 (corrected)

Old

~~~text
[Navrátil and Barrett, eqs. (15)–(18)](https://arxiv.org/pdf/nucl-th/9812062)
~~~

New

~~~text
[Navrátil and Barrett, four-particle case, (15) and the paragraph after (19)](https://arxiv.org/pdf/nucl-th/9812062)
~~~

### v13 citation 54.3 (corrected)

Old

~~~text
[Navrátil and Barrett, eqs. (15)–(18)](https://arxiv.org/pdf/nucl-th/9812062)
~~~

New

~~~text
[Navrátil and Barrett, four-particle case, (15) and the paragraph after (19)](https://arxiv.org/pdf/nucl-th/9812062)
~~~

### v13 citation 46.6 (removed)

Old

~~~text
, [Han, Lemma 2.2](https://arxiv.org/pdf/1103.3545)
~~~

New

Removed.

### v13 citation 359.4 (removed)

Old

~~~text
, [Han, Lemma 2.2](https://arxiv.org/pdf/1103.3545)
~~~

New

Removed.

### v13 citation 52.5 (removed)

Old

~~~text
, [Murphy, §3](https://doi.org/10.1016/0021-8693(81)90205-2)
~~~

New

Removed.

### v13 citation 382.1 (corrected)

Old

~~~text
[Exterior powers and exterior Pieri, §2](https://math.mit.edu/~apost/papers/LR.pdf)
~~~

New

~~~text
[Exterior powers as fundamental representations, §2](https://math.mit.edu/~apost/papers/LR.pdf)
~~~

### v13 citation 383.1 (corrected)

Old

~~~text
[Complete reducibility and highest weights, lectures 18 and 25–26](https://ocw.mit.edu/courses/18-745-lie-groups-and-lie-algebras-i-fall-2020/mit18_745_f20_lec_full.pdf)
~~~

New

~~~text
[Etingof, semisimple complete reducibility and highest-weight theory, lectures 18 and 25–26](https://ocw.mit.edu/courses/18-745-lie-groups-and-lie-algebras-i-fall-2020/mit18_745_f20_lec_full.pdf)
~~~

### v13 citation 385.1 (corrected)

Old

~~~text
[Permutation representations, §6](https://ir.cwi.nl/pub/10125/10125D.pdf)
~~~

New

~~~text
[Young permutation modules and dominance, Theorem 6.5 and §6.9](https://ir.cwi.nl/pub/10125/10125D.pdf), [Macdonald, dominance reversal in I.1, (1.11), and sign twist in I.7, Example 2](https://math.berkeley.edu/~corteel/MATH249/macdonald.pdf)
~~~

### v13 citation 7.3 (link updated)

Old

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/e02d05bc3d47e9ba1f2655dde2d96337/im2520_eng.pdf)
~~~

New

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf)
~~~

### v13 citation 46.4 (link updated)

Old

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/e02d05bc3d47e9ba1f2655dde2d96337/im2520_eng.pdf)
~~~

New

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf)
~~~

### v13 citation 359.5 (link updated)

Old

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/e02d05bc3d47e9ba1f2655dde2d96337/im2520_eng.pdf)
~~~

New

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf)
~~~

### v13 citation 370.4 (link updated)

Old

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/e02d05bc3d47e9ba1f2655dde2d96337/im2520_eng.pdf)
~~~

New

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf)
~~~

### v13 citation 383.3 (link updated)

Old

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/e02d05bc3d47e9ba1f2655dde2d96337/im2520_eng.pdf)
~~~

New

~~~text
[Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf)
~~~

### v13 citation 46.7 (link updated)

Old

~~~text
[Cartan component, Baur’s thesis, Proposition 3.2](https://imsc.uni-graz.at/baur/Articles/Diss.pdf)
~~~

New

~~~text
[Cartan component, Baur’s thesis, Proposition 3.2](https://edoc.unibas.ch/entities/publication/1af5150b-0f45-4b80-b0b4-843a4b08af55/full)
~~~

### v13 citation 359.6 (link updated)

Old

~~~text
[Cartan component, Baur’s thesis, Proposition 3.2](https://imsc.uni-graz.at/baur/Articles/Diss.pdf)
~~~

New

~~~text
[Cartan component, Baur’s thesis, Proposition 3.2](https://edoc.unibas.ch/entities/publication/1af5150b-0f45-4b80-b0b4-843a4b08af55/full)
~~~

### v13 citation 370.5 (link updated)

Old

~~~text
[Cartan component, Baur’s thesis, Proposition 3.2](https://imsc.uni-graz.at/baur/Articles/Diss.pdf)
~~~

New

~~~text
[Cartan component, Baur’s thesis, Proposition 3.2](https://edoc.unibas.ch/entities/publication/1af5150b-0f45-4b80-b0b4-843a4b08af55/full)
~~~

### v13 line 48

Old

~~~text
the squares of the two exterior transfer operators give the two height bounds on a column interaction.
~~~

New

~~~text
the transfer-square calculation in Proposition 3 gives the two height bounds on a column interaction.
~~~

### v13 line 52

Old

~~~text
Jucys’s factorization gives this one-column projector, and Murphy independently developed the branching construction.
~~~

New

~~~text
The one-column factor in Jucys’s factorization or Molev’s branching formula gives this projector.
~~~

### v13 line 54

Old

~~~text
On two exterior powers the two wedge–contraction transfers give the same smaller-height estimate for the entire pair.
~~~

New

~~~text
On two exterior powers, the transfer-square calculation in Proposition 3 gives the same smaller-height estimate for the entire pair.
~~~

### v13 line 56

Old

~~~text
The two transfer directions give both height bounds, and the shorter height counts common rows.
~~~

New

~~~text
The calculation in Proposition 3 gives a height bound in each transfer direction. The shorter height counts common rows.
~~~

### v13 line 164

Old

~~~text
[Permutation-module occurrence, §6](https://ir.cwi.nl/pub/10125/10125D.pdf)
~~~

New

~~~text
[Permutation-module occurrence, §6](https://ir.cwi.nl/pub/10125/10125D.pdf), [Macdonald, dominance reversal in I.1, (1.11), and sign twist in I.7, Example 2](https://math.berkeley.edu/~corteel/MATH249/macdonald.pdf)
~~~

### v13 line 180

Old

~~~text
It forms the full interaction \(X_{cc'}\) on two wedges and uses the positive transfer squares
~~~

New

~~~text
The calculation below relates the interaction \(X_{cc'}\) on two wedges to the positive transfer squares
~~~

### v13 line 280

Old

~~~text
The two exterior transfer squares give the two available height bounds for the same interaction.
~~~

New

~~~text
The transfer-square calculation in Proposition 3 gives the two height bounds for the same interaction.
~~~

### v13 line 311

Old

~~~text
The exterior interaction bound likewise controls the full sum
~~~

New

~~~text
The transfer-square calculation in Proposition 3 bounds the full sum
~~~

### v13 line 382

Old

~~~text
The alternating tensors of degree \(h_c\) identify isometrically with \(\bigwedge^{h_c}\mathbb C^n\) by normalized alternation.
~~~

New

~~~text
Normalized alternation identifies \(\bigwedge^{h_c}\mathbb C^n\) isometrically with the alternating tensors of degree \(h_c\). Each unit basis wedge maps to the signed sum of its \(h_c!\) tensor orderings divided by \(\sqrt{h_c!}\).
~~~

### v13 line 383

Old

~~~text
Finite-dimensional unitary representations decompose orthogonally into irreducibles.
~~~

New

~~~text
Taking invariant orthogonal complements gives an orthogonal decomposition of a finite-dimensional unitary representation into irreducibles.
~~~

### v13 line 386

Old

~~~text
Its squared norm form in each direction gives the corresponding height minus the interaction.
~~~

New

~~~text
The calculation in Proposition 3 identifies the squared norm form in each direction with the corresponding height times the identity minus the interaction.
~~~
