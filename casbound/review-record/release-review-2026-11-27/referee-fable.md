# Referee report

**Manuscript.** L. P. Slothouber, "An automatically generated exposition of the Casimir bound casBound_holds in Alpöge's Lean proof of the Riemann hypothesis", 18 pp., 24 November 2026 (Zenodo 10.5281/zenodo.24514672, Hexagon 2611.01006).

**Recommendation.** Major revision. Reasons and venue in section 6.

**About this report.** The referee is an AI model (Claude Fable 5.2) that had no access to the logs or prompts of the process that produced the paper. So the paper's sentence "No human expert has read this document" (p. 16) is still true after this report. References are to PDF pages, with line numbers of paper.tex in square brackets. Each comment is marked essential, recommended or optional.

## 1. Summary

The paper explains one lemma of Alpöge's Lean archive, the theorem `PositivityTheory.Rg.Cz.casBound_holds`, and adds three short sections on how the text was generated and tested.

The statement, in my words. Take a finite set $Q$ of boxes. Each box sits in a column ($\gamma:Q\to C$) and carries a label $b(p)\in\{0,\dots,n-1\}$; within a column the labels are distinct and form an up-set, so a column of height $h$ carries exactly the labels $n-h,\dots,n-1$ and the data amount to the column heights $h_c\le n$. Let $S\subseteq Q$ be a union of whole columns, let $f\in(\mathbb C^n)^{\otimes Q}$ change sign when two tensor factors in the same column are swapped, and let $K=\sum_{i,j}G_{ij}G_{ji}$ with $G_{ij}=\sum_{p\in S}E^{(p)}_{ij}$ be the $\mathfrak{gl}_n$ Casimir acting on the factors in $S$. Then

$$\langle f,Kf\rangle\ \le\ \Big(\sum_{i=0}^{n-1}m_i(m_i+2i+1-n)\Big)\|f\|^2,\qquad m_i=\#\{p\in S:\ b(p)=i\}.$$

In classical terms $f$ lies in $\bigotimes_c\Lambda^{h_c}(\mathbb C^n)$ (times spectator factors), and the coefficient is the Casimir eigenvalue $\langle\lambda,\lambda+2\rho\rangle$ on the Cartan component $V_\lambda$, where the conjugate of $\lambda$ is the sorted list of heights. Equivalently the coefficient is $\sum_c h_c(n+1-h_c)+2\sum_{c<c'}\min(h_c,h_{c'})$ (p. 13).

The Lean proof is elementary and avoids highest-weight theory: (1) $K=nd+\sum_{p\ne q\in S}P_{pq}$ with $d=|S|$ (Props. 1 and 2); (2) swaps inside a column contribute exactly $-\|f\|^2$ each; (3) for a box $p$ outside a set $B$ on which $f$ alternates, $Y=\sum_{q\in B}P_{pq}$ satisfies $\|f\|^2-\mathrm{Re}\langle f,Yf\rangle=\|f-Yf\|^2/(|B|+1)\ge0$ (Prop. 3); (4) for two columns, apply (3) with $p$ running over the shorter column and $B$ the taller one, and use $P_{pq}=P_{qp}$ for the other order (Props. 6 to 8); (5) add up by label (Props. 4, 5, 9).

Role in the archive. The lemma has one caller. "Coefficient gluing" applies it with $S$ the set of boxes attached to one complex embedding $\tau$ and $f=Jv$, where $J$ embeds a finite-dimensional representation $\Xi$ isometrically into column-alternating tensors. After a shift by a determinant twist, the coefficient equals the Casimir scalar $c_\tau$ fixed by the infinitesimal character of the cuspidal representation $\pi$ (`SumFinVal.arith`), so the Casimir of $\Xi$ is at most $c_\tau$ (`IsSmall`). A Kuga-type identity then makes a Casimir-difference form nonpositive, which forces the cochain differential to vanish, and a nonzero cochain makes $\pi$ cohomological (`ClozelCohomological`: regular algebraic cuspidal representations of $GL_a$ over totally complex fields are cohomological). So the lemma lets the archive avoid computing the highest weight of $\Xi$, and it must hold with no slack. The paper says all of this, but only in the dense paragraphs on pp. 2-3.

## 2. Significance and novelty

**2.1 [essential] Say plainly that the inequality is classical.** The statement is the standard fact that the Casimir on a tensor product of fundamental representations is largest on the Cartan component. It follows from two textbook lemmas: every weight of $\bigotimes_c\Lambda^{h_c}$ is dominated by $\lambda$, and $\langle\mu,\mu+2\rho\rangle\le\langle\lambda,\lambda+2\rho\rangle$ for dominant $\mu\preceq\lambda$. The paper's own "highest-weight proof" (p. 13) is this argument. The abstract and introduction call the result "his existing theorem" and never say that the statement is classical; a reader learns it on p. 4, obliquely. What belongs to the archive is the choice of an elementary coordinate proof that needs none of this theory in Mathlib. The paper should say so in the abstract.

**2.2 Is it worth publishing, and for whom?** As a research article, no: the paper claims no new mathematics, and a representation theorist proves the lemma in a paragraph. As documentation it has real value for three groups: people reconstructing or auditing the archive (the paper reports that none of nine write-ups covers this module); formalisers who want a Mathlib-light proof of a Casimir bound; and people studying automated exposition, for whom this is a worked case with its process disclosed. The lemma is a good choice of target, because its role (a sharp bound standing in for a highest-weight computation) is interesting and not obvious from the Lean.

**2.3 Relation to the literature.** The literature section locates the right neighbours: the Casimir-transposition relation of Schur-Weyl duality (Lévy), the Jucys/Molev factorisation of antisymmetrisers, skew Howe duality (Howe; Cautis-Kamnitzer-Morrison), Cartan components (Baur). I fetched and read four cited locations and all four say what the paper uses them for: Lévy Prop. 2.2; Cautis-Kamnitzer-Morrison §4.2 and Lemma 4.2.3; Gleizer-Postnikov Prop. 2.1; Etingof §§18, 25, 26 (the Casimir scalar is Lemma 26.6, which would be the better locator). I could not read the Howe scan, and the arXiv listing of Yang shows no journal reference, so the Izv. Math. data of [13] are unconfirmed. The other citations are unchecked.

**2.4 [essential] Citations are attached to the wrong sentences.** Each paragraph ends with a cluster of citations fused to its last sentence, with no word on what each supports. Often that last sentence is about Alpöge's proof, so the paper appears to cite Lévy, Szőke or two nuclear-physics papers as sources for it (pp. 2, 3, 4, 5, 11). In one place the result is a false statement (item 3.2 below). The supplementary exposition.md has a descriptive label on every link ("Exterior Pieri", "Casimir normalization", "Transfer actions"); the conversion to LaTeX dropped the labels. Restore them: "for the exterior Pieri rule see [18, Prop. 2.1]".

**2.5 [recommended] Credit for the proof.** The About box says the tool explains "AI-generated Lean proofs", and three of the paper's own references ([3], [7], [9]) name Claude in their titles. The body attributes the theorem and proof to Alpöge alone throughout ("his existing theorem", "Alpöge's coordinate proof"). State once how the archive describes its own authorship, with a citation, and attribute accordingly.

**2.6 [recommended] Missing references a reader would expect.** Section numbers below are from memory and should be checked.
- J. E. Humphreys, *Introduction to Lie Algebras and Representation Theory*, GTM 9, Springer, 1972: §13.4, Lemma C, $(\mu+\delta,\mu+\delta)\le(\lambda+\delta,\lambda+\delta)$ for $\mu$ in the saturated set of $\lambda$, with equality only at $\mu=\lambda$. This is the lemma behind the highest-weight proof and gives its equality case.
- W. Fulton, *Young Tableaux*, LMS Student Texts 35, CUP, 1997, §8.1 (column-alternating tensors and exchange relations), and W. Fulton, J. Harris, *Representation Theory*, GTM 129, Springer, 1991, §6.1 and §25.1 (Weyl's construction; Casimir scalar). These are the standard sources for "tensors alternating in the columns of a diagram".
- A.-A. A. Jucys, Symmetric polynomials and the center of the symmetric group ring, Rep. Math. Phys. 5 (1974), 107-112; G. E. Murphy, A new construction of Young's seminormal representation of the symmetric groups, J. Algebra 69 (1981), 287-297. The operator $Y$ of Prop. 3 is a Jucys-Murphy element (item 3.6). The archive itself defines such elements (`xJ`, `KTypeData.lean:38-39`).
- R. Howe, Perspectives on invariant theory: Schur duality, multiplicity-free actions and beyond, The Schur Lectures (1992), Israel Math. Conf. Proc. 8 (1995), 1-182. Cautis-Kamnitzer-Morrison cite this together with [17] for skew Howe duality (their Theorem 4.2.1).
- For the application, which the paper describes without any source: L. Clozel, Motifs et formes automorphes, in *Automorphic Forms, Shimura Varieties, and L-functions* I, Perspect. Math. 10, Academic Press, 1990, 77-159 (regular algebraic implies cohomological, Lemme 3.14); A. Borel, N. Wallach, *Continuous Cohomology, Discrete Subgroups, and Representations of Reductive Groups*, 2nd ed., AMS, 2000, Ch. II (Kuga's formula).
- [optional] Replace the nuclear-physics references [27], [30] for the coset form of the antisymmetriser by a textbook, or drop them; the identity is three lines (the paper proves it on p. 9).

## 3. Correctness

**What I checked.** I read the five proof files and the statement file against the paper. All nine propositions and Theorem 10 match their Lean declarations in hypotheses, conclusion and proof route. All ten rows of the concordance have correct names and line ranges. The import closure is 975 lines in ten files, with no `sorry`, `admit` or `axiom` token, and the theorem has exactly one caller. I checked every file:line locator on pp. 2-3 (including `cas_shift`, `arith`, `IsSmall`, `kg_casDiff` and the K-type construction behind §2.2) and all are right, as are the signs of the twist correction $-2s|S|+ns^2$. Lean 4.33.1 and the 1,194-line closure of `typePrimesN` are right.

I redid by hand: Props. 1 to 9; $Y^2f=sf-(s-1)Yf$ and the squared-defect identity; the transfer-square computation $T^\dagger T=h_c-X_{cc'}$; the telescoping in the highest-weight proof; $\Gamma_n(\lambda)=\sum_i m_i(m_i+2i+1-n)$ under $\lambda_j=m_{n-j}$; the whole-column counterexample (pp. 9-10); the Prop. 8 example (p. 11); and every numerical illustration (6 versus 2; 12N versus 8N; and so on). All are correct.

Numerically, for 13 configurations with $n\le4$ (heights such as (2,1), (3,2,1), (2,2), with and without an unselected column) I built $K$ from the matrix units, restricted it to column-alternating tensors, and found the largest eigenvalue equal to the paper's coefficient in every case. So the theorem and its sharpness hold there.

**What I did not check.** I did not compile the Lean. I cannot confirm the claims about the coverage survey, the validation run, the counts in §3, or the community certification.

**I found no mathematical error.** The problems below are errors of attribution and labelling, and gaps.

Real errors:

**3.1 [essential] "Checked by hand" means checked by an AI model.** The label "not in the Lean; checked by hand" appears on pp. 2, 4, 10 and 13 [124, 271, 658, 933, 976]. Only p. 16 [1129-1131] says the check was done by an AI model. Next to an About box stating that no human checked the text, "by hand" misleads. Write "checked by an AI model, not in Lean" at each use.

**3.2 [essential] False attribution, p. 13 [943-945].** "Alpöge's coordinate proof follows [18, Proposition 2.1], [12, ...], [13, ...], [14, §2], [20, ...]." In exposition.md the sentence is "Alpöge's coordinate proof follows." and the links belong to the paragraph before it. As printed, the paper says the proof follows Gleizer-Postnikov and others. It does not.

**3.3 [essential] Unlabelled mathematics that is not in the Lean.** Section 5 says the highest-weight proof and two remarks are outside Lean. Three more pieces are, and none is labelled: the transfer-square computation, which sits inside the proof of Prop. 3 (p. 8 [552-559]) and is cited seven times in the paper as "the calculation in Proposition 3"; the content-formula route inside the proof of Prop. 2 (p. 8 [498-513]); and the pair-deficit identity on p. 3 [191-193]. The counterexamples and the equality statement on p. 9 [601] are also outside Lean. All are correct, but a reader who trusts the labels will take them as formally verified. Mark every mathematical claim as one of: in Lean (with declaration), not in Lean and AI-checked, or classical with a citation.

**3.4 [essential] Notation collisions that produce wrong readings.** The size of the target set is $k$ on pp. 2-4 [126-128, 192, 304] and $s$ in Prop. 3 [540 ff.], while the notation table defines $k$ as "length of a weight prefix" [420]. The letter $s$ is also the determinant twist [151, 168, 202]. The same correction is written $-2s|S|+ns^2$ on [151] and $-2s|S|+as^2$ on [168]. The column map is col on pp. 2-3 [136] and $\gamma$ from p. 4. $C_b$ [165] is a Casimir, though $C$ is the column set and $b$ the label map.

**3.5 [essential] The graders are not independent of the writer.** The abstract says "two independent AI graders". By §3 [1075-1078] the pipeline drafts with gpt-6.2-sol, and by §4 [1112] one of the two graders was gpt-6.2-sol. The graders may be independent of each other; one is the same model as the author. Say so, or regrade with models from outside the drafting pipeline.

Gaps and requests for detail:

**3.6 [recommended] Prop. 3, p. 9 [576-603].** Add two facts. First, $Y$ commutes with every swap inside $B$, so it preserves the tensors alternating on $B$. Second, the identity factors as $(Y-1)(Y+s)f=0$. Then $Y$ is a self-adjoint operator on that space with spectrum in $\{1,-s\}$, and $Y\le1$ is immediate. These are the two contents ($+1$ and $-s$) of the box added to a column of length $s$, which is why the constant does not grow with $s$.

**3.7 [recommended] Pair-deficit identity, p. 3 [191-193].** It is stated in the overview and never derived. One line suffices: sum the Prop. 3 identity over $p\in S_c$. The paper also implies, without saying it, that this equals $\|Tf\|^2$ for the exterior transfer $T$.

**3.8 [recommended] Transfer square, p. 8 [552-559].** Say that $A_i^\dagger$ is the Hilbert adjoint of $A_i$ only under the isometric identification of wedges with alternating tensors (stated six pages later, p. 14), and that $\sum_{p\in S_c}E^{(p)}_{ij}$ restricts to $A_i^\dagger A_j$ on the wedge.

**3.9 [recommended] Highest-weight proof, p. 13 [933-942].** Two sentences are missing: that $\mu$ is a weight of $\bigotimes_c\Lambda^{h_c}$, which is what the count of indices bounds; and why the order is reversed (the highest wedge of a column uses the labels $n-1,\dots,n-h_c$). Add the equality case: since $v_k-v_{k+1}\ge2>0$, equality forces $\mu=\lambda$.

**3.10 [optional] Unused hypotheses.** The Lean proof uses the tableau and alternation hypotheses only on boxes of $S$. The paper could say that they are stated on all of $Q$ for convenience.

## 4. Presentation, judged as an exposition

**Does a non-expert learn why the bound holds?** Not from the paper as written. The reason is present in three places: the first paragraph of §2.1, the Remark after Prop. 3 (p. 9), and the heights formula on p. 13. It is never assembled. One displayed identity would do it. Combining the paper's own formulas gives, for column-alternating $f$,

$$\Big(\sum_c h_c(n+1-h_c)+2\sum_{\{c,c'\}}\min(h_c,h_{c'})\Big)\|f\|^2-\langle f,Kf\rangle\ =\ 2\sum_{\{c,c'\}}\ \frac{1}{h_{\mathrm{tall}}+1}\sum_{p\in S_{\mathrm{short}}}\big\|f-Y_pf\big\|^2,$$

where $Y_p$ sums the swaps of $p$ with the taller column, and $(f-Y_pf)/(h_{\mathrm{tall}}+1)$ is the antisymmetrisation of $f$ over that column together with $p$. I verified this identity numerically in the 13 configurations of section 3. It shows the bound as a sum of squares, gives the equality case (every such antisymmetrisation vanishes), and makes Props. 4 to 9 visibly bookkeeping. **[essential]** State an identity of this kind as the main result of the exposition, with the Lean inequality as its corollary.

**4.1 [essential] Road map and order.** The order is: a six-line idea; a page of file:line trace through the callers; a 25-line paragraph on the K-type construction; the theorem as a block of quantified formulas, numbered 10 and placed before Proposition 1; a literature section that leans on "the calculation in Proposition 3" before Proposition 3 is stated; a list of design reasons; a notation table of about two pages; then the propositions. A reader meets the proof on p. 7. Suggested order: statement in words with a picture; the classical meaning and the role, five sentences each; the proof in one page around the identity above; remarks (why the naive estimates fail, the two counterexamples, the classical proofs); then appendices for the Lean concordance, the caller trace with file:line references, and the process.

**4.2 [essential] Proofs are mixed with commentary.** Almost every proof opens with what would go wrong under another approach and reaches the argument later. The proof of Prop. 2 starts with a "scalar background" that the theorem does not have. The proof of Prop. 3 starts on p. 8 and its argument begins on p. 9 [576], after Cauchy-Schwarz, the exterior transfer, a failed norm bound and a "Heuristic". The proof of Theorem 10 contains a second, different proof. Put the argument under "Proof" and the rest under "Remarks".

**4.3 [recommended] Prose compressed past the point of meaning.** Examples: "The strict cutoff $b(p)$ identifies the increasing ordering of each distinct same-column pair" (p. 9 [632]); "Proposition 3 squares the defect, since a large negative eigenvalue can rule out a norm contraction while helping the upper bound" (p. 5 [340]); "Coefficient by coefficient, the normalized quadratic has leading form $\mathrm{Id}-Y$ on $f$" (p. 9 [572]). The accounting words (charge, debit, cost, overcharge) are never defined. Section 2.2 uses "transferred quantum determinant factor", "spherical descent", "compact-fixed tensor", "Whittaker transfer" and "Young contraction" without definition.

**4.4 [recommended] No figure.** A paper about boxes, columns and labels has no picture. One diagram of bottom-aligned columns with labels $n-h_c,\dots,n-1$ and the row counts $m_i$ would replace most of the notation table.

**4.5 [recommended] Cut.** The edge cases $n=0$, $S=\varnothing$, $f=0$, $N\le0$ are discussed about ten times [265-267, 465-466, 519, 600-601, 660, 724-725, 792-793, 849-850, 917-919, 978-979]; one sentence is enough. The first seven "routine facts" (p. 14) are trivia. The notation table lists $\mathbb R$, $\mathbb C$, Re, Id and three kets used once. With these cuts and the reordering, the mathematics fits in about eight pages.

**4.6 Abstract and introduction. [essential]** The abstract does not state the inequality or say that it is classical, and gives a third of its length to a grading exercise on a different theorem. The introduction gives the lemma's Lean name before saying what it asserts.

**4.7 Statements about formal verification.** **[essential]** "The Lean community certified the archive's statement and proof on 21 November 2026" (p. 1 [87-88]) has no source of its own; the only citations in that paragraph are Alpöge's own archive and remark [1, 2]. Give an independent source and say what was certified, by whom and with what tool; otherwise write "claimed". The title has the same dependence. **[recommended]** Replace the token scan with the output of `#print axioms casBound_holds` and the Mathlib revision. Of the 975 lines, 466 are the five proof files; the rest are definitions pulled in by imports.

**4.8 Statements about AI generation.** The About box is clear, complete and well placed, and §5 is candid. Three problems remain. **[essential]** The sole listed author states that he neither wrote nor checked the text. Most journals require authors to take responsibility for the content, so for journal publication the author must check the mathematics or have a named expert do it. **[recommended]** The counts in §3 (22 findings, 12 hand computations, 31 of about 50 citations corrected) have no pointer to evidence; give the repository commit and file paths. The 31-of-50 figure is itself a reason for a human pass over the bibliography. **[recommended]** §4 tests one theorem, with an AI-extracted key and AI graders; it supports the pipeline weakly and this paper's text not at all. Keep it in the body and take it out of the abstract.

## 5. Specific comments

1. p. 1, title [46-48]. **[recommended]** Use the running head's form, "in Alpöge's Lean archive", unless the certification is sourced (4.7).
2. p. 1 [91, 99] and p. 16 [1110]. **[optional]** Citations placed after the full stop.
3. p. 1 [93-99]. **[recommended]** The novelty claim rests on nine write-ups; references [3]-[11] carry no dates, [8] has no author and [11] is a home page. Give versions and access dates.
4. p. 2 [109-112]. **[optional]** The unnumbered line "The tableau Casimir bound." and its sentence repeat the introduction.
5. p. 2 [124-132]. **[essential]** The paragraph opens with "The highest-weight proof" before the reader has a statement. Its closing citations (Casimir eigenvalue sources) hang on a sentence about the coordinate proof. See 2.4.
6. p. 2 [134-142]. **[recommended]** "each with decidable equality" is a Lean detail; "zero-background" is undefined here and explained only on p. 7.
7. pp. 2-3 [144-186]. **[essential]** Move to an appendix and replace with a plain account of the role (my section 1 gives one reading). The key sentence, that any slack "would survive the twist and leave the estimate too weak" [172-174], deserves to be the lead.
8. p. 3 [188-196]. **[essential]** $X_{cc'}$ is used before it is defined. The text says the deficit is a transfer "out of the shorter column", but the formula holds for any source column; the shorter one gives the better bound.
9. p. 4 [239-261]. **[recommended]** State the theorem in prose, by column heights, and give the quantified form in the appendix. Number it before the propositions or call it the Main Theorem.
10. p. 4 [256]. **[optional]** $K$ is self-adjoint, so $\langle f,Kf\rangle$ is real; "Re" mirrors the Lean statement. Say so once.
11. p. 4 [290] and p. 8 [507-508]. **[recommended]** "The dominance comparison in Theorem 10" refers to the highest-weight paragraph inside the proof, not to the theorem.
12. p. 4 [304]. **[essential]** "dividing the defect by $k+1$": should be $s+1$ (3.4).
13. p. 5 [317-321]. **[optional]** "The shorter height counts common rows": say "common labels", as elsewhere.
14. p. 5 [340-341]. **[recommended]** I read this bullet as: $\|Yf\|\le\|f\|$ is false because $Y$ has the eigenvalue $-s$, but a negative eigenvalue only helps an upper bound on $\langle f,Yf\rangle$, so one bounds the form, not the norm. Write that.
15. pp. 5-7 [352-427]. **[recommended]** Shorten the table; fix $k$ and $s$; either add the symbols of §§2.1-2.2 ($a$, the twist $s$, $l_\tau$, $\nu_\tau$, $w_\tau$, $J$, $c_\tau$) or move those sections out. The entry for $X_{cc'}$ says "in their exterior-power realization", yet p. 3 applies it to tensors.
16. p. 7 [459-460]. **[optional]** The last sentence of the proof of Prop. 1 is not needed.
17. pp. 7-8 [484-488, 498-513]. **[essential]** First and third paragraphs of the proof of Prop. 2 are not part of the proof. The third is not in Lean (3.3).
18. p. 8 [495-496]. **[optional]** "at $n=1$ the diagonal swap alone happens to give the right scalar": cut.
19. p. 8 [552-559]. **[essential]** Give the transfer square its own numbered statement, labelled as outside Lean (3.3, 3.8).
20. p. 9 [569-574]. **[recommended]** Cut the "Heuristic" or rewrite it.
21. p. 9 [583-586]. **[optional]** The case $p\in B$ is a digression.
22. p. 9 [606-612]. **[recommended]** This Remark is the reason the proposition is true. Move it into the main text, before the computation.
23. p. 9 [632-635]. **[recommended]** Delete the first paragraph of the proof of Prop. 4; the proof is the second.
24. pp. 9-10 [644-653]. **[recommended]** The counterexample is correct and well chosen. The three citations at its end support nothing in it.
25. p. 10 [670]. **[optional]** Prop. 5 assumes the full tableau condition but uses only injectivity; the Remark says so. Fine as a match to Lean.
26. pp. 10-11 [751-764, 781-783]. **[recommended]** Two motivational paragraphs precede the proof of Prop. 7, and the case $N<0$ never occurs in the application.
27. p. 11 [820-829]. **[recommended]** The example is correct: both expectations are 1/2 and $Yf=f$. Say that it is an equality case of Prop. 3.
28. p. 12 [839-844]. **[optional]** This paragraph is a second proof sketch; label it.
29. p. 12 [883-889]. **[optional]** The paragraph on "scales" can go.
30. p. 13 [925-967]. **[essential]** Separate the highest-weight proof from the proof of Theorem 10 (4.2), and fix 3.2.
31. p. 13 [969-981]. **[recommended]** Promote the heights formula to the theorem statement.
32. p. 14 [1012-1013]. **[optional]** Cite Etingof's Lemma 26.6 for the Casimir scalar.
33. pp. 14-15 [1030-1061]. **[recommended]** The concordance omits the auxiliary lemmas of the closure: `count_same` (CountSame.lean:71-88), `count_rhs` (11-20), `dot_pm_swap` (ReSwapSumLe.lean:18-27), `isWH_coeff_one_polynomial` (CountCross.lean:13-26), `eAt_applyC`, `tE_zero_apply`, `sum4`. Each corresponds to a "routine fact"; list them. One row of the table is stranded on p. 14.
34. p. 16 [1112-1113]. **[essential]** See 3.5.
35. p. 16 [1101-1119]. **[recommended]** Say whether the `typePrimesN` exposition, the key and the grades are public, and where.
36. pp. 16-18, bibliography. **[recommended]** Give DOIs or MR numbers. [14] links to a session-specific mathnet.ru address that will break. [31] links to a course-hosted copy of Macdonald's book, and [17], [24], [29] to third-party copies; remove these links. [19] has no locator. [26] is an unrefereed ResearchGate upload; cite a standard source for the same fact or drop it. Confirm the journal data of [13]. [22]: "Grassmann".

## 6. Recommendation

**Major revision.**

The mathematics is correct and the match to the Lean is exact in everything I checked. The paper is honest about how it was made. It does not yet do its stated job. The idea that makes the bound obvious is split across three places and never displayed; proofs are buried under commentary; the overview is a file:line trace; notation collides; the provenance labels ("checked by hand", "independent") say something other than what happened; and citations hang on sentences they do not support, once to the point of a false statement. None of this needs new mathematics. It needs reordering, cutting to about half the length, relabelling, and a human who takes responsibility for the result.

Essential for any further publication: 2.1, 2.4, 3.1 to 3.5, the displayed identity and 4.1, 4.2, 4.6, 4.7 (certification source), 4.8 (author responsibility).

Venue. It is not a fit for a research journal, which would want new mathematics, nor for a general expository journal, which would want more than one classical lemma. As a preprint or technical report on Zenodo and Hexagon it is in the right place already, once the essential corrections are made. After a human-checked rewrite, the mathematical part would suit a venue for formalised mathematics (Annals of Formalized Mathematics, or a short paper at CICM or ITP), or better, a section of one of the community reconstructions of the archive, which per the paper's survey lack this module. (Venue names are from memory.) The pipeline is a separate contribution; with an evaluation on more than one theorem and graders outside the drafting models, it would suit AITP or a similar workshop.
