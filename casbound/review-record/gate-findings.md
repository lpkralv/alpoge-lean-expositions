Release-gate findings on assembled-v13.md (Claude check, PASS WITH FIXES, and a fresh quantifier audit, audit-v13.md):
1. Remove pipeline residue: concordance entries "Slice 1-x", "sole planner key result", "Absorbed statement in planner"; the "Decision 1-7" framing; the bold "**not traced**" (keep the information in plain words).
2. Note in the concordance that the Lean lemmas behind Props 6 and 7 (sum_sum_ite_col_ne_eq_sum_by_col, sum_filter_col_le_sum_ite_of_bound, CountCross.lean) are private.
3. Correct the ClozelCohomologicalOf.lean line range for the assembly theorem to 55-63 (51-53 is the Kuga definition).
4. Prop 7 remark "an empty target column forces N>=0": it holds only if some column other than gamma(p) has empty S_c; qualify it.
5. Label as "not in the Lean; checked by hand" the highest-weight proof, the sharpness remark ("nested highest wedges attain the bound") and the "terminal subcolumns" remark.
6. Soften contrasts such as "the proof here recovers ..." so they cannot read as priority claims; add near the top a line saying this is an exposition of a theorem in Levent Alpöge's 2026 Lean archive (alpo.ge/lean.tar.gz, published 2026-11-20).
7. Audit, line 11: each squared one-box defect needs the factor 1/(k+1), k the target column height (see audit-v13.md for the identity and the counterexample); fix the sentence.
8. Citations: apply the results of citation-check.md (correct, mark "not verified", or remove each pinpoint claim it could not confirm).
