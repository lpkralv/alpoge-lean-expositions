Superseded. This is the version 1 exposition source. Version 2 of the paper (paper/paper.pdf) corrects errors found in a release review on 2026-11-27, including a false attribution, claims about certification, grading independence and hand checks; see casbound/review-record/release-review-2026-11-27/. Use version 2.

# The tableau Casimir bound

This is an exposition of the tableau Casimir bound in Levent Alpöge’s 2026 Lean archive, published on 2026-11-20. [Lean archive](https://alpo.ge/lean.tar.gz).

## The idea in brief

Expand the quadratic Casimir in the original tensor coordinates, with the column signs kept in view. Bounding the cross-column transpositions one at a time misses the constraint they share: a whole column of target boxes alternates. The central move is to square the defect of the sum of swaps from one outside box into that column, which bounds the entire sum using the nonnegativity of one squared norm. Symmetry then lets us count from the smaller column in either order, and the terminal intervals of tableau labels turn that count and the exact within-column debit into the multiplicity formula.

The highest-weight proof (not in the Lean; checked by hand) bounds the Casimir scalar on each irreducible summand using dominance of highest weights. In Alpöge’s coordinate proof, for one box outside an alternating column of size \(k\), one forms \(f-Yf\), where \(Y\) sums the swaps of that box with the column. The identity \(\|f\|^2-\operatorname{Re}\langle f,Yf\rangle=\|f-Yf\|^2/(k+1)\) bounds the entire sum using the nonnegativity of one squared norm. The Casimir expansion supplies these sums, and counting from the shorter column combines their bounds with the exact within-column signs to give the coefficient in tableau labels. [Etingof, lectures 18 and 25–26](https://ocw.mit.edu/courses/18-745-lie-groups-and-lie-algebras-i-fall-2020/mit18_745_f20_lec_full.pdf) and [Yang, Ex. 5.4](https://arxiv.org/pdf/2202.12225), [Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf).

The bound assumes a natural-number rank \(n\), a finite slot set \(Q\) and a column set \(C\), each with decidable equality, labels \(b:Q\to\{0,\ldots,n-1\}\) that are distinct and upward closed in each column of \(\mathrm{col}:Q\to C\), a union \(S\) of whole columns, and a complex tensor \(f\) that changes sign under every swap of distinct slots in one column (`StepFormula.lean:88–90`, `KTypeData.lean:51–52`). It bounds the real quadratic form of the zero-background slot Casimir on \(f\) by \(\sum_{i=0}^{n-1}m_i(m_i+2i+1-n)\|f\|^2\), where \(m_i\) counts slots in \(S\) with label \(i\) (`StepFormula.lean:91–94`). In the automorphic application, the \(K\)-type construction supplies the slots and tableau with an embedding label constant on each column and a formula for each embedding’s label counts in terms of the infinitesimal weights, while the cochain construction carries the tensor’s swap signs to the cochain values (`KTypeHolds.lean:27`, `KTypeData.lean:104–111`, `IsStarRep.lean:88–93`). The Lie-action formula uses the fiber \(S\) of each embedding, which is a union of columns, and the shift identities show how the diagonal twist \(s\) contributes \(-2s|S|+ns^2\) and how the corrected multiplicity sum becomes the quadratic Casimir scalar of the infinitesimal weights (`KTypeData.lean:60`, `IsStarRep.lean:75–80,95–98`, `SumFinVal.lean:33–37,111–114`). The archive passes the universal bound to coefficient gluing, whose output is an algebraic coefficient representation with the required trace and Casimir comparisons and a nonzero cochain (`ClozelCohomologicalOfThree.lean:11`, `ClozelCohomologicalOfRest.lean:19–21`, `IsStarRep.lean:102`, `ClozelCohomologicalOf.lean:37–49`). At rank \(a\), coefficient gluing takes slots \(\mathrm{Fin}(q)\), column indices \(\mathbb N\), the supplied column and label maps, \(S=\mathrm{fib}(\mathrm{lab},\tau)\), and \(f=Jv\) for each coefficient vector \(v\). Intertwining expresses the coefficient Casimir as \(J^\dagger C_bJ\), where \(C_b\) is the twisted ambient Casimir at \(\tau\), and the isometry gives \(\|Jv\|^2=\|v\|^2\). The coefficient quadratic form on \(v\) is thus the ambient form on \(Jv\). Adding the twist correction \((-2s|S|+as^2)\|v\|^2\) to the zero-background bound makes the right-hand side \(c_\tau\|v\|^2\), where \(c_\tau\) is the automorphic Casimir scalar (`CoefGlueHolds.lean:120–150`, `SumFinVal.lean:111–114`). The `IsSmall` comparison uses this same \(c_\tau\) as its ceiling, and a positive excess in the tableau coefficient would survive the twist and leave the estimate too weak for nonzero \(v\) (`ClozelCohomologicalOf.lean:39–43`). The separate Kuga argument uses unitarity up to twist and the opposite trace scalars to express its Casimir difference as twice the sum of the coefficient-minus-automorphic differences. The fiberwise upper bound makes this form nonpositive on the tensor product. Positivity then forces the cochain differential to vanish in every degree, and the nonzero cochain yields cohomology (`KgCasDiff.lean:37–52`, `KugaGlueHolds.lean:15–21,80–100`, `KugaAbsHolds.lean:137–181`, `IsStarRep.lean:67–70`). The assembled theorem gives cohomologicality for regular algebraic cuspidal representations of positive rank over totally complex number fields (`ClozelCohomologicalOf.lean:55–63`, `ClozelCohomological.lean:8–9`, `ClozelCohomologicalModel.lean:10–12`).

The exterior-transfer derivation below combines Lévy’s slot expansion with Howe’s exterior-algebra action. The calculation in Proposition 3 expresses the deficit for each pair of alternating columns as the squared norm of a transfer out of the shorter column. In tensor coordinates, for a source column \(c\) and a target column \(c'\) of height \(k=h_{c'}\), the pair deficit is \(h_c\|f\|^2-\operatorname{Re}\langle f,X_{cc'}f\rangle=\frac{1}{k+1}\sum_{p\in S_c}\|f-Y_pf\|^2\), where \(Y_p=\sum_{q\in S_{c'}}P_{pq}\). The Lean proof uses this normalization for the one-box inequality and the inherited labels of whole selected columns to express the bound in label multiplicities. [Lévy, Prop. 2.2](https://arxiv.org/pdf/math/0703690) and [Cautis, Kamnitzer and Morrison, §4.2](https://arxiv.org/pdf/1210.6437), [Howe, Theorem 8 and the exterior-algebra example](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf).

## Where the hypothesis comes from

For a regular algebraic cuspidal representation, the \(K\)-type construction sorts the distinct integer weights at each embedding \(\tau\) in decreasing order \(l_\tau(w_\tau(i))\), and sets \(s=\sum_{\tau,k}|l_\tau(k)|\), so the integer gaps make \(\nu_\tau(i)=s-l_\tau(w_\tau(i))-i\) nonnegative and nondecreasing in \(i\). The finite slots are triples \((\tau,i,c)\) with \(0\le c<\nu_\tau(i)\), numbered as \(\mathrm{Fin}(q)\), with natural-number column code for \((\tau,c)\) and label \(i\), so a label determines at most one slot per column and raising the label keeps the same column available. The archive adds two copies of the pairs \(c<i\) indexed by one embedding from each conjugate pair. The two copies together add \(i\) occurrences of label \(i\) at each embedding \(\tau\), giving the enlarged multiplicity \(\nu_\tau(i)+i=s-l_\tau(w_\tau(i))\). Each transferred quantum determinant factor \(u+l_\tau(w_\tau(i))+\nu_\tau(i)+i\) is therefore \(u+s\). Spherical descent uses the resulting eigenvalue \((u+s)^n\) to obtain a compact-fixed tensor. The archive takes its signed column sum, whose terms a same-column transposition reindexes with opposite sign. The slot data for the Casimir bound use the original multiplicities \(\nu_\tau(i)\). Contracting the added pairs against Hermitian matrix entries and alternating the arguments carries every original-slot sign to the cochain values, since a swap of original slots affects only the input tensor, and Hermitian matrix tests detect the nonzero paired alternation. Evaluating a cochain value at a nonzero coordinate and choosing a complex linear functional that detects it gives a nonzero scalar tensor with those signs, and the ambient tensor action preserves the column-alternating space by commuting with swaps of slots labeled by the same embedding. The archive chooses a stable subspace of least dimension inside that alternating space with nonzero pairing against the scalar tensor, and uses an orthonormal basis to embed every coefficient vector \(v\) as a column-alternating tensor \(Jv\). Coefficient gluing applies the bound at the positive automorphic rank with these slots, columns, labels and \(f=Jv\), taking \(S\) to be each embedding fiber, which is a union of whole columns because the column code fixes the embedding. The proof of simultaneous Whittaker transfer, the individual steps of the spherical descent and the Young contraction proof used to ensure nonzero paired alternation are outside the scope of this exposition.

## Theorem

In the statement below, \(L_n=\{0,\ldots,n-1\}\), with \(L_0=\varnothing\), and \(\mathcal V=\mathbb C^{L_n^Q}\) has the coordinate Hermitian inner product. Here \(L_n^Q\) is the set of assignments \(x:Q\to L_n\). For \(p,q\in Q\), \(P_{pq}\) interchanges the two slots, so \((P_{pq}f)(x)=f(x\circ(p\,q))\), including \(P_{pp}=\mathrm{Id}\). The operator \(E^{(p)}_{ii'}\) is the matrix unit \(e_{i'}\mapsto e_i\) in slot \(p\), acting as the identity in all other slots. The Casimir is \(K=\sum_{i,i'\in L_n}G_{ii'}G_{i'i}\) with \(G_{ii'}=\sum_{p\in S}E^{(p)}_{ii'}\), and \(m_i=|\{p\in S:b(p)=i\}|\).

**Theorem 10 (tableau Casimir bound).**

\[
\begin{gathered}
\text{For every }n\in\mathbb Z_{\ge0},\ \text{finite set }Q,\ \text{set }C,\
\gamma:Q\to C,\ b:Q\to L_n,\ S\subseteq Q,\ f\in\mathcal V,\ \text{assume}\\
\forall p,q\in Q,\quad
  \gamma(p)=\gamma(q)\ \land\ b(p)=b(q)\ \Longrightarrow\ p=q,\\
\forall p\in Q,\ \forall i\in L_n,\quad
  b(p)<i\ \Longrightarrow\ \exists q\in Q:\ \gamma(q)=\gamma(p),\ b(q)=i,\\
\forall p,q\in Q,\quad
  \gamma(p)=\gamma(q)\ \Longrightarrow\ (p\in S\ \Longleftrightarrow\ q\in S),\\
\forall p,q\in Q,\quad
  \gamma(p)=\gamma(q)\ \land\ p\ne q\ \Longrightarrow\ P_{pq}f=-f.
\\[3pt]
\text{Then}\qquad
\operatorname{Re}\langle f,Kf\rangle
\le \left(\sum_{i\in L_n}m_i(m_i+2i+1-n)\right)\|f\|^2 .
\end{gathered}
\]

The hypotheses are distinctness and upward closure of the tableau labels, selection by whole columns, and alternation of the tensor within every column. They are structural hypotheses of the inequality. No conjecture or separate theorem is assumed. When \(S=\varnothing\) the generators and the multiplicities vanish, and when \(f=0\) both quadratic forms vanish. For \(n=0\) the label map forces \(Q=\varnothing\), so the same empty-selection case applies.

## Literature context

**Whole-space inequality (Theorem 10).** The highest-weight proof (not in the Lean; checked by hand) gives the full inequality by comparing irreducible summands. Alpöge’s coordinate proof bounds the quadratic form on the given tensor itself. The active alternating space identifies with the tensor product of the column exterior powers, with the factors outside \(S\) carried along by the identity. In reversed basis order its highest constituent has row lengths \(\lambda_j=m_{n-j}\) for \(1\le j\le n\), and the trace-form eigenvalue \(\Gamma_n(\lambda)=\sum_{j=1}^n\lambda_j(\lambda_j+n+1-2j)\) is the displayed coefficient. Constituent dominance and orthogonal decomposition give the upper bound for all alternating tensors. The normalization is for \(\mathfrak{gl}_n\), including the scalar direction. For \(n>0\) the trace-form \(\mathfrak{sl}_n\) operator would subtract \(d^2/n\) times the identity, where \(d=|S|\). [Exterior Pieri, Proposition 2.1](https://math.mit.edu/~apost/papers/LR.pdf), [Highest-weight theory, lectures 18 and 25–26](https://ocw.mit.edu/courses/18-745-lie-groups-and-lie-algebras-i-fall-2020/mit18_745_f20_lec_full.pdf), [Casimir normalization, Example 5.4](https://arxiv.org/pdf/2202.12225), [Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf), [Baur, §1](https://imsc.uni-graz.at/baur/Articles/Cartan/tg.pdf), [Cartan component, Baur’s thesis, Proposition 3.2](https://edoc.unibas.ch/entities/publication/1af5150b-0f45-4b80-b0b4-843a4b08af55/full).

The transposition-content formula gives another route once the signed column condition restricts the allowed shapes. The necessity of dominance in the permutation-module occurrence theorem suffices after twisting by the sign character and conjugating partitions. The converse, established in the literature on Young permutation modules, gives a full occurrence criterion. Proposition 2 converts the content sums to trace-form eigenvalues, which the dominance comparison in Theorem 10 bounds by \(\Gamma_n(\lambda)\). A second route works pairwise on exterior powers: the transfer-square calculation in Proposition 3 gives the two height bounds on a column interaction. [Permutation-module occurrence, introduction and references](https://ir.cwi.nl/pub/10134/10134D.pdf), [Permutation representations, §6](https://ir.cwi.nl/pub/10125/10125D.pdf), [Transposition contents, Okounkov–Vershik, (2.1) and Proposition 6.2](https://www.esi.ac.at/preprints/esi333.pdf), [Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437), [Frobenius’s character formula, §2](https://faculty.fordham.edu/dswinarski/snchar/Frobenius1900.pdf), [Cesi, transposition class sum, (4.1) and Proposition 4.1, and cross-block spectrum, (4.2) and Theorem 5.3, (5.9)](https://arxiv.org/pdf/0902.0727), [Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf).

**Slot expansion (Propositions 1–2).** Lévy contracts the matrix units into diagonal terms and swaps. Szőke uses the negative internal signs on Young-symmetrized tensors. Column alternation alone gives these signs in Alpöge’s proof. [Lévy, Prop. 2.2](https://arxiv.org/pdf/math/0703690) and [Szőke, §§III–IV](https://www.researchgate.net/publication/327777204_Eigenvalues_of_the_quadratic_Casimir_operator_of_SUn_in_Young_tableaux_representation).

**One-box defect (Proposition 3).** On a tensor already alternating on the target, dividing the defect by \(k+1\) projects onto tensors alternating on the enlarged set. Alpöge’s coordinate proof derives the norm identity by multiplying swaps. The one-column factor in Jucys’s factorization or Molev’s branching formula gives this projector. [Navrátil, Kamuntavičius and Barrett, three-particle antisymmetrizer (30) and compressed matrix elements (35)](https://arxiv.org/pdf/nucl-th/9907054) and [Molev, eqs. (7)–(9)](https://arxiv.org/pdf/math/0612207), [Jucys, eq. (3)](https://ncatlab.org/nlab/files/Jucys-1971.pdf), [Navrátil and Barrett, four-particle case, (15) and the paragraph after (19)](https://arxiv.org/pdf/nucl-th/9812062).

**Summing into a column (Propositions 3 and 8).** The enlarged-set projector bounds the sum from one box. On two exterior powers, the transfer-square calculation in Proposition 3 gives the same smaller-height estimate for the entire pair. Alpöge’s proof sums the one-box inequality in the original slots. [Navrátil, Kamuntavičius and Barrett, three-particle antisymmetrizer (30) and compressed matrix elements (35)](https://arxiv.org/pdf/nucl-th/9907054) and [Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437), [Navrátil and Barrett, four-particle case, (15) and the paragraph after (19)](https://arxiv.org/pdf/nucl-th/9812062), [Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf).

**Choosing the source column (Propositions 6–8).** The calculation in Proposition 3 gives a height bound in each transfer direction. The shorter height counts common rows. Alpöge’s proof uses inclusion of the inherited label intervals to choose the source for both orders of the swap sum. [Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437) and [Macdonald, ch. I, §1](https://math.berkeley.edu/~corteel/MATH249/macdonald.pdf), [Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf).

**Recovering the coefficient (Propositions 4, 5 and 9).** The row-and-column Casimir formula gives the coefficient after adjusting the scalar direction. In Alpöge’s proof, upward closure supplies a box in the same column for each higher label, and whole-column selection puts each such box in \(S\). Gross’s earlier derivation also counts overlaps by pairing indicators for nested rows of the diagram. [Gross and Taylor, eqs. (2.1)–(2.2)](https://arxiv.org/pdf/hep-th/9301068) and [Macdonald, ch. I, §1](https://math.berkeley.edu/~corteel/MATH249/macdonald.pdf), [Gross, Appendix A.1](https://arxiv.org/pdf/hep-th/9212149).

## Why the proof is built this way

- Theorem 10 bounds every column-alternating tensor. Evaluating the Casimir on the tensor of highest wedges tests a single vector.
- Propositions 1 and 2 expand the operator, and Proposition 9 retains the column signs, since an active column of height at least two excludes the fully symmetric active tensors that attain the ambient maximum.
- Proposition 3 groups swaps into one target column, since estimating them individually charges a product of column heights.
- Proposition 3 squares the defect, since a large negative eigenvalue can rule out a norm contraction while helping the upper bound.
- Proposition 7 uses symmetry and label inclusion to obtain both ordered bounds from the smaller source, since the fixed orientations give a sum of heights.
- Proposition 6 groups the cross-column terms before applying the equal-label comparison of Propositions 7 and 8, since individual unequal-label swaps can have positive expectation.
- Proposition 4 uses whole columns, and Proposition 9 combines its count with the count in Proposition 5, since arbitrary selections can leave holes above selected labels and invalidate the multiplicity formula.

## Notation

All sums over slots and columns are finite. The column-index set \(C\) itself may be arbitrary. A displayed family indexed by \(c\) or \(i\) uses the same convention at any other index of the corresponding type.

| Symbol | Meaning |
| --- | --- |
| \(n\) | Nonnegative dimension of the one-slot space. |
| \(L_n\) | Label and coordinate-value set \(\{0,\ldots,n-1\}\), empty at \(n=0\). |
| \(Q\) | Finite set of tensor slots or boxes. |
| \(p\), \(q\), \(q'\), \(p_1\), \(p_2\), \(p_3\), \(p_*\) | Boxes in \(Q\), with \(p_*\) the witness box in Proposition 7. |
| \(C\) | Set of column indices. |
| \(\gamma\) | Map assigning each box its column. |
| \(c\), \(c'\) | Column indices. |
| \(S\) | Set of selected boxes. |
| \(d\) | Number of selected boxes, \(\lvert S\rvert\). |
| \(S_c\) | Selected boxes in column \(c\), namely \(\{p\in S:\gamma(p)=c\}\). |
| \(C_S\) | Set of active column indices, \(\gamma(S)\). |
| \(h_c\) | Height of selected column \(c\), namely \(\lvert S_c\rvert\). |
| \(\ell_c\) | Least label in \(S_c\), defined as \(n\) if \(S_c\) is empty. |
| \(b\) | Fixed tableau label map \(Q\to L_n\). |
| \(i\), \(i'\), \(i_*\) | Values in \(L_n\). The value \(i_*\) is the witness label \(b(p_*)\). |
| \(m_i\) | Number of selected boxes with tableau label \(i\). |
| \(\mathcal T(\gamma,b)\) | Tableau condition. Two boxes in the same column with the same label coincide, and for every \(p\in Q\) and \(i\in L_n\) with \(b(p)<i\) there is \(q\in Q\) with \(\gamma(q)=\gamma(p)\) and \(b(q)=i\). |
| \(\mathcal U(\gamma,S)\) | Whole-column selection. For all \(p,q\in Q\) with \(\gamma(p)=\gamma(q)\), membership of \(p\) and \(q\) in \(S\) is equivalent. |
| \(x\) | Variable coordinate assignment \(Q\to L_n\), varied independently of \(b\). |
| \(x[p\leftarrow i']\) | Assignment obtained from \(x\) by replacing its value at \(p\) by \(i'\). |
| \(e_i\) | Standard basis vector of \(\mathbb C^n\) with index \(i\). |
| \(\mathcal V\) | Space \(\mathbb C^{L_n^Q}\) of complex-valued tensor coordinates, with the coordinate Hermitian inner product. |
| \(f\) | Tensor in \(\mathcal V\). |
| \(\langle\cdot,\cdot\rangle\) | Hermitian inner product, conjugate-linear in its first argument and linear in its second. |
| \(\|\cdot\|\) | Norm induced by that inner product. |
| \(\operatorname{Re}\) | Real part of a complex scalar. |
| \(\lvert010\rangle\), \(\lvert100\rangle\), \(\lvert001\rangle\) | Coordinate basis tensors for the indicated triples of coordinate values in the designated slot order. |
| \(\mathrm{Id}\) | Identity on the operator's underlying space. |
| \((p\,q)\) | Transposition of slots \(p,q\), with the identity convention for \(p=q\). |
| \(P_{pq}\) | Tensor operator of \((p\,q)\), sending \(f(x)\) to \(f(x\circ(p\,q))\) at coordinate \(x\). |
| \(E^{(p)}_{ii'}\) | Matrix unit in slot \(p\), taking \(e_{i'}\) to \(e_i\) in that slot. |
| \(G_{ii'}\) | Sum of the matrix units \(E^{(p)}_{ii'}\) over selected slots. |
| \(K\) | Trace-form quadratic Casimir \(\sum_{i,i'\in L_n}G_{ii'}G_{i'i}\) with zero scalar background. |
| \(z_{ii'}\), \(z\) | Scalar background entries for the comparison in Proposition 2, with \(z=z_{00}\) when \(n=1\). |
| \(B\) | Set of target slots for the one-box estimate. |
| \(s\) | Number of slots in \(B\). |
| \(Y\) | Sum of the swaps \(P_{pq}\) from the outside slot \(p\) into \(B\). |
| \(g\) | Defect \(f-Yf\). |
| \(N\) | Real scale in the counting argument, specialized to \(\|f\|^2\) in the Casimir application. |
| \(R\) | Real symmetric kernel in the counting argument, specialized to \(\operatorname{Re}\langle f,P_{pq}f\rangle\) at \((p,q)\). |
| \(F\) | Arbitrary real kernel for the reindexing identity. |
| \(\mathbf 1\) | Indicator of the subscripted condition. |
| \(X_{cc'}\) | Cross-column interaction, the sum of swaps between the two factors in their exterior-power realization. |
| \(\lambda\) | Highest weight of the tensor of highest wedges, with row lengths \(\lambda_j=m_{n-j}\). |
| \(\mu\) | Highest weight of a constituent of the tensor product of the active exterior powers. |
| \(j\) | Row or coordinate index of a weight, starting at \(1\). |
| \(k\) | Length of a weight prefix, from \(1\) through \(n\). |
| \(\Gamma_n\) | Trace-form eigenvalue function on highest weights, specified in the literature context. |
| \(D_k\) | Difference between the length-\(k\) prefix sums of \(\lambda\) and \(\mu\). |
| \(v_j\) | Coefficient \(\lambda_j+\mu_j+n+1-2j\) in the comparison of the trace-form eigenvalues. |
| \(\mathfrak{gl}_n\), \(\mathfrak{sl}_n\) | Lie algebras of all and of traceless complex \(n\times n\) matrices, respectively. |
| \(\mathbb Z_{\ge0}\), \(\mathbb R\), \(\mathbb C\) | Nonnegative integers, real numbers, and complex numbers, respectively. |

## Proposition 1. Contraction of two slot matrix units

\[
\begin{gathered}
\text{For every }n\in\mathbb Z_{\ge0},\ \text{finite set }Q,\
p,q\in Q,\ f\in\mathcal V,\ x\in L_n^Q,\\
\sum_{i,i'\in L_n}\bigl(E^{(p)}_{ii'}E^{(q)}_{i'i}f\bigr)(x)
=
\begin{cases}
n f(x),&p=q,\\
f(x\circ(p\,q)),&p\ne q .
\end{cases}
\end{gathered}
\]

**Proof.** By the matrix-unit action, the outer operator forces \(i=x(p)\) and reads the intermediate assignment \(x[p\leftarrow i']\), obtained by replacing the value at \(p\) by \(i'\). The inner operator contributes only when that intermediate assignment has value \(i'\) at \(q\), and then replaces the value at \(q\) by \(i\).

When \(p=q\) the first replacement makes the inner condition automatic for all \(n\) values of \(i'\), and the second restores \(i=x(p)\), giving \(n f(x)\). When \(p\ne q\) the first replacement leaves \(x(q)\) intact, so the inner condition forces \(i'=x(q)\) and exactly one term survives. Its replacements put the original value of each slot in the other slot and preserve the entire assignment elsewhere. Even if \(x(p)=x(q)\), there is still only one contributing term, because the two slots are distinct.

**Remarks.** For \(n=0\) and a nonempty slot set, there is no assignment at which to evaluate the identity. At \(n=1\) the two branches have the same scalar effect.

## Proposition 2. Slot expansion of the zero-background Casimir

\[
\begin{gathered}
\text{For every }n\in\mathbb Z_{\ge0},\ \text{finite set }Q,\ S\subseteq Q,\\
K=nd\,\mathrm{Id}+
\sum_{p\in S}\ \sum_{\substack{q\in S\\q\ne p}}P_{pq}.
\end{gathered}
\]

**Proof.** The generators here have zero scalar background. If a scalar background \(z_{ii'}\mathrm{Id}\) were added, the mixed terms and the product of backgrounds would also enter the expansion. For example, with \(n=1\), \(S\) a singleton and \(z_{00}=z\), the sole generator would be \((1+z)\mathrm{Id}\) and its square \((1+z)^2\mathrm{Id}\), giving \(\mathrm{Id}\) at \(z=0\) and \(4\mathrm{Id}\) at \(z=1\).

Distribute the two sums over \(S\) in each product and group the matrix-index contraction by the ordered slot pair \((p,q)\). Proposition 1 gives \(n\,\mathrm{Id}\) at \(p=q\) and \(P_{pq}\) at \(p\ne q\). Isolating \(n\,\mathrm{Id}\) per box leaves exactly the distinct ordered pairs needed for the count. Including \(P_{pp}\) in addition to the scalar term adds \(d\,\mathrm{Id}\), whereas replacing the scalar term by \(\sum_{p\in S}P_{pp}\) loses \((n-1)d\,\mathrm{Id}\). A singleton selection has operator \(n\,\mathrm{Id}\), and at \(n=1\) the diagonal swap alone happens to give the right scalar.

The ordered transposition sum on the entire active tensor power has largest eigenvalue \(d(d-1)\) for \(n>0\), attained on fully symmetric tensors. Adding the diagonal term gives the ambient Casimir maximum \(nd+d(d-1)\). With a single active column of height \(d\le n\), every distinct swap acts by \(-1\) and the exact coefficient is \(nd-d(d-1)\). Thus the ambient estimate has excess \(2d(d-1)\), giving \(6\) versus \(2\) at \(n=d=2\). The content formula applies once the allowed shapes are restricted. Twisting the Young permutation module associated with the sorted column heights by the sign character converts occurrence to the column-sign condition, and dominance necessity, followed by conjugation of partitions, leaves only shapes dominated by \(\lambda\). On each such shape \(\mu\), doubling the content sum and adding \(nd\) gives the trace-form eigenvalue \(\Gamma_n(\mu)\). The dominance comparison in Theorem 10 gives \(\Gamma_n(\mu)\le\Gamma_n(\lambda)\), so a full occurrence criterion is unnecessary. The slot argument carries the signs directly into Proposition 9. [Schur–Weyl duality, Theorem 27.3](https://ocw.mit.edu/courses/18-755-lie-groups-and-lie-algebras-ii-spring-2024/mit18_755_s24_lec01.pdf), [Permutation-module occurrence, §6](https://ir.cwi.nl/pub/10125/10125D.pdf), [Macdonald, dominance reversal in I.1, (1.11), and sign twist in I.7, Example 2](https://math.berkeley.edu/~corteel/MATH249/macdonald.pdf), [Transposition contents, Okounkov–Vershik, (2.1) and Proposition 6.2](https://www.esi.ac.at/preprints/esi333.pdf), [Frobenius’s character formula, §2](https://faculty.fordham.edu/dswinarski/snchar/Frobenius1900.pdf), [Cesi, transposition class-sum scalar, (4.1) and Proposition 4.1](https://arxiv.org/pdf/0902.0727).

**Remarks.** There are \(d(d-1)\) ordered off-diagonal terms. Each unordered pair contributes its swap twice. Empty \(S\) makes both terms of the expansion zero.

## Proposition 3. Swaps from one outside box into an alternating set

\[
\begin{gathered}
\text{For every }n\in\mathbb Z_{\ge0},\ \text{finite set }Q,\
B\subseteq Q,\ p\in Q\setminus B,\ f\in\mathcal V,\\
\left(\forall q,q'\in B,\quad q\ne q'\ \Longrightarrow\ P_{qq'}f=-f\right)
\ \Longrightarrow\
\sum_{q\in B}\operatorname{Re}\langle f,P_{pq}f\rangle\le\|f\|^2.
\end{gathered}
\]

**Proof.** Estimating each matrix element by Cauchy–Schwarz, using that each swap is unitary, gives only \(s\|f\|^2\) for \(s=|B|\). This agrees with the desired bound at \(s=1\) and loses \((s-1)\|f\|^2\) for \(s>1\). For columns of heights \(h_c,h_{c'}\), summing those separate estimates costs \(2h_ch_{c'}\|f\|^2\) in the two orders. Grouping the swaps into a row costs one squared norm per source box and ultimately gives \(2\min(h_c,h_{c'})\|f\|^2\). At equal heights the separate and grouped coefficients are \(2h_c^2\) and \(2h_c\), respectively. The exterior approach also obtains this pair bound. The calculation below relates the interaction \(X_{cc'}\) on two wedges to the positive transfer squares \(h_c\mathrm{Id}-X_{cc'}\) and \(h_{c'}\mathrm{Id}-X_{cc'}\). The one-box estimate uses only the target’s alternation and applies to any set \(B\), a convenience since the application takes \(B=S_c\) for a column other than the source column. [Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437), [Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf).

To compute the first transfer square, write \(A_i\) for contraction by \(e_i\) and \(A_i^\dagger\) for exterior multiplication by \(e_i\). The transfer from \(c\) to \(c'\) is \(T=\sum_i A_i\otimes A_i^\dagger\). Using \(A_iA_j^\dagger=\delta_{ij}\mathrm{Id}-A_j^\dagger A_i\) and \(\sum_i A_i^\dagger A_i=h_c\mathrm{Id}\) on the source wedge gives \(T^\dagger T=h_c\mathrm{Id}-\sum_{i,j} A_i^\dagger A_j\otimes A_j^\dagger A_i\). The operator \(A_i^\dagger A_j\) is the matrix unit acting on the wedge, so the sum is \(X_{cc'}\) by the matrix-unit contraction of Proposition 1. Reversing the transfer gives the square with \(h_{c'}\).

Set \(Y=\sum_{q\in B}P_{pq}\). A bound \(\|Yf\|\le\|f\|\) could give the desired upper bound by Cauchy–Schwarz, but when \(n\ge s+1\) there are nonzero tensors fully alternating on \(B\cup\{p\}\), on which \(Yf=-sf\). Their norm ratio is \(s\), which exceeds \(1\) for \(s>1\), though their expectation is already below the upper bound. The sign needed is that of \(\operatorname{Re}\langle f,f-Yf\rangle\). The exterior transfers certify a one-sided bound on a pair of wedges. The one-box calculation below uses the square with just one source box and one target set.

Heuristic: As the target size \(s\) grows, the separate upper estimate grows linearly in \(s\), and the fully alternating example has expectation \(-s\|f\|^2\). In the square of the swap sum there are \(s\) diagonal terms and \(s(s-1)\) off-diagonal terms, with a minus sign and multiplicity \(s-1\) per target in the latter. Coefficient by coefficient, the normalized quadratic has leading form \(\mathrm{Id}-Y\) on \(f\), and the squared-defect formula will divide by a factor of leading size \(s\).

The exact product identity for distinct \(q,q'\in B\) is \(P_{pq}P_{pq'}=P_{pq'}P_{qq'}\), the transposition relation on three distinct slots. It places the internal swap next to \(f\), giving \(-P_{pq'}f\), and the \(s\) diagonal products give \(sf\). Each \(q'\) appears \(s-1\) times in the off-diagonal part, so
\[
Y^2 f=sf-(s-1)Yf .
\]
This identity yields a constant independent of \(s\). The calculation uses \(p\notin B\). If \(p\in B\) with \(s\ge1\), the self-swap is the identity and the other \(s-1\) swaps negate \(f\), so \(Yf=(2-s)f\). The inequality still holds there, but at \(s=2\) with \(f\ne0\) the quadratic identity would predict \(Y^2f=2f\) instead of zero.

Set \(g=f-Yf\). The product identity gives \(Yg=-sg\). Each term of \(Y\) is a self-adjoint involution, so \(Y\) is self-adjoint and
\[
\begin{aligned}
\|g\|^2
 &=\operatorname{Re}\langle(\mathrm{Id}-Y)f,g\rangle
  =\operatorname{Re}\langle f,(\mathrm{Id}-Y)g\rangle
  =(s+1)\operatorname{Re}\langle f,g\rangle,\\
\|f\|^2-\sum_{q\in B}\operatorname{Re}\langle f,P_{pq}f\rangle
 &=\frac{\|f-Yf\|^2}{s+1}\ge0 .
\end{aligned}
\]
The division works for every \(s\ge0\). At \(s=0\) the sum is zero, \(g=f\), and the divisor is \(1\). Equality holds exactly when \(Yf=f\), and on a tensor fully alternating on \(B\cup\{p\}\) one has \(g=(s+1)f\). The squared norm \(\|Yf\|^2\) alone gives no sign for the difference.

**Remarks.** The same squared-defect identity follows from the orthogonal antisymmetrizer on \(B\cup\{p\}\). Its signed group average splits into \(s+1\) cosets of the subgroup permuting \(B\), represented by the identity and the swaps \(P_{pq}\). On a vector alternating on \(B\) the average equals \((f-Yf)/(s+1)\), so the equality comes from the norm identity for an orthogonal projection.

## Proposition 4. The number of higher labels in a selected column

\[
\begin{gathered}
\text{For every }n\in\mathbb Z_{\ge0},\ \text{finite set }Q,\ \text{set }C,\
\gamma:Q\to C,\ b:Q\to L_n,\ S\subseteq Q,\ p\in S,\\
\mathcal T(\gamma,b)\ \land\ \mathcal U(\gamma,S)
\ \Longrightarrow\
|\{q\in S:\gamma(q)=\gamma(p),\ b(q)>b(p)\}|=n-1-b(p).
\end{gathered}
\]

**Proof.** The strict cutoff \(b(p)\) identifies the increasing ordering of each distinct same-column pair. Using a weak inequality counts \(p\) itself and raises the answer by one. A common cutoff would give the same count for every box in a column containing all labels, whereas the count at label \(0\) is \(n-1\) and the count at label \(n-1\) is \(0\).

Map each selected box in the given column whose label exceeds \(b(p)\) to its label. Injectivity alone gives an upper bound on the number of such boxes. For the upper Casimir estimate this goes in the wrong direction, because the count is multiplied by \(-2\|f\|^2\). Upward closure supplies a box for every label in \(L_n\) above \(b(p)\), and whole-column selection puts each such box in \(S\). The map is thus a bijection onto the \(n-1-b(p)\) labels \(b(p)+1,\ldots,n-1\).

Consider using the same multiplicity formula after arbitrary selection inside a column. At \(n=2\), take an ambient column with labels \(0,1\) and select only its label-\(0\) box. The selected box has zero selected boxes above it, although \(n-1-b(p)=1\). A nonzero alternating tensor on the ambient column exists, and by Proposition 2 the singleton Casimir is \(2\,\mathrm{Id}\). The original selected label gives \(m_0=1\), \(m_1=0\), so the proposed bound would read \(2\|f\|^2\le0\). The height expression from the two-column exterior calculation assigns a singleton of height \(1\) the coefficient \(1(2+1-1)=2\). Its height remains valid for that selection, while the retained label \(0\) fails to encode the terminal interval for height \(1\). [Lévy, Prop. 2.2](https://arxiv.org/pdf/math/0703690) and [Gross and Taylor, eqs. (2.1)–(2.2)](https://arxiv.org/pdf/hep-th/9301068), [Gross, Appendix A.1](https://arxiv.org/pdf/hep-th/9212149).

**Remarks.** In a variant (not in the Lean; checked by hand), selecting terminal subcolumns would preserve both the upward count and the nested-label comparison below. The whole-column hypothesis ensures these properties directly. At \(n=0\) there is no \(p\in S\) in the proposition.

## Proposition 5. The number of equal labels in other columns

\[
\begin{gathered}
\text{For every }n\in\mathbb Z_{\ge0},\ \text{finite set }Q,\ \text{set }C,\
\gamma:Q\to C,\ b:Q\to L_n,\ S\subseteq Q,\ p\in S,\\
\mathcal T(\gamma,b)
\ \Longrightarrow\
m_{b(p)}=1+|\{q\in S:\gamma(q)\ne\gamma(p),\ b(q)=b(p)\}|.
\end{gathered}
\]

**Proof.** Partition the selected boxes of label \(b(p)\) into those in the column of \(p\) and those in other columns. The first part contains \(p\) because \(p\in S\), and label injectivity makes it a singleton. Subtracting one therefore removes exactly \(p\). When \(m_{b(p)}=1\), there is no other-column match. Using \(m_{b(p)}\) as the other-column count would add one charge \(N\) per box, hence \(dN\) overall. If \(p\notin S\), the same-column part is empty and the other-column count is \(m_{b(p)}\).

**Remarks.** The hypothesis includes upward closure as part of the tableau condition, although this count uses only injectivity in each column. The subset \(S\) need not be a union of whole columns here.

## Proposition 6. Partition of cross-column pairs

\[
\begin{gathered}
\text{For every finite set }Q,\ \text{set }C,\ \gamma:Q\to C,\
S\subseteq Q,\ F:Q\times Q\to\mathbb R,\\
\sum_{p\in S}\ \sum_{\substack{q\in S\\\gamma(q)\ne\gamma(p)}}F(p,q)
=
\sum_{c\in C_S}\ \sum_{\substack{c'\in C_S\\c'\ne c}}
\ \sum_{p\in S_c}\ \sum_{q\in S_{c'}}F(p,q).
\end{gathered}
\]

**Proof.** Each ordered cross-column pair belongs to the unique product \(S_c\times S_{c'}\) with \(c=\gamma(p)\) and \(c'=\gamma(q)\). For distinct column indices, every pair in that product passes the cross-column test. For equal indices, the whole product is omitted by that test, including pairs of distinct boxes. This partitions exactly the domain of the sum. The use of an arbitrary kernel is a convenience: the proof needs the same partition for \(F(p,q)=R(p,q)\) and for \(F(p,q)=N\mathbf 1_{b(p)=b(q)}\), so the two sums can be compared on identical ordered column pairs in a single grouping step.

**Remarks.** The reindexing depends only on the column map and the chosen subset. If \(S=\varnothing\), then \(C_S=\varnothing\) and both sums are zero.

## Proposition 7. Comparison for two distinct columns

\[
\begin{gathered}
\text{For every }n\in\mathbb Z_{\ge0},\ \text{finite set }Q,\ \text{set }C,\
\gamma:Q\to C,\ b:Q\to L_n,\ S\subseteq Q,\
R:Q\times Q\to\mathbb R,\ N\in\mathbb R,\\
\text{assume }\mathcal T(\gamma,b),\quad\mathcal U(\gamma,S),\quad
\forall p,q\in Q,\quad R(p,q)=R(q,p),\\
\forall p\in S,\ \forall c\in C\setminus\{\gamma(p)\},\qquad
\sum_{q\in S_c}R(p,q)\le N.
\\
\text{Then for every }c,c'\in C\text{ with }c\ne c',\\
\sum_{p\in S_c}\sum_{q\in S_{c'}}R(p,q)
\le\sum_{p\in S_c}\sum_{q\in S_{c'}}N\mathbf 1_{b(p)=b(q)} .
\end{gathered}
\]

**Proof.** Applying the row bound in the displayed order gives \(h_cN\), and in the reverse order it gives \(h_{c'}N\). For \(N>0\) and \(h_c>h_{c'}\), the first estimate overcharges by \((h_c-h_{c'})N\). The two ordered sums are equal by symmetry of \(R\), so using the smaller source twice yields \(2h_{c'}N\) in place of \((h_c+h_{c'})N\). At heights \(3\) and \(1\) the two estimates are \(2N\) and \(4N\). The transfer-square calculation in Proposition 3 gives the two height bounds for the same interaction. In the coordinate proof, symmetry permits both orientations, and label inclusion picks the orientation used for the count. [Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437), [Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf).

If one height grows while the other stays fixed, the sum of the fixed-orientation bounds \((h_c+h_{c'})N\) increases for \(N>0\), stays zero for \(N=0\), and decreases for \(N<0\). Once the shorter height is fixed, the number of common labels is fixed as well, and orienting both sums from the shorter column gives \(2\min(h_c,h_{c'})N\) in total.

The label sets are terminal intervals, possibly empty, by upward closure and selection by whole columns. To see the orientation explicitly, first suppose every label in \(S_c\) has a match in \(S_{c'}\). For each \(p\in S_c\), there is then exactly one such match by label injectivity, so the row on the right sums to exactly \(N\), which bounds the row on the left. Equal label sets use this branch.

Otherwise take \(p_*\in S_c\) with label \(i_*=b(p_*)\) missing from \(S_{c'}\). A box \(q\in S_{c'}\) of label \(i_*\) contradicts the choice of \(i_*\). If \(b(q)<i_*\), upward closure from \(q\) supplies \(i_*\) in its column, and selection by whole columns puts that box in \(S_{c'}\), again a contradiction. Therefore \(b(q)>i_*\), and upward closure from \(p_*\) and whole-column selection give \(q\) a match in \(S_c\). Now interchange the sums and use \(R(p,q)=R(q,p)\) to apply the row bound to each \(q\in S_{c'}\), with its unique match giving exactly \(N\) on the right.

In either branch, the right side is \(\min(h_c,h_{c'})N\), because the contained label set has one match per box. This is an exact count, so the proof works for \(N=0\) and \(N<0\) as well. In particular, for \(N<0\) the orientation is justified by the matching identity, independently of which product of a height and \(N\) is numerically smaller.

**Remarks.** Write \(\ell_c,\ell_{c'}\) for the least selected label in each column, with value \(n\) for an empty column. In the missing-label branch any \(i_*\) with \(\ell_c\le i_*<\ell_{c'}\) works, since only its presence in \(S_c\) and its absence from \(S_{c'}\) are needed. The statement allows empty columns for convenience, while Proposition 8 uses only indices in \(C_S\). If either column is empty, both double sums vanish. If \(p\in S\) and some column \(c\ne\gamma(p)\) has \(S_c=\varnothing\), the row bound for \(p\) and \(c\) reads \(0\le N\).

## Proposition 8. Cross-column comparison by equal labels

\[
\begin{gathered}
\text{For every }n\in\mathbb Z_{\ge0},\ \text{finite set }Q,\ \text{set }C,\
\gamma:Q\to C,\ b:Q\to L_n,\ S\subseteq Q,\
R:Q\times Q\to\mathbb R,\ N\in\mathbb R,\\
\text{assume }\mathcal T(\gamma,b),\quad\mathcal U(\gamma,S),\quad
\forall p,q\in Q,\quad R(p,q)=R(q,p),\\
\forall p\in S,\ \forall c\in C\setminus\{\gamma(p)\},\qquad
\sum_{q\in S_c}R(p,q)\le N.
\\
\text{Then}\qquad
\sum_{p\in S}\ \sum_{\substack{q\in S\\\gamma(q)\ne\gamma(p)}} R(p,q)
\le
\sum_{p\in S}\ \sum_{\substack{q\in S\\\gamma(q)\ne\gamma(p),\ b(q)=b(p)}}N .
\end{gathered}
\]

**Proof.** Replacing each cross-column entry by its own equal-label charge would use the pointwise comparison \(R(p,q)\le N\mathbf 1_{b(p)=b(q)}\). Take \(n=2\), with slots \(p_1,p_2\) forming a column with labels \(0,1\), respectively, and a singleton \(p_3\) with label \(1\). In this slot order take \(f=(|010\rangle-|100\rangle)/\sqrt{2}\), which alternates in \(p_1,p_2\) and has squared norm \(1\). The swap of \(p_1,p_3\) fixes \(|010\rangle\) and sends \(|100\rangle\) to \(|001\rangle\), which is orthogonal to \(f\). Its expectation is \(1/2>0\) despite unequal tableau labels. The swap of \(p_2,p_3\) fixes \(|100\rangle\) and sends \(|010\rangle\) to \(|001\rangle\), giving the other expectation \(1/2\). The column total \(1/2+1/2=1\) is exactly the single equal-label charge. The label \(b\) stays fixed in the count while the coordinate assignment \(x\) varies in the inner product. The transfer-square calculation in Proposition 3 bounds the full sum \(X_{cc'}\). Its coefficient \(\min(h_c,h_{c'})\) counts common labels for terminal intervals without an entrywise comparison. [Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437), [Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf).

Use Proposition 6 on both sides, with \(R\) on the left and \(N\mathbf 1_{b(p)=b(q)}\) on the right. Each side then ranges over the same ordered pairs of distinct active columns. Proposition 7 gives the inequality for every such pair, and addition proves the result.

The same bound can be counted by label using whole rows. Orient each unordered pair of active columns from the shorter column, with one choice of orientation in a tie. Each source label \(i\) occurs once there and also occurs in the target column. Its row contributes at most \(N\), and symmetry lets that row bound account for both orders. Exactly \(\binom{m_i}{2}\) unordered column pairs contain \(i\) in both columns, so the total upper bound from rows charged to label \(i\) is \(2\binom{m_i}{2}N\).

**Remarks.** With at most one active column the cross-column domain is empty, so both sides vanish for every real \(N\).

## Proposition 9. The tableau count for a symmetric kernel

\[
\begin{gathered}
\text{For every }n\in\mathbb Z_{\ge0},\ \text{finite set }Q,\ \text{set }C,\
\gamma:Q\to C,\ b:Q\to L_n,\ S\subseteq Q,\
R:Q\times Q\to\mathbb R,\ N\in\mathbb R,\\
\text{assume }\mathcal T(\gamma,b),\quad\mathcal U(\gamma,S),\quad
\forall p,q\in Q,\quad R(p,q)=R(q,p),\\
\forall p,q\in Q,\quad
\gamma(p)=\gamma(q)\ \land\ p\ne q\ \Longrightarrow\ R(p,q)=-N,\\
\forall p\in S,\ \forall c\in C\setminus\{\gamma(p)\},\qquad
\sum_{q\in S_c}R(p,q)\le N.
\\
\text{Then}\qquad
ndN+\sum_{p\in S}\sum_{\substack{q\in S\\q\ne p}}R(p,q)
\le \left(\sum_{i\in L_n}m_i(m_i+2i+1-n)\right)N.
\end{gathered}
\]

**Proof.** The formulation for an arbitrary symmetric real kernel and a real scale of either sign is a convenience. The application uses \(R(p,q)=\operatorname{Re}\langle f,P_{pq}f\rangle\) and \(N=\|f\|^2\ge0\). Here the within-column contribution is an exact identity multiplied by \(N\), and the cross-column bound already holds in its signed form.

The signed internal contribution from a column of height \(h_c\) is \(-h_c(h_c-1)N\), of magnitude \(h_c(h_c-1)|N|\). In the tensor application \(N=\|f\|^2\ge0\), so for a tall column the internal debit has leading magnitude \(h_c^2N\), compared with a diagonal charge \(nh_cN\). Across two equally tall columns the separate estimates grow as \(2h_c^2N\), while the whole-column estimate grows as \(2h_cN\). The latter counts only common labels. These are scales for the terms separately. When \(h_c=n\) the quadratic part of the diagonal and internal contributions cancels and their combined charge is only \(nN\).

Split the distinct ordered pairs into same-column and cross-column pairs. The case \(q=p\) has no term in this sum. Within a column the hypothesis supplies \(-N\) for distinct pairs only, and across columns the terms retain the kernel \(R(p,q)\). Assigning \(-N\) to the diagonal as well would add an erroneous debit of \(dN\), already changing the answer for a singleton when \(N>0\).

Each unordered pair of distinct boxes in a column has exactly one increasing-label ordering, by label injectivity. Charge both orders to its lower label. Proposition 4 counts \(n-1-b(p)\) such partners for \(p\), giving the exact signed contribution
\[
-2N\sum_{p\in S}(n-1-b(p)).
\]
For \(N\ge0\), dropping the nonpositive terms loses \(2N\sum_{p\in S}(n-1-b(p))\). A single active column of height \(h_c\) has no cross-column contribution and gives exactly \(nh_c-h_c(h_c-1)\) as the coefficient of \(N\). Dropping the signs gives the coefficient \(nh_c\).

For the remaining ordered pairs, Proposition 8 bounds the sum by one \(N\) for each equal-label match across columns. Proposition 5 gives \(m_{b(p)}-1\) such matches from \(p\). Adding the diagonal \(n\), the internal debit \(-2(n-1-b(p))\), and the cross-column charge \(m_{b(p)}-1\) yields \(m_{b(p)}+2b(p)+1-n\) per box. Summing by label puts \(m_i\) identical terms together and gives the right side of the proposition.

**Remarks.** With \(S=\varnothing\) both sides vanish. With \(N=0\) the within-column and diagonal parts vanish and the cross-column part is nonpositive. The latter part can be strictly negative for an abstract kernel even at \(N=0\).

## Theorem 10. Application to the slot Casimir

**Proof.** Evaluating \(K\) on the tensor of highest wedges identifies a distinguished eigenvalue. That direct test alone gives no bound on every alternating tensor. At \(n=2\) with two singleton columns, Proposition 2 gives \(K=4\,\mathrm{Id}+2P_{p_1p_2}\), where \(p_1,p_2\) are the two slots. Both the symmetric and alternating tensors are admissible, with eigenvalues \(6\) and \(2\), respectively.

**Highest-weight proof (not in the Lean; checked by hand).** For any constituent highest weight \(\mu\), a basis wedge in column \(c\) uses distinct indices, so at most \(\min(k,h_c)\) of its indices can lie among the first \(k\) basis vectors in reversed order. Thus the first \(k\) coordinates of \(\mu\) sum to at most \(\sum_{c\in C_S}\min(k,h_c)=\sum_{j=1}^k\lambda_j\), with equality at \(k=n\) because the degrees agree. Put \(D_k=\sum_{j=1}^k(\lambda_j-\mu_j)\) and \(v_j=\lambda_j+\mu_j+n+1-2j\). The difference of the trace-form eigenvalues is the sum of \((\lambda_j-\mu_j)v_j\), which telescopes to \(\sum_{k=1}^{n-1}D_k(v_k-v_{k+1})\). Each \(D_k\) is nonnegative and \(v_k-v_{k+1}\ge2\) since both weights are dominant. Orthogonal decomposition now bounds the quadratic form on arbitrary sums of constituents, with the factors outside \(S\) acting as spectators. This comparison needs no constituent multiplicities from exterior Pieri. Alpöge’s coordinate proof follows. [Exterior Pieri, Proposition 2.1](https://math.mit.edu/~apost/papers/LR.pdf), [Orthogonal complete reducibility and highest weights, lectures 18 and 25–26](https://ocw.mit.edu/courses/18-745-lie-groups-and-lie-algebras-i-fall-2020/mit18_745_f20_lec_full.pdf), [Trace-form eigenvalues, Example 5.4](https://arxiv.org/pdf/2202.12225), [Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf), [Cartan component, Baur’s thesis, Proposition 3.2](https://edoc.unibas.ch/entities/publication/1af5150b-0f45-4b80-b0b4-843a4b08af55/full).

Set \(N=\|f\|^2\) and \(R(p,q)=\operatorname{Re}\langle f,P_{pq}f\rangle\). By Proposition 2 and linearity of the real part of the inner product in its second argument over the reals,
\[
\operatorname{Re}\langle f,Kf\rangle
=ndN+\sum_{p\in S}\sum_{\substack{q\in S\\q\ne p}}R(p,q).
\]
Keeping exact within-column terms but bounding cross-column swaps individually would cost \(h_ch_{c'}N\) for the ordered pair of columns \(c,c'\). For two full columns at \(n=2\), the diagonal gives \(8N\) and the internal terms give \(-4N\). The individual estimates add \(8N\) and give \(12N\), whereas the grouped bounds add \(4N\) and give \(8N\). The reduction from \(h_ch_{c'}\) charges to \(\min(h_c,h_{c'})\) comes from Propositions 3 and 7.

The kernel is symmetric because \(P_{pq}=P_{qp}\). The global alternation hypothesis first gives the exact value \(R(p,q)=-N\) for distinct same-column boxes. It is used a second time with only the alternation within a target column \(S_c\). For \(p\in S\) and \(c\ne\gamma(p)\), that column lies entirely away from \(p\), so Proposition 3 bounds \(\sum_{q\in S_c}R(p,q)\) by \(N\). Empty target columns also satisfy the bound, which then reads \(0\le N\). These are exactly the hypotheses of Proposition 9. Its conclusion is the asserted inequality.

**Remarks.** The coefficient can also be written by heights as \(\sum_{c\in C_S} h_c(n+1-h_c)+2\sum_{\{c,c'\}\subseteq C_S}\min(h_c,h_{c'})\), where the second sum is over two-element subsets. The first sum is the diagonal plus the exact internal contribution. The second counts each cross-column interaction twice. Sharpness (not in the Lean; checked by hand). For \(n>0\), the tensor of nested highest wedges attains this coefficient by the trace-form eigenvalue formula. If \(S=\varnothing\) or \(f=0\), both sides are zero, and \(n=0\) forces \(Q=S=\varnothing\). [Trace-form eigenvalues, Example 5.4](https://arxiv.org/pdf/2202.12225), [Exterior Pieri, Proposition 2.1](https://math.mit.edu/~apost/papers/LR.pdf), [Gross, Appendix A.1](https://arxiv.org/pdf/hep-th/9212149), [Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf), [Cartan component, Baur’s thesis, Proposition 3.2](https://edoc.unibas.ch/entities/publication/1af5150b-0f45-4b80-b0b4-843a4b08af55/full).

## Routine and classical facts

- Finite sums can be reordered, expanded by distributivity, or collected according to the values of a map on their index set.
- In the matrix-unit action, \(E^{(p)}_{ii'}f\) at \(x\) is \(f(x[p\leftarrow i'])\) when \(x(p)=i\), and is zero otherwise. A zero scalar background gives only the sum of the slot matrix units.
- A slot permutation acts by permuting the coordinate basis and products of the operators follow composition of the permutations. A transposition is a unitary involution, hence self-adjoint.
- The Hermitian norm is nonnegative, and the real part of a Hermitian matrix element is bounded above by the product of the two norms by Cauchy–Schwarz.
- The interval of labels strictly above \(i\in L_n\) has \(n-1-i\) elements. In a column with distinct labels, a prescribed label contributes exactly once when present and zero times when absent.
- Within one column, each unordered pair of distinct boxes corresponds to two ordered pairs and to exactly one pair in increasing label order.
- For any real-valued function of the tableau label, the sum of its values over selected boxes uses the value at label \(i\) exactly \(m_i\) times.
- The signed average over a finite unitary permutation group is the orthogonal projector onto its sign subspace.
- Normalized alternation identifies \(\bigwedge^{h_c}\mathbb C^n\) isometrically with the alternating tensors of degree \(h_c\). Each unit basis wedge maps to the signed sum of its \(h_c!\) tensor orderings divided by \(\sqrt{h_c!}\). [Exterior powers as fundamental representations, §2](https://math.mit.edu/~apost/papers/LR.pdf).
- Taking invariant orthogonal complements gives an orthogonal decomposition of a finite-dimensional unitary representation into irreducibles. The trace-form quadratic Casimir acts on the highest-weight constituent of weight \(\mu\) by \(\Gamma_n(\mu)\). [Etingof, semisimple complete reducibility and highest-weight theory, lectures 18 and 25–26](https://ocw.mit.edu/courses/18-745-lie-groups-and-lie-algebras-i-fall-2020/mit18_745_f20_lec_full.pdf), [Trace-form eigenvalues, Example 5.4](https://arxiv.org/pdf/2202.12225), [Perelomov and Popov, §2](https://www.mathnet.ru/links/31651a58ff26049b02381fcda398189c/im2520_eng.pdf).
- Schur–Weyl duality identifies the tensor-power constituents indexed by partitions. On the symmetric-group constituent the sum of all transpositions has scalar equal to the sum of the contents of its boxes. [Schur–Weyl duality, Theorem 27.3](https://ocw.mit.edu/courses/18-755-lie-groups-and-lie-algebras-ii-spring-2024/mit18_755_s24_lec01.pdf), [Transposition contents, Okounkov–Vershik, (2.1) and Proposition 6.2](https://www.esi.ac.at/preprints/esi333.pdf), [Frobenius’s character formula, §2](https://faculty.fordham.edu/dswinarski/snchar/Frobenius1900.pdf), [Cesi, transposition class-sum scalar, (4.1) and Proposition 4.1](https://arxiv.org/pdf/0902.0727).
- Occurrence in a Young permutation module forces dominance of its indexing partition by the constituent's partition. Tensoring with sign conjugates the partition, reversing dominance. [Young permutation modules and dominance, Theorem 6.5 and §6.9](https://ir.cwi.nl/pub/10125/10125D.pdf), [Macdonald, dominance reversal in I.1, (1.11), and sign twist in I.7, Example 2](https://math.berkeley.edu/~corteel/MATH249/macdonald.pdf).
- On a tensor product of exterior powers the exterior transfer moves a basis vector from one factor into the other by contraction and wedge multiplication. The calculation in Proposition 3 identifies the squared norm form in each direction with the corresponding height times the identity minus the interaction. [Transfer actions, Cautis–Kamnitzer–Morrison, §4.2, Lemma 4.2.3 at \(q=1\)](https://arxiv.org/pdf/1210.6437), [Exterior-algebra framework, Howe, Theorem 8 and example (d)](https://www.math.utah.edu/~ptrapa/math-library/howe/howe-remarks-invariant-theory-TAMS-1989.pdf).

## Concordance

Module-local declarations are listed by their source name within the indicated module.

| Displayed result | Declaration | Source |
| --- | --- | --- |
| Theorem 10. Tableau Casimir bound | `PositivityTheory.Rg.Cz.casBound_holds` | CasBoundHolds.lean:9–32. Statement in StepFormula.lean:88–94. |
| Proposition 1. Contraction of two slot matrix units | `PositivityTheory.Rg.Cz.pair_apply` | Expand.lean:32–55 |
| Proposition 2. Slot expansion | `PositivityTheory.Rg.Cz.cas_expand'` | Expand.lean:66–92 |
| Proposition 3. One outside box | `PositivityTheory.Rg.Cz.re_swapSum_le'` | ReSwapSumLe.lean:29–83 |
| Proposition 4. Higher labels | `PositivityTheory.Rg.Cz.count_up` | CountSame.lean:22–44 |
| Proposition 5. Equal labels | `PositivityTheory.Rg.Cz.count_eqb` | CountSame.lean:46–69 |
| Proposition 6. Partition of cross-column pairs | `sum_sum_ite_col_ne_eq_sum_by_col` (private) | CountCross.lean:59–83 |
| Proposition 7. Comparison for two distinct columns | `sum_filter_col_le_sum_ite_of_bound` (private) | CountCross.lean:28–57 |
| Proposition 8. Cross-column comparison | `PositivityTheory.Rg.Cz.count_cross` | CountCross.lean:85–102. Uses the lemmas for Propositions 6 and 7. |
| Proposition 9. Tableau count | `PositivityTheory.Rg.Cz.cas_count` | CountCross.lean:104–153 |
