# Cold read of the tableau Casimir bound

I read the PDF before consulting the TeX for wording. Line numbers count all lines in the layout-preserving PDF text extraction, starting with the running header.

## Where I lost the thread

- **p. 2, l. 14–25.** I could follow the instruction to sum the swaps into one column. I lost the reason for squaring $f-Yf$ and for dividing by $k+1$. The formula arrives before I know what it measures. The paragraph also introduces the highest-weight proof just as I am trying to identify the argument the paper will teach.
- **p. 2, l. 36 to p. 3, l. 51.** I stopped trying to follow the application at “coefficient gluing” and skipped to the theorem. I still needed the slot action and the normalization of $K$. The twist, $J$, and the Kuga argument arrive before I can see what the untwisted estimate contributes.
- **p. 8, l. 42–55.** I read the exterior-transfer calculation as the start of the proof of Proposition 3. It proves a bound for a pair of wedges. The proposition asks for a bound from a single box into an alternating target set, and its calculation starts at l. 56.
- **p. 10, l. 35 to p. 11, l. 24.** The abstract kernel and the discussion of negative $N$ made me lose sight of the tensor argument. The missing-label witness proves that the two label sets are nested. Drawing the two terminal intervals would make the choice of orientation immediate.

## Terms and steps that need an earlier explanation

- “Terminal intervals” and the “within-column debit” occur on p. 2, l. 16–17. The former means each selected column contains one box at every label from its lowest label to $n-1$. The latter comes from the $-1$ action of each internal swap. The swap action and the Casimir with “zero background” (p. 2, l. 30) first get formulas on p. 4, l. 3–8. State there that the generators are sums of slot actions with no added scalar term.
- The pair-deficit display uses $h_c,S_c,X_{cc'},P_{pq}$ on p. 3, l. 14–24, ahead of the notation and swap definitions. The application also uses “embedding fiber” and “coefficient gluing” before giving enough local context. A fiber here simply selects all slots attached to one embedding, and $J$ puts the coefficient vector into the alternating tensor space.
- The key idea is announced on p. 2, l. 13–24. Its explanation is in the remark on p. 9, l. 28–31. Antisymmetrizing over the target column plus the outside box gives $(f-Yf)/(k+1)$ because the tensor already alternates on the target. This gives the reader a reason to form the defect and explains the divisor. The swap multiplication on p. 9, l. 10–24 gives the coordinate proof of the identity.
- I understood the purpose of the regrouping on p. 10, l. 27–32 only after the example on p. 11, l. 41–49. A swap between differently labeled boxes can have positive expectation. Equal labels count the allowances for an entire column pair. The paper distinguishes the fixed label $b$ from the varying coordinate $x$ in its notation, but the example is where I understood why that distinction matters.

## How I would explain the bound to a colleague in ten lines

1. Contract the matrix units. The Casimir becomes $n|S|I$ plus the sum of swaps over distinct ordered slot pairs in $S$.
2. Set $N=\|f\|^2$. Every swap within a column has expectation $-N$ by alternation.
3. For an outside box $p$ and an alternating target column $B$ of height $k$, put $Y=\sum_{q\in B}P_{pq}$.
4. In $Y^2f$, equal targets give $kf$. Different targets leave an internal swap acting on $f$ and give $-(k-1)Yf$, with $k-1$ terms per surviving swap.
5. Since $Y$ is self-adjoint, this gives $(k+1)(N-\operatorname{Re}\langle f,Yf\rangle)=\|f-Yf\|^2$. One source box therefore contributes at most $N$ to a target column.
6. Reversing the column order preserves the sum since $P_{pq}=P_{qp}$. Sum from the shorter column and double the bound to cover both orders.
7. Each selected column has a terminal interval of labels. The shorter interval is contained in the longer one, so each source box accounts for exactly one common label.
8. Label $i$ occurs in $m_i$ different columns and supplies $m_i(m_i-1)$ ordered cross-column allowances.
9. A box labeled $i$ has $n-1-i$ higher partners in its own column. Counting both orders gives its internal contribution $-2(n-1-i)N$.
10. Add $nN$ per box and collect the counts by label. The result is $\operatorname{Re}\langle f,Kf\rangle\le N\sum_i m_i(m_i+2i+1-n)$.

Yes, by the end I could explain the proof from the paper. I had to assemble the geometric reason for the square on p. 9, the meaning of the equal-label comparison on p. 11, and the coefficient by heights on p. 13, l. 48–54. I wanted one continuous argument showing where the height bound ends and where the tableau labels enter.

## Fixes ranked by how much they would help

1. Put the theorem and a short proof by heights before the application and literature survey. Start with $n|S|$, subtract $\sum_c h_c(h_c-1)$, and add $2\min(h_c,h_{c'})$ per unordered column pair. Then derive the $m_i$ formula. Keep the proposition-by-proposition derivation for readers following the Lean.
2. Open Proposition 3 with the enlarged-column antisymmetrizer and its $k+1$ signed coset terms. Follow it immediately with the three-slot product and the norm identity. Place the transfer calculation after the one-box proof and give the highest-weight argument its own heading.
3. Carry the existing $n=2$ example through the whole proof. Draw selected columns with labels $\{0,1\}$ and $\{1\}$, show the two expectations of $1/2$ in the row from the singleton, and finish with $6-2+2=6$ for the unit tensor. The same example gives $m_0=1$ and $m_1=2$.
4. Define slots, the fixed labels, the coordinate assignments, and $K$ at first use. Move the supplier trace and twist calculation after the proof. Introduce them there by stating that whole columns come from an embedding fiber and the multiplicities set the ceiling required by the application.
