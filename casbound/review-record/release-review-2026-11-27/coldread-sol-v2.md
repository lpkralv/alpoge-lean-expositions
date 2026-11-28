# Cold read of the v2 Casimir-bound exposition

Yes, I could explain the coordinate proof to a colleague after reading v2. Equation (2) on p. 2 gave me the strategy, and the projector on p. 7 explained why the estimate works. I could also explain why the caller needs the exact constant. The twist takes that constant to the caller’s ceiling, and any excess survives the shift. I used only the v2 manuscript. Line numbers below refer to its LaTeX source.

## Where I lost the thread

- **p. 2, ll. 117–122.** The first derivation sends me to two theorems I have yet to read and invokes the “tableau condition” before defining it. I could follow the height formula, but I had to wait until pp. 3–4 to see that the labels align columns at a common top label and make overlaps countable. The later distinction between a fixed label and a varying tensor coordinate helped.
- **p. 7, ll. 529–589.** I followed the projector argument. I paused at the Jucys–Murphy paragraph, where “seminormal,” “addable box” and “content” arrive without explanation. When Proposition 3 returned to $g=f-Yf$, it took a reread to see that the swap calculation verifies the same enlarged alternation. Its intermediate formula gives $P_{pq}g=-g$ for every $q\in B$ immediately.
- **pp. 9–10, ll. 730–783.** This is where I first lost the main proof. The introduction promises to sum from the shorter column. Proposition 7 introduces an indicator and a box with a missing label. Only the subsequent remark tells me that the case split finds the column whose label set is contained in the other. The equal-label pairs count how many times to apply the one-box bound. The running example on p. 10, ll. 823–832, shows why a swap between unequal labels can still contribute positively.
- **p. 11, ll. 878–894.** “Per box” momentarily made me read the displayed coefficient as a local bound for the swaps incident to that box. The remark corrects this. A single sum over labels would make it easier to see which step bounds the total and which steps just count pairs.
- **pp. 16–17, ll. 1294–1319 and 1344–1368.** I could follow $J$, the scalar shift and the ceiling $\kappa_\tau$. I lost the argument at “opposite trace scalars” and “Positivity then forces,” where I needed the signed Laplacian identity and the quadratic form that controls the differential. In §6.2 I followed the slot construction from $\nu_\tau$, then lost track of how the transferred quantum determinant and spherical descent yield the tensor. I could see how the signed column sum supplies signs, but I could not track nonvanishing through the contraction and the choice of summand.

The one-box identity is prominent in the abstract and introduction. Its explanation is the signed average on p. 7. The idea buried in the formal proof is why equal-label counting gives the *same* constant as choosing the shorter column. That connection is below Proposition 7 and split across the remarks after Propositions 7–9 and the proof of Theorem B.

## The proof I would give a colleague in ten lines

1. Write $N=\|f\|^2$, let $d$ be the number of selected boxes, and write $P_{pq}$ for a slot swap.
2. Expanding the Casimir in matrix units gives $n\,\mathrm{Id}$ for a repeated slot and $P_{pq}$ for distinct slots.
3. The diagonal gives $ndN$. A column of height $h$ gives $-h(h-1)N$ from its ordered internal swaps.
4. For a box $p$ outside an alternating column $B$ of size $s$, set $Y=\sum_{q\in B}P_{pq}$ and $g=f-Yf$.
5. Use $P_{pq}P_{pq'}=P_{pq'}P_{qq'}$ for distinct $q,q'\in B$ to get $P_{pq}g=-g$, hence $Yg=-sg$.
6. Self-adjointness gives $\|g\|^2=(s+1)\operatorname{Re}\langle f,g\rangle$, so the swaps from $p$ into $B$ contribute at most $N$.
7. Sum from the shorter column. Reversing the columns gives the same sum, so each unordered pair contributes at most $2\min(h,h')N$.
8. Add the three terms to get the height coefficient $\sum_c h_c(n+1-h_c)+2\sum_{\{c,c'\}}\min(h_c,h_{c'})$.
9. The labels in a column of height $h$ are $n-h,\ldots,n-1$, so every box in the shorter column has one match in the taller one. With $m_i$ boxes labeled $i$, there are $m_i(m_i-1)$ ordered matches at that label.
10. There are $n-1-i$ internal partners above a box labeled $i$. Count both orders there and add the diagonal and match counts to get the bound $\sum_i m_i[n-2(n-1-i)+(m_i-1)]N$ of Theorem A.

The paper gave me every ingredient for those ten lines. I had to assemble the three counts myself when moving between the height and label proofs. What I still could not explain was how the archive turns the twisted upper bound into a nonzero cohomology class.

## Fixes ranked by reader benefit

1. In the derivation on p. 2, explain that two columns have one common label per box in the shorter column. Use that fact to open §3.4. Mark a pair of unequal columns in Figure 1, draw one match per box in the shorter column, and label the two orientations. Before Proposition 9, give a three-row table of the diagonal, within-column and cross-column counts in height and label notation. Explain that Proposition 7’s cases recover the same comparison directly from Lean’s hypotheses.
2. Put the signed projector directly beside the swap proof and point out $P_{pq}g=-g$ in the intermediate line. Move the Jucys–Murphy paragraph to §5, where “content” can be defined as column index minus row index. Gloss “Cartan component” at its first use on p. 1 and point to the formula that fixes the normalization of $K$.
3. In §6.1, substitute $m_i=\nu_\tau(i)$ into the twisted coefficient in one display, then give the signed Kuga identity and identify the nonnegative form and the nonzero cochain to which it applies. In §6.2, state what each named operation supplies before introducing its formula, especially where nonvanishing is used.
4. Add a strict case to the running example. At $n=3$ with the same heights $2,1$, take a normalized fully alternating tensor on the three slots. Then $Yf=-2f$, the one-box deficit is $3$, and the Casimir expectation is $3$ against the ceiling $9$. The current $n=2$ example forces the enlarged alternating space to vanish, so every admissible tensor for that diagram attains the bound.
