# FIX — casBound v2 final delta

## Two corrections

1. **Kuga adjoint normalization (§6, paper.tex:1277–1281).** The paragraph calls the operator after the differential its adjoint and then multiplies its quadratic form by the degree factor. With the archive's cochain pairing, write δ for `kDel` and q for the degree of ω. The source identity is ⟨dω,θ⟩ = (q+1)⟨ω,δθ⟩, so the adjoint on degree q+1 is (q+1)δ. The quantity estimated by the Casimir terms is Re⟨ω,δdω⟩. Multiplying it by q+1 gives ‖dω‖². Naming δ in those two sentences preserves the vanishing argument. See `KugaAbsoluteValues/KugaAbsHolds.lean:15,145–151,158–171`.
2. **V2 fact-check attribution (§8.3, paper.tex:1608).** Change “Codex checked” to “Sol checked” or “Codex Sol checked.” Both the TeX and the PDF give only the platform. The review record supplied for this check identifies the model as Sol.

## 1. Lean dependency

I followed the source bodies from ordinary RH down to the bound in the specified Lean tree. The entries give the reference made at each site. This was a source trace without a Lean rebuild.

| Proof site under targets/alpoge/lean/src | Reference in the body |
|---|---|
| `Main.lean:4` | `riemannHypothesis` takes `rhOfAll`. |
| `Supplements/Kernels/MainTheorems.lean:9` | `rhOfAll` applies `Formalism.VW.rh_of_every` to `allChi`. The former uses its hypothesis at modulus one in `Formalism/GammaFactorNonvanishing/CritLine.lean:29–32`. |
| `Supplements/Kernels/MainTheorems.lean:7` | `allChi` takes `UpperTheory.FinalTheorems.everyCharacter`. |
| `CharacterBoxes/MainConclusion.lean:10–11` | `everyCharacter` applies `everyCharacter_of_row` to the Galois input. |
| `CharacterBoxes/MainConclusion.lean:7–8` | `everyCharacter_of_row` applies `UpperTheory.LiteratureTheorems.every_character_of_literature_of_vWin`. |
| `ThirdPlaceSeries/EveryCharacterOfLiteratureOfVWin.lean:810–811` | The first argument to `every_character_of_theta_integrals_local_matching` is `published_results_eigen O`. The receiving theorem uses the package at `ThirdPlaceSeries/SiegelEisensteinSecondTermHypotheses.lean:69–73`. |
| `EveryCharacterOfLiteratureOfVWin.lean:666–667` | The constructor for `published_results_eigen` sets its cohomologicality field to `clozel_cohomological_of_literature O`. |
| `EveryCharacterOfLiteratureOfVWin.lean:327–328` | That theorem takes `PositivityTheory.Rg.Cz.clozelCohomological`. |
| `KugaCoordinates/ClozelCohomological.lean:8–9` | `clozelCohomological` applies `clozelCohomological_of_three`. |
| `KugaCoordinates/ClozelCohomologicalOfThree.lean:10–11` | Its final argument to `clozelCohomological_of_rest` is `casBound_holds`, declared in namespace `PositivityTheory.Rg.Cz` at `KugaCoordinates/CasimirBounds/CasBoundHolds.lean:7–9`. |

The second route through the purity field also checks out. Line 689 of `EveryCharacterOfLiteratureOfVWin.lean` takes the theorem at lines 493–494, which supplies the Clozel wrapper to the constructor at `SatakeParameters/RegularAlgebraicPurityOfClozel.lean:8–11`. The other consumers in Table 3 occur at `ModularityArgument/ClozelCohomology/ClozelCohC.lean:11,24` and `DenseThresholdCases/TemperedProductOfSquareIntegrable.lean:277–278`. Their respective callers are `ClozelConjC.lean:26–27` and `TopMainZj.lean:38,49`.

## 2. Running example

The displayed coefficients are the permutation signs on six distinct orthonormal basis vectors, divided by √6. Thus ‖u‖² = 1 and each transposition sends u to −u. Proposition 2 gives Ku = (9−6)u = 3u. The heights 2 and 1 give 4+3+2 = 9 in Theorem B(a). Independently, the label counts (0,1,2) give 0+1+8 = 9. For the unique box in the shorter column, Y is the sum of two swaps, hence (I−Y)u = 3u. Theorem B(b) gives 2·9/(2+1) = 6, exactly 9−3. At rank two the enlarged exterior cube vanishes, as the preceding example states.

## 3–4. Notice and history

The first-page notice in the TeX and PDF says no human checked either version. It credits automated generation and AI review, and identifies Louis as the person who set the goal, approved the approach and decided to publish and revise.

Section 8.2 agrees with the seven entries in `CONSOLIDATED.md`: Fable and Astra verified v1, Fable and Astra refereed, Opus and Sol supplied cold reads, and Sol audited the prose. Section 8.3 correctly assigns the v2 adversarial deltas and referee reports to Fable and Astra, the cold reads to Sol and Terra, and the prose audit to Sol. It scopes those reports to the pre-final draft. The missing model name in the targeted fact-check is correction 2 above.

## 5. Sources

Macdonald's second edition gives the column-length formula for the conjugate partition at I.1 (1.3), dominance reversal at I.1 (1.11), and the sign twist at I.7, Example 2. These support the uses at paper.tex:248 and 1215. [Macdonald, second edition](https://math.berkeley.edu/~corteel/MATH249/macdonald.pdf)

Grobner and Raghuram explicitly invoke Clozel's Lemme 3.14 in the opening sentence of the proof sketch of Theorem 6.3. The title, authors, journal, volume 10, issue 4, year 2014, pages 963–1013, DOI and arXiv identifier agree. [Authors’ paper, Theorem 6.3](https://arxiv.org/pdf/1102.1872#page=20) · [University of Vienna publication record](https://ucrisportal.univie.ac.at/en/publications/on-some-arithmetic-properties-of-automorphic-forms-of-glm-over-a-/) · [Journal article](https://doi.org/10.1142/S1793042114500110)

## 6. Protected mathematics

I extracted the complete statement after each label through the end of its theorem or proposition environment from both supplied TeX files. Theorem A (v1 label thm:bound) and Propositions 1–9 all match word for word after collapsing whitespace. This comparison preserves every hypothesis, formula and conclusion and excludes the headings and labels. The Kuga normalization issue is in the new application prose.
