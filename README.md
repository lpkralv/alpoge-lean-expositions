**About this document**

An automated process generated this entire document, including this notice
and the framing sections, without human intervention in the text. It
combined mechanical work (a Lean build, dependency extraction and scripted
checks) with AI work (OpenAI models via Codex and Anthropic Claude models).
No human wrote, edited or checked the mathematical text of this document, including its framing sections.

Louis P. Slothouber, a computer scientist, set the goal of building a tool
to explain AI-generated Lean proofs, approved the plan and method choices
proposed by the AI agents, and decided to publish. Errors are possible.
Corrections are welcome at https://github.com/lpkralv/alpoge-lean-expositions.

## Contents

- [paper/](paper/) contains the exposition as [paper.pdf](paper/paper.pdf) and [paper.tex](paper/paper.tex).
- [casbound/exposition.md](casbound/exposition.md) contains the exposition; [casbound/review-record/](casbound/review-record/) contains every review, audit, gate check, citation check and revision log.
- [validation-typeprimes/](validation-typeprimes/) contains the second exposition and two grades against a hidden key built from Jeremy Rodgers's human reconstruction and other write-ups.
- [method/pipeline.md](method/pipeline.md) describes the method.

## The theorem

The exposition explains Levent Alpöge's theorem `casBound_holds`, the tableau Casimir bound, and its coordinate proof. It bounds the real quadratic form of the slot Casimir on a union of whole columns by the squared tensor norm times an explicit coefficient in the tableau label multiplicities. The contribution is expository. Alpöge's Lean archive, published on 2026-11-20, is available as `lean.tar.gz` parts at [alpo.ge](https://alpo.ge).

## Limitations

No human expert has read the paper. The AI models used for review and grading may share blind spots. The literature step required extensive correction before the citation check was complete. The audit covered the theorem and its callers; claims elsewhere in the archive remain outside it. The highest-weight proof and two remarks labelled “not in the Lean; checked by hand” were checked by an AI model outside Lean. The supplied Lean archive has no licence file.

## Corrections and licence

Please report corrections through [GitHub issues](https://github.com/lpkralv/alpoge-lean-expositions/issues) or by email to [lpslot@me.com](mailto:lpslot@me.com).

This repository is licensed under [Creative Commons Attribution 4.0 International](LICENSE).
