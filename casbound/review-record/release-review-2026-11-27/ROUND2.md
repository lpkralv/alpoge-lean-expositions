# casBound v2 final edit round

## Lean dependency trace

Yes. The proof term of `riemannHypothesis` in `Main.lean` transitively references `PositivityTheory.Rg.Cz.casBound_holds`. The route below follows uses in theorem bodies, including a structure field, through the all-character nonvanishing proof. The title is supported by this route.

Each entry after the first consumes its predecessor. Paths are relative to `targets/alpoge/lean/src` in the supplied read-only Lean tree.

| Declaration | Definition and use |
| --- | --- |
| `PositivityTheory.Rg.Cz.casBound_holds` | `Development/WeilBound/RepresentationTheoryGL/CasimirAlgebra/KugaCoordinates/CasimirBounds/CasBoundHolds.lean:9` |
| `PositivityTheory.Rg.Cz.clozelCohomological_of_three` | `Development/WeilBound/RepresentationTheoryGL/CasimirAlgebra/KugaCoordinates/ClozelCohomologicalOfThree.lean:10–11` passes `casBound_holds` to `clozelCohomological_of_rest`. |
| `PositivityTheory.Rg.Cz.clozelCohomological` | `Development/WeilBound/RepresentationTheoryGL/CasimirAlgebra/KugaCoordinates/ClozelCohomological.lean:8–9` |
| `UpperTheory.LiteratureTheorems.clozel_cohomological_of_literature` | `Development/AutomorphicArithmetic/ThetaCorrespondence/ThetaPairLifts/ThirdPlaceSeries/EveryCharacterOfLiteratureOfVWin.lean:327–328` |
| `UpperTheory.LiteratureTheorems.published_results_eigen` | The same file at lines 666–667 fills the `clozelCohomological` field. |
| `UpperTheory.LiteratureTheorems.every_character_of_literature_of_vWin` | The same file at lines 810–811 passes `published_results_eigen O` to `UpperTheory.Lit.every_character_of_theta_integrals_local_matching`. |
| `UpperTheory.FinalTheorems.everyCharacter_of_row` | `Development/AutomorphicArithmetic/CharacterBoxes/MainConclusion.lean:7–8` |
| `UpperTheory.FinalTheorems.everyCharacter` | The same file at lines 10–11. |
| `allChi` | `Supplements/Kernels/MainTheorems.lean:7` |
| `rhOfAll` | `Supplements/Kernels/MainTheorems.lean:9` passes `allChi` to `Formalism.VW.rh_of_every`, defined at `Formalism/GammaFactorNonvanishing/CritLine.lean:29`. |
| `riemannHypothesis` | `Main.lean:4` uses `rhOfAll`. The separate `UpperTheory.FinalTheorems.riemannHypothesis` also uses `everyCharacter` at `Development/AutomorphicArithmetic/CharacterBoxes/MainConclusion.lean:13–14`. |

The literature wrapper also feeds `regular_algebraic_purity_of_literature` at `EveryCharacterOfLiteratureOfVWin.lean:493–494`. The constructor `GlobalTheory.regularAlgebraicPurity_of_clozel` pairs the purity and cohomologicality conclusions at `Development/AbelianVarietyTheory/Proofs/SatakeParameters/RegularAlgebraicPurityOfClozel.lean:8–11`. The resulting field enters the same package at `EveryCharacterOfLiteratureOfVWin.lean:689`.

The other two direct uses of `PositivityTheory.Rg.Cz.clozelCohomological` are `UpperTheory.V.Z.Coh.clozelCohC` at `Development/AutomorphicArithmetic/AutomorphicVarieties/ModularityArgument/ClozelCohomology/ClozelCohC.lean:11,24`, which feeds `clozelConjC` in the adjacent `ClozelConjC.lean:26–27`, and `UpperTheory.LiteratureTheorems.clozel_cohomological_of_open` at `Development/AutomorphicArithmetic/AutomorphicVarieties/ModularityArgument/ThresholdArguments/DenseThresholdCases/TemperedProductOfSquareIntegrable.lean:277–278`, which supplies a field of `automorphic_inputs_from_literature` in the adjacent `TopMainZj.lean:38,49`. Table 3 records all three direct uses. The trace used source searches for names followed by inspection of their declaring proof bodies. The Lean tree was read-only throughout. Mathlib was not built.

## Source checks

- Macdonald, second edition, chapter I, §1. Display (1.3) defines the conjugate by column lengths. Display (1.11) reverses dominance under conjugation and remains cited in the content proof. [Macdonald, PDF](https://math.berkeley.edu/~corteel/MATH249/macdonald.pdf)
- Harald Grobner and A. Raghuram, *On some arithmetic properties of automorphic forms of GL(m) over a division algebra*, *International Journal of Number Theory* 10(4) (2014), 963–1013. The opening of the proof of Theorem 6.3 invokes Clozel’s Lemme 3.14. [University of Vienna publication record](https://ucrisportal.univie.ac.at/en/publications/on-some-arithmetic-properties-of-automorphic-forms-of-glm-over-a-/) · [Authors’ PDF](https://homepage.univie.ac.at/harald.grobner/papers/GLn%28D%29.pdf) · [arXiv](https://arxiv.org/abs/1102.1872)

## Verification

- The comparison extracted the full statement bodies by label from the supplied v1 and final v2 TeX, using `thm:bound` in v1 and `thm:A` in v2. It removed all whitespace and excluded headings and labels. All ten matched. The lengths in order A, 1–9 were 632, 245, 171, 283, 262, 240, 280, 500, 517 and 556 characters. Changing `2i+1-n` to `2i-1-n` in an in-memory control produced a mismatch.
- Exact rational arithmetic on the six signed basis coefficients confirmed the new unit tensor has Casimir expectation 3, ceiling 9, one-order deficit 3 and total deficit 6. The TeX shows the calculation by swaps and by Theorem B.
- The PDF was rebuilt with pdfLaTeX. Three passes produced 25 pages. All 41 citation keys resolved, and the final log reported no undefined references, undefined citations or overfull boxes.

## Reviewer suggestions not applied

- Fable 2 and venue advice on human responsibility. Louis’s direction fixes the current attribution and disclosure. The notice gives the errata address.
- Fable 4. The alternate title was conditional on the trace. The current title follows from the proof terms.
- Fable 5. The optional subject classification changes were outside the corrections agreed on for this round.
- Fable 10. A rebuild script and all fourteen checksums would add deliverables, and the historical compile results remain attributed to the reviewers who ran them.
- Fable 16 and Astra §4 on making the height argument the main proof. The coordinate order remains aligned with the Lean. The introduction and Theorem B now give the short route by heights.
- Fable 18 and Astra §4 on consolidating Propositions 4–9 or factoring out all standing data. This would alter the presentation of the protected statements.
- Fable 24 on a separately numbered lemma. The proof now derives the formula directly from Proposition 2, with the partition and internal swaps stated where used.
- Fable §3 and §4 on a precise purity application and formal-library motivation. The paper identifies the purity field and its consumer. The reason the archive’s authors chose the coordinate proof is unverified.
- Fable 30 and 41 on more background references. The additional catalogue of standard references for Pieri, content, Young’s rule, Cartan components and skew duality was optional. The proposed Macdonald content pinpoint was from memory.
- Fable §2 and 41 on adding Lichtenstein, Weyman’s book, Towber, Goodman–Wallach, Rowe–Carvalho–Repka, Matsushima–Murakami, Enright, and Vogan–Zuckerman. These are optional extensions to the literature discussion. The existing proofs have local references, with Etingof and Akin–Buchsbaum–Weyman added where they directly support the exposition.
- Fable §2 and 41 on Lean and Mathlib system papers, Mizar, Coscoy–Kahn–Théry, and recent model informalization work. A history of formal-proof exposition and system citations would extend the paper’s scope.
- Fable 31. The proposed skew Howe dual-pair identity would add a representation-theoretic derivation. The paper gives the transfer-square calculation already used in the comparison.
- Fable 36–39, Astra §4 and Sol prose audit on moving Sections 7–9, the concordance, model roster and revision history. This is a structural revision. The reports and checks now have explicit version and draft attribution.
- Fable 38 on repeating the full citation audit. The paper identifies the targeted v2 checks on record. A second full sweep is unverified.
- Fable and Astra venue suggestions, and Fable’s larger evaluation across theorems and with human readers. Venue choice and a new study are separate tasks.
- Sol cold read on drawing match arrows directly on Figure 1. The caption identifies the columns, matching label and two orders without adding graphical notation.
- Sol cold read’s three-row assembly table and Terra’s one-page proof map. The proof opening and displayed arithmetic supply the requested counts in place.
- Terra on a diagram beside the first list of notation. Figure 1 follows the short observation that explains its labels and heights.
- Terra on superscripting every use of the pair-specific Y. Theorem B already says the operator is defined for that pair.
- Sol prose audit’s first proposed rewrite. The notice follows the user’s instruction to preserve the existing authorship framing.
- Sol prose audit on removing every numbered remark or replacing every correction and transition. Some local rewrites remain optional, including the mirrored endings of the two cases of Proposition 7 and some explanatory transitions in §§4–5.
- Sol prose audit on rewriting the detailed pipeline inventory in §8.1 and compressing the `typePrimesN` grading account in §9. The chronological record and grading qualifications remain in place.
