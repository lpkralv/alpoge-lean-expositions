# Referee report

Manuscript: "An automatically generated exposition of the Casimir bound casBound_holds in Alpöge's Lean proof of the Riemann hypothesis", version 2, 25 pages (paper.pdf, built 27 November 2026).

Report date: 27 November 2026. The referee is an AI model (Claude Fable 5.2). I saw no earlier review of this paper and no record of how it was made. By the paper's own caveat in Section 10 (AI reviewers may share blind spots), this report is not the independent human check that the paper lacks.

Comments are marked [essential], [recommended] or [optional]. Page numbers refer to the PDF.

## What I checked, and what I did not

- I read the whole PDF and its LaTeX source.
- Sections 2 to 5: I checked every proof and every number by hand. That covers the Observation, Figure 1, the running example, Propositions 1 to 11, Theorems A and B, the three comparisons in Section 4 and the variant in Section 4.3.
- Numerically, with random column-alternating tensors in ten configurations (rank at most 4, at most five boxes, two of them with an unselected column): Theorem B(a), the identity of Theorem B(b), sharpness, and the two equality statements (Theorem B(c) and Section 5.1). All agree. In every case the top eigenspace of K on the admissible tensors equals the set where every Y_p f = f, and its dimension is that of the expected Schur module.
- Against the Lean: the statement of Theorem A and Propositions 1 to 9 against the five proof files, KTypeData.lean and StepFormula.lean. Every line range in Tables 1 and 2 is right. In Table 3 I checked every location except those in KugaGlueHolds.lean, KugaAbsHolds.lean and CochainHolds.lean; the ones I checked are right.
- I recomputed the import closure: ten files, 975 lines, 466 in the five proof files. A text search finds no sorry, admit or axiom in them. The toolchain file says Lean 4.33.1 and the manifest pins Mathlib at 0df444a3. The SHA-256 of part 01 in reference [1] matches the retained checksum file.
- I did not recompile anything and did not run #print axioms. The supplied tree has no built Mathlib.
- Citations: I compared the pinpoint citations to ten sources with the sources themselves, fetched today: the joint statement [3]; both quotations from Alpöge's remark [2] and its footnote with the download locations; Lévy, Proposition 2.2 (arXiv v2); Molev, Section 2, (7) to (9); Yang, Example 5.4; Cesi, (4.1) and Proposition 4.1; Cautis, Kamnitzer and Morrison, Lemma 4.2.3; Gross and Taylor, (2.1) and (2.2); Gleizer and Postnikov, Proposition 2.1; Hazewinkel and Martin, 6.5, 6.9 and 6.10. All ten say what the paper says they say. Humphreys 13.4, Macdonald (1.11) and Clozel's Lemme 3.14 I know from memory only. I did not check Baur, Baur's thesis, Fulton 8.1 (4), Fulton and Harris, either Jucys paper, Murphy, either set of Etingof notes, Perelomov and Popov, Gross's Appendix A.1, either Howe reference, Okounkov and Vershik, Hazewinkel and Vorst, Borel and Wallach, or the nine write-ups [4] to [12].

## 1. Summary

The paper explains one lemma of Alpöge's Lean archive and the 466 lines of Lean that prove it.

The statement. Take a finite set Q of boxes, a map sending each box to its column, a label on each box from {0, ..., n-1}, and a set S of selected boxes that is a union of whole columns. The tableau condition says that labels within a column are distinct and closed upward, so a column of height h carries exactly the labels n-h, ..., n-1. Let f be a tensor in the product of copies of C^n indexed by Q that changes sign under every swap of two boxes in one column, and let K be the quadratic Casimir of gl_n acting on the factors in S. With m_i the number of selected boxes of label i, Theorem A says

    Re <f, K f>  <=  ( sum_i m_i (m_i + 2i + 1 - n) ) ||f||^2 .

Read by column heights h_c (Theorem B(a)), the coefficient is sum_c h_c(n+1-h_c) + 2 sum over pairs of min(h_c, h_c'). This is the value of the Casimir on the irreducible representation whose highest weight is the conjugate of the column heights. So the lemma is the classical fact that on a tensor product of exterior powers of C^n the Casimir is largest on the Cartan component.

The proof in the archive uses no highest-weight theory. The Casimir is nd plus the sum of all swaps of two selected boxes (Proposition 2). A swap inside a column contributes -||f||^2. For one box p and an alternating set B of s boxes not containing p, with Y the sum of the s swaps of p into B, one has ||f||^2 - Re<f, Yf> = ||f - Yf||^2/(s+1), because (f - Yf)/(s+1) is the antisymmetrization of f over B together with p (Proposition 3). Applying this from each box of the shorter of two columns bounds the swaps between them by min(h_c, h_c')||f||^2 per order. The Lean does the bookkeeping by labels (Propositions 4 to 9).

The paper adds, outside the Lean: the heights form, an exact formula for the deficit as a sum of squares, and the equality case (Theorem B); a section on why cruder estimates fail; three classical proofs (dominance of weights, exterior transfer operators, contents and Young's rule); and an account of the lemma's single use. That use is in the archive's proof that regular algebraic cuspidal representations of GL_n over a totally complex field are cohomological (Clozel's Lemme 3.14). After a twist, the bound says that the Casimir of a coefficient representation is at most the Casimir scalar fixed by the infinitesimal character of the automorphic representation, with no slack, which is what the Kuga argument needs. Sections 7 to 10 give a concordance with the Lean, the history of the automated production, a test of the method on a different theorem, and limitations.

## 2. Significance and novelty

There is no new mathematics here and the paper does not claim any. The inequality is classical, the one-box identity is the positivity of an antisymmetrizer (Jucys, Murphy), and the pair bound is the positivity of T†T for a skew Howe transfer. Theorem B(b) is a tidy way to write the deficit and I expect it is folklore (see comment 31).

Is the exposition worth publishing? For people auditing the archive, yes. The Lean statement is written in a label encoding that hides its meaning. The useful result of this paper is a recognition: this node of the formal proof is a known theorem, the constant is sharp, and here is the equality case. An auditor wants exactly that, and I confirmed it is right. For people interested in machine-written exposition it is a documented case with unusually candid provenance. As a mathematics article for a research journal it is out of scope.

Two limits on what the case shows. First, this lemma is one of the easiest kinds of node to explain: finite-dimensional, elementary, and classical. It shows the method can recognise a classical statement; it does not show the method can explain a node with no classical counterpart. Second, the paper spends 25 pages and about 14,600 words on an argument whose core fits on page 2.

Credits. On the sample I checked, the credits are accurate. The archive's proof is credited to the archive, the classical fact to the literature, and the paper says which calculations are its own. One sentence overreaches: "the archive's coordinate proof does not follow any of the sources cited here" (p. 13). Nobody can know what an AI-assisted proof followed. Say that the proof was not found in the sources cited. [recommended]

The choice of sources is odd in places. Textbook facts are cited to research papers that happen to contain them: Yang (2023) for the gl_n Casimir, Cesi (2010) for the content sum, Gleizer and Postnikov for Pieri's rule, Gross and Taylor for the row and column formula, Hazewinkel and Martin for Young's rule, Baur for the Cartan component. The pinpoints are right, but a specialist will find the list strange. Add standard references next to them. [recommended]

References a reader would expect:

- For "the Casimir picks out the Cartan component": W. Lichtenstein, A system of quadrics describing the orbit of the highest weight vector, Proc. Amer. Math. Soc. 84 (1982), 605-608. This is the classical use of exactly this fact and is closer to the point than Baur.
- For Theorem B(c) and Proposition 11: K. Akin, D. Buchsbaum and J. Weyman, Schur functors and Schur complexes, Adv. Math. 44 (1982), 207-278, and J. Weyman, Cohomology of Vector Bundles and Syzygies, Cambridge Tracts 149 (2003), Section 2.1. They present Schur functors by the maps that move one vector between adjacent exterior powers, which are the paper's transfers. J. Towber, Two new functors from modules to algebras, J. Algebra 47 (1977), 80-104, for the exchange relations.
- One textbook covering Schur-Weyl duality, skew (GL_n, GL_k) duality and Casimir values: R. Goodman and N. Wallach, Symmetry, Representations, and Invariants, GTM 255, Springer 2009 (from memory; I did not look up section numbers).
- For the relation between the Casimirs of a dual pair on fermionic Fock space: D. Rowe, M. Carvalho and J. Repka, Dual pairing of symmetry and dynamical groups in physics, Rev. Mod. Phys. 84 (2012), 711-757 (from memory).
- For Section 6: Y. Matsushima and S. Murakami, On vector bundle valued harmonic forms and automorphic forms on symmetric Riemannian manifolds, Ann. of Math. 78 (1963), 365-416 (the source of the Casimir formula for the Laplacian); T. Enright, Relative Lie algebra cohomology and unitary representations of complex Lie groups, Duke Math. J. 46 (1979), 513-525 (the complex-group case, which is the totally complex field case here); D. Vogan and G. Zuckerman, Unitary representations with nonzero cohomology, Compositio Math. 53 (1984), 51-90. Also a proper entry for Grobner and Raghuram (comment 33).
- For the formal side: L. de Moura and S. Ullrich, The Lean 4 theorem prover and programming language, CADE-28 (2021); The mathlib Community, The Lean mathematical library, CPP 2020.
- For the method: the paper cites no prior work on turning formal proofs into prose. At least the Mizar tradition (the journal Formalized Mathematics has published machine-translated articles since 1990) and Y. Coscoy, G. Kahn and L. Théry, Extracting text from proofs, TLCA 1995, belong here, along with recent work on informalization with language models. (Details from memory.)

## 3. Correctness

I found no mathematical error. Theorem A matches the Lean statement CasBound. Propositions 1 to 9 match their Lean lemmas in hypotheses and conclusion, and the proofs given follow the Lean proofs step for step. Everything the paper marks "not in the Lean; checked by an AI model" that I checked is correct: the derivation of (1), the Observation, Figure 1, the running example, the projector formula, all Remarks, Theorem B, Section 4, Propositions 10 and 11, sharpness and the equality statement. The account in Section 6.1 of how the theorem is called (CoefGlueHolds.lean, line 144), of the twist identity and of the identity arith is accurate.

Real inaccuracies, all small:

- p. 1, notice. See comment 1. As written it is unclear whether a human checked version 2.
- p. 4, paragraph after the proof of the Observation. Macdonald I (1.11) is cited for "the m_i form the partition conjugate to the sorted heights". From memory, (1.11) is the statement that conjugation reverses dominance, which is how the paper itself uses it on p. 16; the conjugate partition is defined at (1.3). Please check. [recommended]
- p. 7, "It proves the same identity by multiplying swaps". The Lean theorem re_swapSum_le' states the inequality only. The identity (2) exists as intermediate steps (hgg and hfg, lines 65-68 and 80-81) and is not a Lean declaration. Since (3) and Theorem B(b) rest on the identity, say so here. [recommended]
- p. 14, top. Yang's Example 5.4 displays the projection as sum E_ii^2 + sum_{i<j} (E_ii - E_jj). The paper's form with (n+1-2i)E_ii is an equivalent rewriting. Say "equivalently". [optional]
- p. 2, Section 1.2. The second quotation stops mid-clause. The source reads "Claude and I have also formalized the arguments without assumptions." Mark the cut or quote the clause. [optional]
- p. 16. Grobner and Raghuram are cited by a link to a PDF on a home page and have no bibliography entry. See comment 33.
- p. 23. "AI reviewers checked them in the review of version 2." See comment 40.

Gaps and requests for detail:

- The link to the Riemann hypothesis. The title places the lemma "in Alpöge's Lean proof of the Riemann hypothesis". Section 1.2 says the certification concerns ordinary RH. Nowhere does the paper show that the theorem riemannHypothesis in Main.lean depends on casBound_holds. Table 3 stops at ClozelCohomological. I checked two things. The module CasBoundHolds is in the import closure of Main.lean, but so is nearly every module of the archive, so that shows little. And the theorem clozelCohomological is consumed at three places: ClozelCohC.lean line 24, and as the "literature" instances at EveryCharacterOfLiteratureOfVWin.lean line 328 and TemperedProductOfSquareIntegrable.lean line 278; the first of these two feeds regularAlgebraicPurity_of_clozel at line 494 of the same file. The pipeline already extracts dependency graphs. Use it to state whether riemannHypothesis depends on casBound_holds at the level of terms, add the consumers to Table 3, and give one sentence on what purity is used for. If the dependence cannot be shown, change the title. [essential]
- p. 13, Section 4.3, "A variant would survive". This is asserted, and Section 10 reports a numerical check and a paper argument that the reader does not see. It follows from Theorem A in three lines: move each unselected box to a new column of its own and give it the label n-1. The tableau condition, whole-column selection and the alternation hypothesis then hold for the new data, and K and the m_i are unchanged. Put that in. [recommended]
- p. 12, Section 3.6, part (b): "By the proof of Theorem A and Proposition 6". The displayed formula for Re<f, Kf> needs only Proposition 2, the alternation and the partition into columns. State it as a lemma with that proof. [recommended]
- p. 3, lines 2 to 5. The compile and axiom check is reported at second hand. Put a script in the repository that reproduces it, and give all fourteen checksums (reference [1] gives one of fourteen). [recommended]

## 4. Presentation, judged as an exposition

Does a non-expert come away knowing why the bound holds? Yes, from page 2 and Section 3.2. The paragraph beginning "The coordinate proof has one idea" is the best in the paper, and the projector explanation before Proposition 3 gives the reason for the identity instead of only verifying it. Section 4 is useful and short. There is a road map (end of Section 1.3, start of Section 3). After page 8 the key idea gets buried.

The main structural problem [recommended]. Theorem B(a) and (b) together prove Theorem A, and their proof needs only the Observation, Proposition 2, Proposition 3 and the partition into columns: under a page. Propositions 4 to 9 are how the Lean reaches the same count without ever mentioning heights, through an abstract kernel R and a number N. The paper presents these four pages as the proof and then derives Theorem B "from the steps of the Lean proof", which leaves the reader thinking the label machinery is needed. Make the heights argument the main line. Then present Propositions 4 to 9, more briefly, as the Lean's route, and say in a sentence why a formal proof would prefer labels (no case split on which column is shorter, no sorting).

The running example hides the inequality [recommended]. At n = 2 with heights 2 and 1 the admissible space is two-dimensional and irreducible, so every admissible tensor attains the bound (my numerical check confirms this). The example never shows a nonzero deficit. The text says f "turns out to attain the bound"; in fact it has no choice. Use an example with slack. The two one-box columns of Section 4.1 would do: for antisymmetric f, Yf = -f, and Theorem B(b) gives the deficit 2 * (1/2) * ||2f||^2 = 4||f||^2 = (6 - 2)||f||^2. Or n = 3 with heights 2 and 1, where the fully antisymmetric tensor gives 3 against the bound 9. It would also help to use the tensor attached to the labels: the column antisymmetrization of the basis tensor at the assignment x = b is the product of highest wedges, so it is an equality case. That one sentence explains why the labels live in the same set as the coordinates, which the text otherwise only warns against confusing.

What the paper does not say and should [recommended]:

- The equality condition Y_p f = f of Theorem B(c) is the one-box exchange (Garnir, Plücker) relation between a column and a box of a shorter column. The paper cites Fulton 8.1 for exchange relations on p. 13 and never connects them to Theorem B(c). The connection explains why the two equality statements (Theorem B(c) and Section 5.1) agree.
- Why the archive proves a classical fact in coordinates. Presumably because Mathlib has no highest-weight theory for gl_n to call on. Say so, marked as interpretation.
- What the tableau of Section 6.2 is. See comment 34.

Length and what to cut [recommended]. Sections 7 to 10 take about six and a half pages. Section 8.2 is a changelog of version 1's defects. Section 9 tests the pipeline on another theorem and says itself that it "is not evidence about the present text". Move both to the repository or an appendix, with the three tables. Keep half a page on provenance and checks. Version-history remarks are also scattered through the mathematics ("It is Theorem 10 of version 1", p. 5; "keep their numbers from version 1", p. 6; "added in version 2", p. 4; "Version 1 called the extra term a background", p. 5). A reader of version 2 does not need them.

The provenance tag. "Not in the Lean; checked by an AI model" appears 22 times, in the abstract, in theorem headings and in the names of three environments. The separation it marks is right and worth keeping. Replace the phrase by a symbol defined once in Section 1.3. The phrase "checked by an AI model" has no settled meaning for a reader; Section 10 says what was checked, and that is where the reader should be sent. [recommended]

Abstract and introduction. The abstract is long, carries the tag, and ends with two sentences that point to "(1)" and "Theorems A and B(a)". An abstract must stand alone. The phrase "The bound (not in the Lean; ...) is" will puzzle a first reader of a paper about a Lean theorem. Say instead that the Lean theorem is stated by labels and is equivalent to the displayed bound by a relabelling given in the paper. [recommended] The derivation paragraph after (1) on p. 2 refers to labels, the tableau condition and two theorems before any of them is defined. Make it a corollary after Theorem B. [recommended]

Statements about formal verification. Careful and well placed in Section 1.2. I confirmed that the joint statement says what the paper reports. The missing piece is the dependence of RH on this lemma (Section 3 above).

Statements about automated generation. The boxed notice on page 1 is clear, prominent and the right idea. Two problems. It says no human wrote, edited or checked the text of version 1, and then only that an AI model drafted version 2; the reader will infer that a human checked version 2. If none did, say so in the same words [essential]. And the paper has a human author and a statement that no human vouches for the text. For any refereed venue the notice must say who answers for the content [essential]; see Section 6.

Section 6.2. The first two paragraphs are clear and I checked them against PKTypeA.lean. The third ("The embedding J is constructed last ...") cannot be followed: it strings together names for steps the paper does not explain. Cut it to two sentences on what J is and what it supplies. [recommended]

## 5. Specific comments

1. p. 1, notice. State whether any human read, edited or checked version 2. [essential]
2. p. 1, author line and notice. State who is accountable for the correctness of the text. [essential]
3. p. 1, abstract. Remove the tag and the cross-references; shorten. [recommended]
4. p. 1, title. Consider "The tableau Casimir bound in Alpöge's Lean archive: an automatically generated exposition", subject to comment 9. [optional]
5. p. 1, subject classification. 11M26 does not describe the content. 68V20 (formalization of mathematics) fits better than 68V15; consider 20C30. [optional]
6. p. 2, paragraph after (1). Move after Theorem B as a corollary. [recommended]
7. p. 2, "[13, Section 1, p. 309]". Placed so that Baur seems to give the coefficient. Baur gives the definition of the Cartan component; the value is computed in Section 5.1. [optional]
8. p. 2, Section 1.2. Truncated quotation. [optional]
9. pp. 2-3 and 16-17. Show the term-level dependence of riemannHypothesis on casBound_holds, or change the title. Add the three consumers of clozelCohomological to Table 3. [essential]
10. p. 3, lines 2-5, and p. 23, reference [1]. Reproduction script; all fourteen checksums. [recommended]
11. p. 3, survey paragraph. "One bookkeeping result" is unnamed. Name it or drop the sentence. [optional]
12. p. 4. Macdonald (1.11) is probably the wrong pinpoint here; (1.3) defines the conjugate. [recommended]
13. p. 4, Figure 1. Say in the caption that the rows, read upward from the bottom, are the partition (4,3,1) and that its conjugate (3,2,2,1) is the list of heights. [optional]
14. p. 5 and p. 7. "Background" is introduced as version 1's word and then used in the Remarks on p. 7 as current terminology. Define it or drop it. [optional]
15. pp. 4, 5, 6, 18. Collect the version-history remarks in one place. [recommended]
16. p. 5 and p. 12. Make Theorem B(a), (b) the main proof of Theorem A. [recommended]
17. p. 6. Replace or supplement the running example with one that has slack. [recommended]
18. pp. 6-11. Each of nine propositions repeats "For every n, finite set Q, set C, ..." in a display. State the standing data once. [optional]
19. p. 7, second paragraph of Section 3.2, and p. 15. "Murphy's ... is a background reference" and "Howe's 1995 chapter is a background reference" read as padding. Say what each is cited for or remove it. [optional]
20. p. 7. "It proves the same identity": the identity is an internal step of the Lean proof. [recommended]
21. p. 7, Remarks after Proposition 2. The n = 1 example with (1+z)^2 teaches nothing. Cut. [optional]
22. p. 8, Remark (4). Cut. [optional]
23. p. 10 (after Proposition 7 and in Remark (1)) and p. 11 (after Proposition 9). That the statements hold for real N of either sign is said three times. It is an artifact of the Lean statement, since N = ||f||^2 in the only use. Once is enough. [optional]
24. p. 12, part (b). State the formula for Re<f, Kf> by columns as a lemma. [recommended]
25. p. 12, (3) and Theorem B(c). Name the exchange relation and cite Akin, Buchsbaum and Weyman. [recommended]
26. p. 13, Section 4.3. Give the three-line reduction of the variant to Theorem A. [recommended]
27. p. 13, first paragraph of Section 5. "Does not follow any of the sources": reword. [recommended]
28. p. 13, Section 5.1. Two sentences reprove complete reducibility of a unitary representation. Cite and move on. [optional]
29. p. 14. Yang: "equivalently". [optional]
30. pp. 14-15. Add textbook references beside Gleizer and Postnikov, Baur, Cesi, Hazewinkel and Martin. For the content sum, Macdonald I.7, Example 7 (from memory). [recommended]
31. p. 15, Proposition 11. The clean statement behind Theorem B(b) is a duality of Casimirs. On the exterior algebra of C^n tensor C^m in degree d, with gl_m acting on the column index, the two Casimirs add up to (n+m)d. On the weight space with column heights h_a, the gl_m Casimir equals sum h_a^2 + sum over pairs |h_a - h_b| + 2 sum over pairs T†T, where T is the transfer from the shorter column of the pair into the taller. Subtracting gives Theorem B(b) with deficit 2 sum ||Tf||^2, and the constant comes out as in Theorem B(a). I checked this by hand; the authors should verify it. One sentence of this kind would let a representation theorist see the whole theorem at once. [recommended]
32. p. 15. "use Cautis-Kamnitzer-Morrison": "see". [optional]
33. p. 16. Give Grobner and Raghuram a bibliography entry. I believe the paper is: H. Grobner and A. Raghuram, On some arithmetic properties of automorphic forms of GL_m over a division algebra, Int. J. Number Theory 10 (2014), 963-1013 (from memory; check against the linked PDF). [essential]
34. pp. 16-17. Say what the diagram is. From the paper's own formulas, lambda_j = nu_tau(n-j), so with rho_j = (n+1-2j)/2 one gets lambda_j + rho_j - t = -( l_tau(w_tau(n-j)) + (n-1)/2 ). So the twist is the tensor product with the power -t of the determinant, and the twisted diagram is the highest weight whose infinitesimal character is the negative of that of the automorphic representation at tau, in the archive's normalisation of l. The identity arith is then the usual |mu + rho|^2 - |rho|^2. I verified the algebra. This is the sentence a number theorist is looking for in Section 6, and it makes plain why equality, not an estimate, is needed. [recommended]
35. p. 17, third paragraph of Section 6.2. Shorten to what J is and supplies. [recommended]
36. pp. 17-20. Tables 1 to 3 are accurate where I checked. Move them to an appendix. In Table 3 the definition of IsSmall starts at line 37; the row gives 39-43, which is only its per-embedding clause. [optional]
37. pp. 20-22, Section 8. Reduce to a short provenance statement; move the changelog to the repository. [recommended]
38. p. 21. Version 1's citation check flagged 31 of about 50 citations. Say whether the check was run again on the version 2 list. In the ten sources I sampled every pinpoint was right. Outside the sample I found one pinpoint that is probably wrong (comment 12) and one work with no entry (comment 33). [recommended]
39. p. 22, Section 9. Remove or move to the repository. [recommended]
40. p. 23, "AI reviewers checked them in the review of version 2". Section 8 describes no review of version 2. Say who ran it, when, on which draft and what it found, or delete the clause. Changes made after that review are unreviewed and the text should say so. [essential]
41. References. Add the Lean and Mathlib citations and the references listed in Section 2 above. [recommended]

## 6. Recommendation

Minor revision, as an exposition.

Reasons. The mathematics is correct as far as I could check, and I checked all of Sections 2 to 5 and the correspondence with the Lean. The paper does what it sets out to do: a mathematician who reads pages 1 to 8 knows what the lemma says, that it is classical, and why it holds. The five essential items are small: two sentences in the notice (comments 1 and 2), one dependency check and a few lines in Section 6 (comment 9), one bibliography entry (comment 33), and one process statement (comment 40). The recommended restructuring (heights proof as the main line, a better example, process material out of the body) would improve the paper a good deal and would cut it to about fifteen pages, but the paper is usable without it.

For the editor, two cautions that bear on the venue. First, as a research article in a mathematics journal this is out of scope: the result is classical and the paper says so. Second, the notice says that no human has checked the text. Most journals' policies on generated text require a human author who takes responsibility for all of it. Until the author states that he does, and on what basis, a refereed journal cannot take the paper, whatever its accuracy.

Venues. The best fit is where version 1 already sits: a versioned preprint with a public repository and an errata channel. Among refereed venues, the closest are those for formalized mathematics and for AI in theorem proving: Annals of Formalized Mathematics for the exposition, or a workshop such as AITP or CICM for the method. For the method to be the subject, Section 9 would need a real evaluation: several theorems, including some with no classical counterpart, and human readers. The mathematical content alone, rewritten in six to eight pages by an author who vouches for it (the one-box identity, Theorem B, the duality in comment 31, the equality case as exchange relations), would make a fair note for an expository journal such as Expositiones Mathematicae or the American Mathematical Monthly.
