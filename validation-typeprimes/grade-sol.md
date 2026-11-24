## 1. Exposition

I count an insight as captured when the exposition explicitly gives its central mathematical point. I flag missing parts of that insight separately. Line references are to [assembled-v10.md](assembled-v10.md).

| Key insight | Grade | Evidence |
|---|---|---|
| 1. The generator is congruent to one | **Captured** | L21 gives the two divisibilities. L410 says “The identity ray class encodes this generator congruence.” L402–406 derive the rational congruence and give a counterexample to its converse. L11 connects the two certificates to the host and splitting. |
| 2. The analytic input supplies a uniform dyadic pool | **Captured** | L418 says “The proof uses the assumed estimate at \(h=1\).” L420 says “The threshold is independent of \(d,N,Y\).” L424 checks the conductor and absorbs the denominator to get \(Y^{9/10}\). |
| 3. Each prime has at most \(3r+1\) labels | **Captured** | L161 says “four of them would have product greater than \(m>n\).” L178–182 apply this to \(g^j-1\), sum the layers, and include the singleton. |
| 4. The minimum valuation gives a large common modulus | **Captured** | L267 says “Taking the minimum gives the largest common modulus” and uses the minimizing base to prove its size. L269 counts “at most \(2j\) root classes” and applies spacing. L205–226 explain the factor of two and the odd-prime case. |
| 5. Two unions bound the overlap at one anchor | **Captured** | L293 says “The base \(g=\ell\) can carry the label without any exceptional witness and costs at most one,” then sums over exponents. L315–319 sum over the anchor’s labels. L338 makes explicit that the bound applies to “arbitrary integer bases.” |
| 6. The gap between the counts leaves a distinct second prime | **Captured** | L354 gives the “factor \(Y^{3/20}\) beyond the spacing scale.” L356 makes the strict count comparison. L358 says “The anchor belongs to that subset, so the selected candidate is distinct.” |
| 7. The prescribed scale absorbs polynomial losses and gives comparable primes | **Captured** | L443–446 give the Taylor-term proof. L481 says “all larger \(k\) help both comparisons,” and L483–487 check both inequalities. Comparability follows immediately from the displayed dyadic interval. The downstream rank inequality \(g_0-2>2fk\) is absent. |
| 8. Two primes give a local test in every residue characteristic | **Captured, with a gap in the explanation** | L13 says “The choice can depend on \(\ell\)” and “this also gives \(\ell\ne g_i\).” It identifies root separation and residual irreducibility. It leaves out how the fourth-root cutoff limits collisions when constructing good types, and how the test feeds the comparison behind the prime-sum bound. |

**Counts:** 8 captured, 0 buried, 0 missed, 0 wrong at the level of the central insights.

The strongest extra insight is that the prescribed norm condition forces both exponent-one factors to be divisible by \(N\), so demanding coprime products of shifted powers is impossible (L471). The exposition also gives a valid alternative to choosing a minimizer: take the first power of \(\ell\) above \(Y^{j/4}\). Keeping the full \(j\)-dependent spacing then improves the overlap bound to \(O(rY^{3/4}+r^3)\) (L271, L295). A separate downstream insight is that the pair’s logarithmic size bounds let the cyclic construction apply `ShortNorm` again, at a different window, to find \(T\) at modulus \(N(g_0g_1)^2\) (L11, `scope.json`).

## 2. Digest

Line references are to [digest-v7.md](digest-v7.md). I grade each item’s central claim.

| Item | Class | Stands alone? |
|---|---|---|
| 1. Delete collisions at the original modulus (L3–15) | **a.** Key 6, the outer union of key 5, and the polynomial-loss part of key 7. | Yes, as a selection argument given the stated pool and incidence bounds. |
| 2. Minimum valuation (L17–29) | **a.** Key 4. | Yes. It gives the common divisibility, modulus size, and spacing count. |
| 3. Uniform dyadic count (L31–43) | **a.** The conductor and uniformity part of key 2. | Yes, as a conditional raw count. |
| 4. Three labels per exponent (L45–57) | **a.** Key 3. | Yes. The factorization argument is self-contained. |
| 5. Sum over the partner’s exponent (L59–71) | **a.** The inner union of key 5. | The bound is recoverable from the item, but “anchor” is undeclared and the fixed-label role is clearer after item 1. |
| 6. Budget one tenth (L73–85) | **a.** The loss calculation in key 2. | Partly. The calculation works on its own given the raw bound, but “in the conductor range” relies on item 3 to specify and verify that range. |
| 7. Prescribed generator (L87–99) | **a.** Key 1’s arithmetic content. | Yes. It omits the host-splitting application. |
| 8. Two cyclic cosets at 2 (L101–113) | **c.** Correct supporting detail of key 4, already used in item 2. | Yes. |

**Precision:** \(7/8=87.5\%\), counting the separate item on powers of two as supporting detail. **Recall:** \(7/8=87.5\%\), crediting key 7 across items 1 and 3. The digest omits key 8 altogether. **The ranking is design-first.** It opens with the arbitrary-anchor deletion argument and follows with the minimum-valuation move that makes deletion affordable.

## 3. Reasons, literature, and provenance

- **The digest overstates what the gcd comparison requires.** L63 says the exponential upper bound “would need” \(\delta\le\log Y/(4r)\) for \(i=1,j=r\). This is sufficient. Since the gcd is integral, an upper bound strictly below \(\lfloor Y^{1/4}\rfloor+1\) also suffices. Exposition L287 makes this correction. The real obstacles are the moving bases and potentially small exponents.
- **“The dyadic norm count is assumed in Lean” is imprecise** (digest L9). Lean assumes the raw `ShortNorm` estimate over its full interval range. It derives the \(Y^{9/10}\) dyadic pool. The product-modulus objection in digest L7 and exposition L475 is valid for a modulus containing the anchor at the same window. Its scope is that specific construction.
- **The literature record supports precedents for components.** The hypergraph citation explains the selection rule, and the Poonen, Hooley, and primary-component references are analogies at the stated level. They supply no evidence of priority for the exact arithmetic pair. The \(A=3\) estimate is a specialization argued in `lit.md` L284–290. It should be credited as a derivation from the 2019 cumulative estimate. The 2017 result listed in `sources.md` is a separate antecedent. The search’s claim that the exact pair did not appear *in the sources reviewed* is appropriately limited.
- **I found no positive evidence of use of the excluded Rodgers write-up.** The shared formulas and proof moves follow from the Lean. Exposition L13 does go beyond the recorded trace, which stops at the local-type constructor and flags irreducibility links as unopened (`scope-levels.json` L307–341). Its mathematical point agrees with the key and it cites Lean locations, so the paragraph is a provenance gap in the package. The local materials do not establish which route supplied it. The analytic narrative at L17 likewise goes beyond the proof excerpts available here.

## 4. Faithfulness to Lean

Theorem 15 faithfully renders `typePrimesN`, including the quantifier order, all of `ModAt`, natural-valued \(N,d,k,r\), the closed output interval, both norm certificates, distinctness, and disjointness. Replacing `Fin 2 → ℕ` with two primes is equivalent. The candidate pool really has a strict lower endpoint by the floor convention at these positive endpoints. **The root’s explicit analytic premise is `ShortNorm`.** It has no separate RH, GRH, or `SmallOne` hypothesis. The empty top-level `premises` array in `units4.json` does not erase the implication in the signature. The archive supplies `ShortNorm` downstream through the analytic theorem, as recorded in `scope.json` L180–203.

Propositions 1–14 preserve the central hypotheses and bounds. In particular, 7–9 retain the abstract root-count and label-count premises where Lean uses them, 10 discharges them, 11 preserves the strict exclusion threshold, and 12–14 preserve the conductor, count, and exponential estimates. Proposition 5 correctly distinguishes the weaker odd-prime bound in the Lean statement from the stronger cyclic bound proved on the way. The additional sharpenings are valid mathematical remarks beyond those statements.

## 5. Verdict

An expert could reconstruct why the selection proof works from the exposition and could recover its arithmetic design from the digest alone. The digest explains how to find the pair, but gives no reason the larger argument wants two primes with disjoint exceptional sets. The single highest-value change is to add the downstream mechanism to the digest immediately after the selection argument: for each residue characteristic, disjointness supplies a usable prime different from that characteristic, and the fourth-root cutoff controls collisions among the prime-to-characteristic parts of the local roots used in the irreducibility test.
