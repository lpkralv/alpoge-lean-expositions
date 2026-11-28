**Records:** Zenodo concept DOI [10.5281/zenodo.24514671](https://doi.org/10.5281/zenodo.24514671); version 1 DOI [10.5281/zenodo.24514672](https://doi.org/10.5281/zenodo.24514672); version 2 DOI [10.5281/zenodo.24619939](https://zenodo.org/records/24619939). Hexagon: [hexagon:2611.01006](https://hexagonmath.org/2611.01006); version 2 was submitted to Hexagon as a new version of hexagon:2611.01006 on 2026-11-28 and is awaiting moderation (once accepted it will be at https://hexagonmath.org/2611.01006v2).

Version 2 corrects a false attribution created by citation placement in version 1. It corrects the description of the Lean community's certification, which covers the Lean statement and proof of Mathlib's RiemannHypothesis. It removes the claim that the graders and first reviewers were independent and clarifies that AI models performed the checks previously described as hand checks. Supplementary results and blocks outside the Lean are now labelled. The paper adds the dependency chain from casBound_holds to the Riemann hypothesis theorem. Following journal-referee reviews, it reorganizes the exposition and adds explanatory material. The mathematics of Theorem A and Propositions 1–9 is unchanged.

**About this document**


An automated process generated this entire document, including this notice
and the framing sections, without human intervention in the text. It
combined mechanical work (a Lean build, dependency extraction and scripted
checks) with AI work (OpenAI models via Codex and Anthropic Claude models).
No human wrote, edited or checked the mathematical text of version 1, including its framing sections. An AI model drafted version 2 after AI review of version 1; no human checked version 2.

Louis P. Slothouber, a computer scientist, set the goal of building a tool
to explain AI-generated Lean proofs, approved the plan and method choices
proposed by the AI agents, and decided to publish. Errors are possible.
Corrections are welcome at https://github.com/lpkralv/alpoge-lean-expositions.

## Contents

- [paper/](paper/) contains version 2 as [paper.pdf](paper/paper.pdf) and [paper.tex](paper/paper.tex); [paper/v1/](paper/v1/) preserves version 1.
- [casbound/exposition.md](casbound/exposition.md) is the superseded version 1 exposition. The [release review record](casbound/review-record/release-review-2026-11-27/) contains the reviews, adjudication and revision logs; [casbound/review-record/](casbound/review-record/) also contains earlier reviews and checks.
- [validation-typeprimes/](validation-typeprimes/) contains the second exposition and grades against a hidden key built from Jeremy Rodgers's human reconstruction and other write-ups. The [before-review grades](validation-typeprimes/before-review/) document the 7 of 8 figure.
- [method/pipeline.md](method/pipeline.md) describes an early version of the method.

## The theorem

The exposition explains Levent Alpöge's theorem `casBound_holds`, the tableau Casimir bound, and its coordinate proof. It bounds the real quadratic form of the slot Casimir on a union of whole columns by the squared tensor norm times an explicit coefficient in the tableau label multiplicities. The contribution is expository. Alpöge's Lean archive, published on 2026-11-20, is available as `lean.tar.gz` parts at [alpo.ge](https://alpo.ge).

## Limitations

No human expert has read the paper. The AI models used for review and grading may share blind spots. The literature step required extensive correction before the citation check was complete. The audit covered the theorem and its callers; claims elsewhere in the archive remain outside it. Supplementary arguments outside Lean were checked by AI models and are labelled in the paper. The supplied Lean archive has no licence file.

## Corrections and licence

Please report corrections through [GitHub issues](https://github.com/lpkralv/alpoge-lean-expositions/issues) or by email to [lpslot@me.com](mailto:lpslot@me.com).

This repository is licensed under [Creative Commons Attribution 4.0 International](LICENSE).
