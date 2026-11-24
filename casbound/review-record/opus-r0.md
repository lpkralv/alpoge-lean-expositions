# Round 0 review: casBound_holds exposition (assembled-v11.md)

Reviewer: Opus, read-only. Sources checked: assembled-v11.md, units4.json, scope.json, supply.json, report.md, and the Lean files CasimirBounds/{CasBoundHolds,Expand,ReSwapSumLe,CountSame,CountCross}.lean, CoefficientGluing/{CoefGlueHolds,SumFinVal}.lean, TensorRelationsGL/ClozelCohomologicalOf.lean, KugaCoordinates/IsStarRep.lean. No web, so I could not check any cited paper.

## Verdict

The mathematics is sound. I re-derived every displayed computation and example: Props 1-9, the n=2 examples at lines 223, 309, 353 and 362, the antisymmetrizer remark at line 205, the dominance and Abel-summation argument at line 355, the height form of the coefficient at line 366, and the content and Young-module route at line 164. All of them are correct. I found no error that breaks the argument. The main gap concerns the result's role downstream, not its proof.

## Findings

**O1 (missing, insight gap), line 9.** The exposition never says that the consumer leaves zero slack. IsSmall (ClozelCohomologicalOf.lean:39-43) requires Re<v, C_Xi v> <= c|v|^2, where c is exactly pi's Casimir scalar at tau. In coefGlue_holds (CoefGlueHolds.lean:104, 144-150), c is the closed form of the infinitesimal weights, and SumFinVal.lean:111-114 (arith) shows that the tableau coefficient minus the twist term 2s|S|-ns^2 equals c identically. So a looser coefficient would not give IsSmall. That rules out the ambient nd+d(d-1), and it rules out bounding cross-column swaps one at a time. Decisions 2-6 (lines 62-68) are justified by "excess" without saying why no excess is affordable. Line 9 mentions the shift identities but not this consequence.

**O2 (unsupported), line 11.** "The classical exterior-transfer argument ..." The document's own literature section rates the source-column step as only a "partial precedent" (line 56) and calls the transfer approach "A second route" (line 48). As line 11 describes the citations, they supply ingredients: Levy's expansion, skew-Howe transfers (CKM Thm 4.2.1) and Howe's exterior action. None is said to contain the per-pair deficit proof of this bound. The fix is either to cite a source that carries out this argument or to present it as a reconstruction. The mathematics itself checks out: summing Prop 3 over the shorter column gives a deficit of sum_p |f-Y_p f|^2/(b+1), which is a sum of squared antisymmetrizer norms.

**O3 (overstatement), line 309.** "a direct count by tableau label would require the pointwise comparison". It does not. sum_filter_col_le_sum_ite_of_bound (CountCross.lean:28-57) uses only row sums (hcross) and collapses the right side to exactly N per row (isWH_coeff_one_polynomial, lines 13-26). The example correctly refutes the pointwise inequality. It does not show that a label count needs it. This agrees with the audit's item 3.

**O4 (overstatement), line 58.** "selecting whole columns ensures that each higher label charged to a box actually occurs in its column." Upward closure (IsTab, second clause) makes the higher label occur in the column. Whole-column selection only puts that box in S. count_up uses both: CountSame.lean:34 calls hT.2 and line 37 calls hS. Line 221 gets this right.

**O5 (overstatement), line 63.** Decision 2's reason holds only when some active column has height 2 or more. With d singleton columns, all labeled n-1, the coefficient is d(d+n-1) = nd+d(d-1), which equals the ambient symmetric maximum quoted at line 164. In that case alternation excludes nothing. This agrees with the audit's item 1, and the computation shows that the two numbers coincide.

**O6 (missing, local), line 164 (also line 48).** The content route stops one step short. Restricting to shapes mu dominated by lambda and doubling contents gives Gamma_n(mu), but bounding it by Gamma_n(lambda) needs Gamma_n (or the content sum) to be monotone under dominance. That step appears only at line 355, for the highest-weight route, and line 164 does not point to it.

## The earlier audit (report.md)

I checked its four items. Items 1 and 3 hold, and I report them as O5 and O3 with added evidence. Items 2 (line 280) and 4 (line 337) are also correct: Lean's cas_count and sum_filter_col_le_sum_ite_of_bound allow N < 0. But both sentences are labelled heuristics and follow text that says "For N>0" or fixes N = |f|^2 >= 0, so I did not list them separately. I did not recount the audit's tally table.

## Heart of the proof

| # | Idea | Conveyed | Where |
|---|---|---|---|
| 1 | Slot expansion K = nd Id + sum of ordered swaps. Within a column every term is exactly -|f|^2. | yes | Props 1-2; line 357 |
| 2 | One-box squared-defect identity: Y^2 f = s f-(s-1)Yf, so |f|^2-Re<f,Yf> = |f-Yf|^2/(s+1). A whole alternating column costs one |f|^2. | yes | lines 5, 7; Prop 3 |
| 3 | Nested terminal label intervals plus symmetry of R: charge each column pair from the contained column, giving min(h_c,h_c') = number of common labels. | yes | line 5; Props 7-8 |
| 4 | Per-box charge n - 2(n-1-b) + (m_b - 1) = m_b+2b+1-n, using upward closure and whole-column selection. | yes | Props 4, 5, 9 |
| 5 | The coefficient is Gamma_n(lambda) of the Cartan component, so the bound is sharp. | yes | lines 46, 366 |
| 6 | Downstream, the coefficient after the twist equals pi's Casimir scalar exactly (arith), and IsSmall needs that value. Sharpness is required, not merely convenient. | buried | line 9 |
