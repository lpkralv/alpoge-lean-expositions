I found four local overstatements in [assembled-v11.md](assembled-v11.md). The proof of `PositivityTheory.Rg.Cz.casBound_holds` goes through.

1. **Line 63 — Quantifiers.** “the maximum on the entire tensor power includes directions excluded by alternation”  
   Take \(n=2\) and let \(S=Q\) consist of two singleton columns, both labeled \(1\). The alternation condition in `CasBound` is vacuous, so every direction in the tensor power is admissible, including the entire maximum eigenspace. The stated exclusion occurs when an active column has at least two slots. **Severity — local: the proof still goes through.**

2. **Line 280 — Signs.** “If one height grows and the other stays fixed, the sum of the fixed-orientation bounds grows linearly with the taller column, whereas the number of common labels stays at most the fixed height.”  
   The sum of the bounds is \((h_c+h_{c'})N\). It increases for \(N>0\), stays constant for \(N=0\), and decreases for \(N<0\). Negative \(N\) is possible under `sum_filter_col_le_sum_ite_of_bound`. Take exactly two active columns of heights \(h\) and \(1\), with terminal labels, \(N=-1\), and every cross-column entry equal to \(-1\). The row sums are \(-1\) and \(-h\), so the hypotheses hold and the fixed-orientation bound is \(-(h+1)\). **Severity — local: the proof still goes through.**

3. **Line 309 — Necessity.** “For decision 6, a direct count by tableau label would require the pointwise comparison \(R(p,q)\le N\mathbf 1_{b(p)=b(q)}\) at cross-column pairs.”  
   The pointwise comparison would suffice. A label-indexed count can instead orient each unordered pair of active columns from the shorter column, breaking ties consistently, and charge each source row to its source label. For label \(i\), a row is charged exactly once for each unordered pair of columns containing \(i\). The shorter column’s labels are contained in the taller column’s labels. Bounding each row by \(N\) and using symmetry for the two orders gives \(2\binom{m_i}{2}N\) for label \(i\), without a pointwise comparison. **Severity — local: the proof still goes through.**

4. **Line 337 — Signs.** “In a tall column the internal debit has leading magnitude \(h_c^2N\), compared with a diagonal charge \(nh_cN\).”  
   For the signed scale in `cas_count`, the internal contribution is \(-h_c(h_c-1)N\) and its magnitude is \(h_c(h_c-1)|N|\). For example, use one column of height \(h_c=n\), set \(N=-1\), and set \(R(p,q)=1\) for distinct slots. The cross-column hypothesis is vacuous and the internal contribution is positive. The quoted magnitude applies in the tensor application, where \(N=\|f\|^2\ge0\). **Severity — local: the proof still goes through.**

| Claim kind | Checked | Correct |
|---|---:|---:|
| Quantifiers | 156 | 155 |
| Necessity and sufficiency | 58 | 57 |
| Signs and vanishing | 116 | 114 |

I counted repeated assertions where they appear and assigned overlapping claims to their primary category. The counts include the local deductions in the automorphic discussion. Archive-specific assertions in lines 9 and 15 whose declarations are outside `units4.json` are excluded from the counts.
