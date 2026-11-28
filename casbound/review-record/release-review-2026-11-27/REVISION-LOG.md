# Revision log: casBound paper, version 1 to version 2

Written 2026-11-27 by the writer agent (Claude Fable 5.2) for mathematics-Vance_1.
Revised file: `docs/publications/casbound-release-v2/paper/paper.tex`. Version 1 at `docs/publications/casbound-release/paper/paper.tex` is untouched.
Rulings followed: `review-2026-11-27/ADJUDICATION.md`. Finding ids are those of `review-2026-11-27/CONSOLIDATED.md`.

## Read this first

- **Not compiled.** This session had no shell, so no LaTeX run was possible. I checked by script that braces, environments and math delimiters balance, that every `\cite` has a `\bibitem` and the reverse, that every `\ref` has a `\label`, that table rows have the right number of cells, and that no bare `_ # % ^ &` stands outside math, URLs or tables. Page breaks, the figure and the three longtables need one compile to confirm.
- **Mathematics unchanged.** The displayed statements of Theorem A (version 1's Theorem 10) and Propositions 1 to 9 are character-identical to version 1 apart from white space (checked by script). The proof steps are the same; commentary was moved out of the proofs.
- **Length.** Version 2 is longer than version 1 (about 9,100 words against 6,700 by a crude count), although the reviewers asked for about half. The cuts were made (design list, routine-facts list, notation table, heuristic, repeated edge cases and comparisons). The additions the rulings require outweigh them: classical context, Theorem B, the running example and figure, provenance marks, three concordance tables, the change list and the longer Limitations section.

## Structure of version 2

1. Introduction: the result by heights, that it is classical, what the archive adds, the one identity, the archive's status (joint statement, axioms report), the survey, and the three kinds of statement.
2. Setting and statement: notation in prose, the Observation on labels, Figure 1, Theorem A (the Lean statement), Theorem B (heights form and sum of squares, not in the Lean), the running example.
3. The coordinate proof: Propositions 1 to 9 with the Lean's arguments only, Remarks after each, proof of Theorem A, proof of Theorem B.
4. Why simpler estimates fail (not in the Lean).
5. The classical proofs (not in the Lean): highest weights with Proposition 10, exterior transfer with Proposition 11, the content formula.
6. The role of the theorem in the archive, without line references.
7. Concordance: Table 1 results, Table 2 definitions and auxiliary lemmas, Table 3 the application.
8. How the document was produced, with the eight corrections. 9. The typePrimesN test. 10. Limitations.

Numbering: the main theorem is Theorem A, the heights/identity statement is Theorem B, Propositions 1 to 9 keep their version 1 numbers, Propositions 10 and 11 are the two results version 1 had inside other proofs.

## Findings

| id | what changed in version 2 |
|---|---|
| D1 | Certification sentence rewritten: quotes the joint statement of the Lean FRO and Mathlib Initiative (21 November 2026), scopes it to Mathlib's `RiemannHypothesis`, says it does not mention GRH, and cites it as a new reference [JointStatement]. Release date cited to the joint statement as CONSOLIDATED proposes. Title kept (the allowed option "keep the title only with that citation"); the text says the joint statement is the only basis for the title's words. The running-head form "Alpöge's Lean archive" remains the alternative if Louis prefers it. |
| D2 | "checked by hand" is gone as a label. Every instance is the macro `\notlean` = "not in the Lean; checked by an AI model". The old phrase appears once, quoted, in the list of corrections in Section 8. |
| D3 | No citation cluster hangs on a sentence about the archive's proof. Each citation sits in a sentence that says what the source gives. "Alpöge's coordinate proof follows [five sources]" is gone; Section 5 opens by saying the coordinate proof follows none of the sources cited there. |
| D4 | Every statement is marked: Lean declaration in the head of Theorem A and Propositions 1 to 9; `\notlean` in the head of Theorem B, Propositions 10 and 11, the Observation, the running example and every Remarks block, and in the first line of Sections 4, 5 and 3.6. The transfer squares are Proposition 11. Section 1.3 states the convention; Section 10 lists all non-Lean material and the checks on record. |
| D5 | "independent" dropped for graders and reviews. Sections 8, 9 and 10 say gpt-6.2-sol drafted the text, was one of the two first reviewers and one of the two graders. |
| D6 | Reference [Rodgers]: correct title, "version 2 (repaired referee edition), 22 November 2026", DOI 10.5281/zenodo.24473551. |
| D7 | Reference [AlpogeArchive]: no claim about the home page or SHA256SUMS. Gives the part-01 URL, says the remark links the parts (adversarial-astra 19), and prints the part-01 SHA-256 "as downloaded on 27 November 2026" (verifier-fable 7). |
| D8 | Gleizer–Postnikov §2 pinpoint removed. Section 5.1 gives the reason: the h! orderings are distinct coordinate basis tensors, hence orthonormal. |
| I1 | The 7-of-8 figure stays, in Section 9 only. Section 9 now says the graders ran four times before review and once after, with pipeline steps re-run between rounds, that the round just before review scored 7 of 8 with both graders, and that two earlier rounds on record also did. It says the version 1 package did not include the before-review grades. **Partly open:** no public pointer to the before-review grade files, because they are not yet published (see "For the boss", 1). |
| I2 | typePrimesN removed from the abstract. Section 9 opens and closes with what the test does and does not show. |
| I3 | Abstract and Section 1.1 say the inequality is the classical Cartan-component fact and that the archive's contribution is the coordinate proof. |
| I4 | Section 1.2 quotes the remark ("working with Claude", "Claude and I have also formalized the arguments") and defines "the archive's proof" as that joint work. "Alpöge's proof" and "his existing theorem" no longer appear in the body. The title still reads "Alpöge's Lean proof" (see D1). |
| I5 | Section 1.2: ten files, 975 lines, 466 of them the five proof files (I recounted: 34+96+92+87+157), the rest imported definitions; the `#print axioms` result from both verifiers; Lean 4.33.1; Mathlib revision 0df444a3 (verifier-fable). |
| I6 | "comparison with a human write-up" removed. Section 9: "an answer key that an AI model extracted from published write-ups". No statement about how Rodgers's text was written. |
| I7 | The two-column transfer bound is Proposition 11. No reference to "the calculation in Proposition 3" remains. |
| I8 | Proof of Proposition 11 says A_i†A_j is the induced action of E_ij, not a single matrix unit in the wedge basis, identifies it with the slot sum, and states the adjointness under the isometric identification at that point. |
| I9 | "Heuristic" paragraph deleted. Remark (2) after Proposition 3 gives the exact identity (Id−Y)²f = (s+1)(Id−Y)f. |
| I10 | The pair-deficit identity is equation (3) in Section 3.6, after all its terms are defined (X_cc' is defined in Section 2.2 as the sum of P_pq), derived by summing Proposition 3's identity over p in S_c, with the note that it holds for either source column and the shorter gives the better bound. |
| I11 | Proposition 10 and Section 5.1 add: μ is a weight of the product of exterior powers; why the basis order is reversed; U(n) acts unitarily so summands are orthogonal; equality forces μ = λ, so equality in Theorem A holds exactly on the Cartan component. |
| I12 | The comparison is Proposition 10 and is cited by number. |
| I13 | Section 8.1 points to `casbound/review-record` in the release repository. I checked that the release copies carry the counts: revise1-log.md has 22 "applied" and 1 "rejected"; fix-log.md line 803 has 31, 28 and 3. |
| I14 | Not a writer decision (For Louis, item 2). The honest framing is kept and updated in the About box: an AI model rewrote version 1 after an AI review; no human wrote, edited or checked either version. |
| I15 | Partly done. Math-Net link replaced by the stable record mathnet.ru/eng/im2520; Yang given its DOI; Howe now JSTOR stable 2001418; third-party copies of Macdonald, Jucys and Frobenius removed (Frobenius dropped altogether); arXiv links point to abstract pages; Hazewinkel links are the CWI records; "Grassmann" capitalised; Rodgers dated; undated write-ups marked "as surveyed on 24 November 2026". **Not done, no data in the permitted sources:** DOIs for the other entries, an author for [Dupuy], a document for [Ulam] beyond the home page, a locator for Baur 2003. |
| I16 | Each citation now says what the source gives: CKM gives the transfer generators and Howe the framework, "the transfer-square identities and the height bound are calculations made in this exposition"; Lévy "has the opposite sign and is written with unordered transpositions"; the content scalar is cited to Cesi (4.1) and Prop. 4.1, with Okounkov–Vershik (2.1), Prop. 6.2 and Thm 6.4 named together; Baur's thesis Prop. 3.2 is cited for multiplicity one of the top weight; Cesi's multipartite result and Frobenius are dropped. |
| S1 | **Declined in part: the locators cannot be checked from the permitted files.** CONSOLIDATED says "add them after checking each locator"; referee-fable says its section numbers are from memory; version 1's own citation check removed Murphy 1981 because it could not be fetched. Adding them unchecked would repeat defect D8. The classical context itself is stated from sources already in the paper (Baur, Etingof, Yang, Molev, Jucys 1971, Macdonald). The list for the boss to check and add is under "For the boss", 2. |
| S2 | Remark (2) after Proposition 3: Y commutes with swaps inside B, (Y−Id)(Y+s·Id) = 0 on tensors alternating on B, spectrum in {1, −s}. The text before the proposition names the Jucys–Murphy element and the two contents, attached to the Molev citation. |
| S3 | Navrátil–Kamuntavičius–Barrett, Navrátil–Barrett and Szőke removed. The projector identity is derived in the text and cited to Jucys 1971 (3) and Molev (7)–(9). |
| S4 | Etingof Lemma 26.6 cited for the Casimir scalar. |
| S5 | Reordered as in "Structure" above. |
| S6 | Theorem B: (a) heights form, (b) the sum-of-squares identity of referee-fable, (c) the equality case. Stated next to Theorem A, proved in Section 3.6 from Propositions 2, 3 and 6, marked not in the Lean. |
| S7 | Every proof contains only the argument. Alternatives, failed approaches and counterexamples are in Remarks or Section 4. The highest-weight proof has its own subsection. |
| S8 | Labels n−h..n−1: the Observation in Section 2.1. The antisymmetrizer: the text before Proposition 3. Why the constant must be exact: Section 1.1 and Section 6.1. |
| S9 | Application moved to Section 6 with no line references; one sentence on exactness in the introduction; the reason ν is nondecreasing added from referee-astra 5.2. Archive step names are kept as names, each with what it supplies; the text says they are not explained further. |
| S10 | Running example n = 2, columns {0,1} and {1}, f = (|010⟩ − |100⟩)/√2, carried through Proposition 2, Proposition 3 (equality case Yf = f), Proposition 8 (unequal-label swap with expectation 1/2) and the end of the proof (6 − 2 + 2 = 6). |
| S11 | Figure 1, a tabular diagram of four bottom-aligned labelled columns at n = 4 with the counts m_i. **New illustrative numbers** (heights 3,2,2,1; m = (0,1,3,4); coefficient 40 both ways), computed for this revision and marked as such in the caption. |
| S12 | Edge cases stated once, after Theorem A. The scattered n = 0, S = ∅, f = 0 remarks are cut; the two that carry content stay (s = 0 in Proposition 3; empty target column reads 0 ≤ N). |
| S13 | "Why the proof is built this way" cut. Its reasons sit beside their steps (Remarks) or in Section 4. |
| S14 | Table 2 lists count_rhs, count_same, dot_pm_swap, isWH_coeff_one_polynomial, eAt_applyC, tE_zero_apply, sum4 (and pm_pm, TV, eAt, tE, pm, IsTab, CasBound), with line ranges I read from the Lean files. **The stranded-row page break could not be checked** (no compile). |
| S15 | The abstract states the inequality; the introduction states it before any Lean name. |
| S16 | One sentence each: the hypotheses are stated on all of Q and used only on S (after Theorem A); the signed-N generality is the Lean's and the application has N ≥ 0 (after Proposition 7). |
| S17 | s is only \|B\|. The twist is t. k is only the prefix length in Proposition 10. Target-column size is written h_c'. |
| S18 | c is only a column index; slot triples are (τ, i, r); the Casimir scalar is κ_τ; q is only a box; the twisted Casimir is K^tw_τ; γ throughout; the rank is n throughout. Table 3's caption maps these to the Lean's a, s and Fin(q). |
| S19 | Notation table replaced by prose definitions in Sections 2.1 and 2.2, before the theorem. X_cc' is defined as the sum of P_pq over the two columns. Section 6 defines its own symbols where used. |
| S20 | Terminal intervals: stated as the Observation. Zero-background: explained in Section 2.2. Row bound: renamed "one-box bound" and defined. Tensor of highest wedges: defined in Section 5.1. Active: defined. Ambient, trace-form, equal-label comparison: replaced or defined ("match"). Charge, debit, cost: replaced by "contribution" and "term". |
| S21 | "common rows" no longer appears; the text says common labels. |
| S22 | Same fix as D3 for the remaining clusters. No citation stands after a full stop. |
| S23 | Disclosure said once in the About box; "Errors are possible" cut; purpose stated once; the repeated subheading and the stray "also" are gone. |
| S24 | Section 8.1 rewritten as a plain account ending on the checks and the pointer to the logs. "A final check judged the exposition ready" cut. |
| S25 | Scope boilerplate cut. Section 6.2 ends by saying which archive proofs the document does not explain. The "convenience" sentences are replaced by what the application takes. |
| S26 | "Routine and classical facts" list cut. The classical facts are cited where used in Section 5; the Lean-backed routine steps are in Table 2. |
| S27 | No bold or italic lead-in lines in the literature material; it is connected prose inside Section 5. |
| S28 | Road map reduced to four sentences at the end of Section 1.3 and one at the start of Section 3. Route announcements and handoff sentences cut. |
| S29 | The separate-versus-grouped comparison is stated once, in Section 4.2. The three-way recap for the sign of N is cut. |
| S30 | The four compressed sentences are rewritten (Remark (3) after Proposition 3 uses referee-fable's reading); "spectators" and "carried along" replaced by "K acts as the identity on the factors outside S". |
| S31 | Whole text rewritten with the unslop rules in mind; a script found none of the stock vocabulary and no em dashes. A separate /unslop pass by another model is still worth doing. |

Declined: S1 in part (reason above). Not fully closable by the writer: I1 (public pointer), I14 (Louis), I15 (missing bibliographic data), S14 (page break).

## Statements that are new in version 2 or changed in wording

None changes Theorem A or Propositions 1 to 9. All are marked not in the Lean.

1. The Observation (labels of S_c are n−h_c..n−1; two columns share min(h_c, h_c') labels; m_i is the number of active columns of height at least n−i). Version 1 had the first part inside the proof of Proposition 7.
2. Theorem B(b), the identity from referee-fable §4, and B(c), its equality case. Derivation written out in Section 3.6.
3. Remark (2) after Proposition 3: (Y−Id)(Y+s·Id) = 0 and the spectrum (referee-fable 3.6, adversarial-astra 17).
4. Proposition 10's equality clause, and "equality in Theorem A holds exactly on the Cartan component" (referee-fable 3.9).
5. The explicit reverse transfer T' = Σ A_i† ⊗ A_i in Proposition 11. Version 1 said only "reversing the transfer".
6. K = nd·Id + 2Z and "twice the content sum is Σ μ_j(μ_j+1−2j)" in Section 5.3 (adversarial-astra 4 and 12).
7. Section 6.2: the reason ν is nondecreasing (referee-astra 5.2) and m_i = ν_τ(i) (read from CoefGlueHolds.lean:97).
8. Section 6.1: "a scalar t subtracted on the diagonal" (read from cas_shift, SumFinVal.lean:33–37).
9. Figure 1's numbers and the running example's totals.
10. Yang's formula is printed with n where Yang writes N.

## Cut from version 1

The seven-bullet design list; the notation table; the routine-facts list; the Heuristic paragraph; the Remarks after Propositions 1, 2, 6, 8 and 9 that only restated edge cases; the P_pp accounting sentences in Proposition 2; the weak-cutoff paragraph in Proposition 4; the "would add dN" and "if p ∉ S" sentences in Proposition 5; the "scales" paragraph and the "assigning −N to the diagonal" counterfactual in Proposition 9; the three-way recap in Proposition 7; the sentence that Szőke uses the same signs (dropped with its source). No statement of a theorem or proposition and no proof step was cut.

## Claims I could not support, or supported only at one remove

1. **Release date in the joint statement.** I cite [JointStatement] for "released on 20 November 2026" because CONSOLIDATED D1 says to. CONSOLIDATED quotes the certification sentence but no line with the date, and I could not fetch the page. The SME store entry confirms the date from other sources.
2. **Title of the joint statement.** The bibliography describes it as "joint statement on the Lean verification of the Riemann Hypothesis, Lean community blog". That wording comes from the SME store entry named in CONSOLIDATED, not from CONSOLIDATED itself.
3. **The fourth pre-review grading round.** CONSOLIDATED proposes "each pre-review round scored 7 of 8" but evidences three rounds (v4-condition-scope and two earlier commits) out of four. The paper says "the round just before the review" and "two earlier rounds on record".
4. **Reviewer model versions.** Only referee-fable states a version (Claude Fable 5.2). The paper names the others by family (Astra, Sol, Opus). It names Claude Fable 5.2 as the writer of version 2.
5. **Hashes for parts 02 to 14 and a working checksum file.** Not in any source; only the part-01 hash is printed.
6. **Dates and versions of four write-ups** (Zhang, Dupuy, Adriazola, Ulam): only the survey date is given.
7. **"A search of Rodgers's full text found no treatment of the module"** is carried over from version 1. Adversarial-astra confirms the narrower fact that "casBound" has no match there.
8. **What each cited source contains.** Taken from version 1's citation-check.md and from adversarial-astra 18. No source was fetched for this revision; the paper says so in Sections 8 and 10.
9. **Table 3, second part** (PKType.lean, CochainHolds.lean, Summand.lean locations) comes from verifier-fable 8. I read PKTypeA.lean:13, 15 and 207–220, CoefGlueHolds.lean:88–150, SumFinVal.lean:33–37 and 111–114, KTypeData.lean and StepFormula.lean:88–94 myself; the rest I did not open. The first part repeats version 1's references, which two reviewers confirmed.
10. **The About box** says no human wrote, edited or checked version 2, and that Louis "decided after the review of version 1 that the paper would be revised or retracted" (from ADJUDICATION). Both need to be true on the day of posting.
11. **The `\date` line** reads "Version 2, November 2026" and gives version 1's Zenodo DOI and Hexagon number from CONSOLIDATED. Adjust if the posting date differs.

## For the boss

1. **Before-review grade files (I1).** When they are published, add the pointer to Section 9, last-but-one paragraph, replacing "The package of version 1 did not include the grades made before the review."
2. **S1 references to check and add.** Humphreys, GTM 9, §13.4 Lemma C (place: after Proposition 10); Fulton, Young Tableaux, §8.1 and Fulton–Harris §6.1, §25.1 (Section 2.1 or 5.1); Jucys, Rep. Math. Phys. 5 (1974) 107–112 and Murphy, J. Algebra 69 (1981) 287–297 (text before Proposition 3); Howe, Schur Lectures, Israel Math. Conf. Proc. 8 (1995) 1–182 (Section 5.2); Clozel, Perspect. Math. 10 (1990) 77–159 and Borel–Wallach, 2nd ed., ch. II (Section 6.1). Data as given by the two referees.
3. **Compile once** and look at Figure 1 (tabular with partial rules), the three longtable captions, and the long Lean names in the heads of Propositions 6 and 7.
4. **Title.** Kept. If Louis prefers the running-head form, change `\title` and `pdftitle`, and delete the sentence in Section 1.2 that begins "The joint statement does not mention".
