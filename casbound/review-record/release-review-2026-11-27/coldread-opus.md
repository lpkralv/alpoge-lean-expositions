I couldn't write `local-source/Mathematics/docs/publications/casbound-release/review-2026-11-27/coldread-opus.md`. My instructions here forbid writing any file, and this session has no write or edit tool. The full report is below; save it as-is if you want it in the review folder. I read only `<local>/paper.tex` and the PDF for page numbers. I did not open the Lean or the longer exposition.

**Top findings**
1. paper.tex:766 (p11): the key structural fact is buried. Distinct labels plus upward closure mean column c's labels are exactly {n−h_c,…,n−1}. The paper only says this halfway through the proof of Proposition 7. Stated up front, it reduces Propositions 4, 5 and 7 to counting.
2. paper.tex:971–974 (p13): the clearest form of the bound comes only in the final remark: Σ h_c(n+1−h_c) + 2Σ min(h_c,h_c′). The classical meaning ("on ⊗Λ^{h_c}ℂⁿ the Casimir is at most its value on the Cartan component") is spread across lines 273–279.
3. paper.tex:124, 271, 658, 933, 976: "checked by hand" conflicts with paper.tex:31 ("No human … checked") and :1129–1130 ("checked by an AI model"). A reader will assume a human did the check.
4. paper.tex:576–603 (p9): the one-box identity is the core of the paper. It comes after about 35 lines of failed alternatives, an exterior-transfer calculation the Lean doesn't use, and a "Heuristic" paragraph that doesn't make sense to a reader.
5. paper.tex:144–227 (p2–3): the "idea in brief" turns into two dense automorphic paragraphs. "Coefficient gluing", "Kuga", "IsSmall", "spherical descent" and "quantum determinant factor" are never defined, and Lean line numbers are scattered through the text. This is where I lost the thread.
6. Notation reuse: s is both |B| and the twist (lines 151, 202, 409). k is a column height (126, 192) and a prefix length (420). n is used where a is meant (151 vs 168). c is a column index and also a slot coordinate (204).
7. Most proofs (Propositions 2, 3 and 9, and the Theorem) start with paragraphs that say what would fail, then give the argument. The argument starts at lines 490, 576, 891 and 947.
8. I spot-checked every numeric example (lines 486–502, 645–651, 821–828, 929–931, 955–957), the Y² identity, the per-box count and the λ_j = m_{n−j} ↔ Γ_n conversion. All are correct.

FINDINGS: 8

**Full report (for coldread-opus.md)**

Cold read, casBound exposition (paper.tex / paper.pdf, 19 pp). Reader: a mathematician who hasn't seen the Lean.

*Where I lost the thread*
- p2–3 (paper.tex:144–186): after a good first paragraph, the "idea in brief" moves into the automorphic application. It packs about 20 Lean line references and undefined terms (coefficient gluing, J^†C_bJ, IsSmall, Kuga argument, cochain differential) into two paragraphs. I couldn't tell which parts I needed.
- p3 (:188–196): it promises an "exterior-transfer derivation below", but there is no such section. The derivation is an aside inside the proof of Proposition 3, and the Lean doesn't use it.
- p3 (:200–227), "Where the hypothesis comes from": it does explain upward closure (ν_τ is nondecreasing, so a column (τ,c) holds a terminal set of labels), but that point is hidden among spherical descent, quantum determinant factors, Hermitian matrix tests and Whittaker transfer.
- p8–9 (:539–575): the proof of Proposition 3 makes the reader go through Cauchy–Schwarz, the transfer square T^†T, the failure of ‖Yf‖≤‖f‖ and a "Heuristic" ("normalized quadratic has leading form Id−Y … leading size s") before the actual argument.

*Terms used before they are defined*
- "terminal intervals" at :121. It is only explained at :766.
- "zero-background slot Casimir" at :140, defined at :236.
- "tensor of highest wedges" at :333 and :927, never defined.
- "row" and "row bound" at :543 and :751. These mean the inner sum Σ_{q∈S_c}R(p,q) for fixed p, which is never said, and "row" clashes with columns.
- "active", "ambient", "trace-form", "label inclusion", "equal-label comparison", "content formula", "Young permutation module", "occurrence": none is explained where it first appears.
- X_{cc′} is defined at :416 only in its "exterior-power realization", but :192 uses it on tensors. It should be defined plainly as Σ_{p∈S_c, q∈S_c′} P_pq.
- "Why the proof is built this way" (:332–350) refers to Propositions 1–9 before any of them is stated, and its bullets don't make sense without them (for example :340–341, "a large negative eigenvalue can rule out a norm contraction").

*Steps whose purpose is not explained in place*
- Proposition 2's proof opens with scalar backgrounds (:484–488). They matter only because of the twist mentioned at :151, and the proof doesn't say so.
- Proposition 2's proof also contains a content-formula and dominance argument (:503–509) that doesn't prove Proposition 2.
- Proposition 7, paragraph 2 (:761–764), on how the bound grows with N>0, N=0 and N<0, is padding.
- The Theorem's proof includes the whole highest-weight proof, which is not in the Lean (:933–945), before the coordinate proof. Readers will mix the two up.

*Where the key idea is buried*
- The terminal-interval fact (:766), and therefore "common labels = min of the heights".
- The heights form of the coefficient (:971–974).
- The one-box identity ‖f‖² − ReΣ⟨f,P_pq f⟩ = ‖f−Yf‖²/(s+1), which appears at :128, again at :193 and in full only at :596.
- Why the bound has to be exact: a positive excess survives the twist and breaks the IsSmall comparison (:171–174). This is the reason the result matters downstream, and it sits inside a sentence full of Lean references.

*My 10-line explanation to a colleague*
1. In each column the labels are distinct and upward closed, so a column of height h has labels n−h,…,n−1.
2. Propositions 1 and 2 expand the Casimir: K = nd·Id + Σ over ordered distinct pairs of P_pq.
3. Same-column swaps act by −1, so the diagonal plus same-column terms give exactly h_c(n+1−h_c) per column.
4. Fix a box p outside column c′ and let Y = Σ_{q∈c′} P_pq. Since f alternates on c′, Y²f = kf − (k−1)Yf.
5. So ‖f‖² − Re⟨f,Yf⟩ = ‖f−Yf‖²/(k+1) ≥ 0. This is the antisymmetrizer on c′∪{p} in disguise.
6. Summing over p in c bounds the cross terms for (c,c′) by h_c‖f‖². By symmetry, use the shorter column as source in both orders: 2·min(h_c,h_c′).
7. The total is Σ h_c(n+1−h_c) + 2Σ_{pairs} min(h_c,h_c′).
8. Written by labels, this is Σ m_i(m_i+2i+1−n). It is the Casimir eigenvalue Γ_n(λ) of the Cartan component of ⊗Λ^{h_c}, so the bound is sharp.
9. The application needs this exact constant because the downstream comparison uses the automorphic Casimir scalar as its ceiling.
10. The paper never puts lines 1, 7–8 and 9 in one place. I had to build them from :766, :971 and :273–279.

*Fixes, ranked by how much they help*
1. Open Section 2 with a short plain-language summary: the terminal-interval structure, the heights form, the "Cartan component" reading, then the one-box identity as the single idea.
2. Move the automorphic material and "Where the hypothesis comes from" to a late section. Keep one sentence up front on why exactness matters. Take the Lean line references out of the running text; the concordance already has them.
3. In each proof, give the argument first and move the alternatives and counterexamples into the Remarks.
4. Present the highest-weight proof and the exterior-transfer calculation as separate "Alternative proof" subsections, marked as not in the Lean.
5. Replace "checked by hand" with "checked by an AI model, not in the Lean".
6. Fix the notation reuse (s, k, n/a, c), define "row bound" and the tensor of highest wedges, and move the Notation table before the Theorem.
7. Cut the citation strings attached to single claims; the nuclear-physics references for a standard projector are the clearest case. Add a short note that the inequality itself is classical.
8. Delete "This is an exposition of…" at :111 (it repeats the heading) and the "also" at :96–97, since Rodgers is already one of the nine write-ups.

What the paper didn't give me: a plain statement of the result I could write down from memory.