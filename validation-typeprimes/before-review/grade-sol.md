## 1. Exposition

**7 captured, 0 buried, 1 missed, 0 wrong.** The line numbers below refer to the exposition. [assembled-v9.md](<local>/assembled-v9.md)

| Key insight | Assessment and evidence |
|---|---|
| 1. Generator congruent to one | **Captured.** Lines 400–408 derive the rational congruence, give a counterexample to its converse, and identify the integral generator as “congruent to 1 modulo \(N\mathcal O_K\).” Line 11 connects the generator and rational congruence to the host and splitting. |
| 2. Uniform dyadic pool | **Captured.** Lines 416–422 say the proof “uses the assumed estimate at \(h=1\)” and “the threshold is independent of \(d,N,Y\).” Line 422 checks \(\log D\le10t^2\), \(\log Y\ge8t^5\), and the lower bound of \(Y^{9/10}\). |
| 3. At most \(3r+1\) labels | **Captured.** Line 159 explains that “four of them would have product greater than \(m>n\).” Lines 172 and 176–180 apply this to \(g^j-1\), accumulate the exponent layers, and include the singleton. |
| 4. Minimum valuation gives a large common modulus | **Captured.** Line 265 says “Taking the minimum gives the largest common modulus.” Line 267 gives “at most \(2j\) root classes” with at most \(Y^{3/4}+1\) points each. Lines 203–224 account for the odd-prime bound and the factor of two at \(2\). |
| 5. Two unions bound overlap | **Captured.** Line 291 says “The base \(g=\ell\) … costs at most one” and sums over the partner’s possible witnesses. Lines 313–317 then cover the colliding integers by the sets for the anchor’s at most \(3r+1\) labels and give the exact product bound. |
| 6. The surplus leaves a distinct partner | **Captured.** Line 354 gives “\(Q\le20r^3Y^{3/4}<Y^{9/10}\le |G|\).” Line 356 explains that the anchor is among the deletions, so the survivor is distinct. |
| 7. Prescribed scale absorbs losses and gives comparable primes | **Captured.** Lines 441–445 give the single Taylor term and the \(21x^{15}\) bound. Line 479 explains that “all larger \(k\) help both comparisons,” and lines 481–483 show both inequalities. Factor-two comparability follows immediately from the stated window. The downstream rank inequality is absent. |
| 8. A usable local test in every residue characteristic | **Missed.** Line 11 says the archive “carries it into the field host’s arithmetic conditions and the cyclic host’s local-type data.” This records the handoff. The key’s mechanism is missing: for each \(\ell\), choose an index with \(\ell\notin BB(r,g_i)\). The singleton ensures \(\ell\ne g_i\), and the valuation cutoff controls collisions of prime-to-\(\ell\) parts in the local type used for residual irreducibility. The supplied trace stops before that use. [scope-levels.json](<local>/scope-levels.json:307) |

Two useful additions go beyond the key. Full coprimality of the shifted-power products is impossible because the generator condition forces \(N\mid g_i-1\) for both primes (line 469). That explains why the proof tests the *size* of the primary component. Also, retaining the exponent-dependent spacing improves the integer collision bound to \(O(rY^{3/4}+r^3)\) (lines 269 and 293). The same spacing argument can use the first power of \(\ell\) above \(Y^{j/4}\) as its common modulus.

## 2. Digest

I count a distinct proof idea from the key as **(a)** and a separately ranked technical subcase of an already captured idea as **(c)**. [digest-v7.md](<local>/digest-v7.md)

| Item | Classification | Stands alone? |
|---|---|---|
| 1. Delete collisions at the original modulus, 3–15 | **(a)** Keys 5–7. It defines the labels, gives the deletion bound, and explains survival and distinctness. | **Yes**, as a selection argument conditional on the stated pool size. |
| 2. Use the minimum valuation, 17–29 | **(a)** Key 4. It gives both common divisibility and the spacing saving. | **Yes.** |
| 3. Count eligible primes uniformly, 31–43 | **(a)** The uniform analytic input and conductor check in key 2. | **Yes** for the raw lower bound. Item 6 converts it to the pool size. |
| 4. Three labels per exponent, 45–57 | **(a)** Key 3. The forced-gcd comparison is a useful addition. | **Yes.** The factorization link at line 51 points to an absent earlier draft, but the argument is in the item. |
| 5. Sum over the partner’s witness, 59–71 | **(a)** The inner union of key 5. Item 1 supplies the outer union. | **Partly.** It invokes the fixed-exponent estimate without explaining how to obtain its common modulus, and refers to an anchor without introducing it. |
| 6. Budget one tenth of the exponent, 73–85 | **(a)** The denominator absorption in key 2. | **Yes** as a calculation from the stated raw bound. The conductor test is supplied in item 3. |
| 7. Prescribe the generator residue class, 87–99 | **(a)** Key 1’s generator condition and the failure of the rational-congruence converse. | **Yes** for candidate eligibility. The downstream splitting payoff is absent. |
| 8. Two cyclic cosets at \(2\), 101–113 | **(c)** A correct technical subcase of key 4, already covered by item 2. | **Yes.** |

**Precision \(7/8=87.5\%\). Recall \(7/8=87.5\%\)** at the level of the eight mechanisms, counting key 7’s scale argument even though its downstream payoff is absent. If an explicitly keyed subcase earns **(a)** as its own item, precision is **\(8/8\)** with the same recall. The ranking is design-first. Item 1 gives the global move, and item 2 gives the arithmetic move that makes deletion cheap. The last slot goes to a technical subcase while the reason for wanting disjointness is missing.

## 3. Reasons, literature, and provenance

- **One overstated reason.** Exposition line 285 and digest line 63 say the gcd comparison *needs* the stated upper bound on \(\delta\). The condition suffices when using the displayed coarse lower bound on the shared prime power. A stronger lower bound could allow larger \(\delta\). The actual objection stands: the cited fixed-base, large-exponent result gives no uniform control for these moving bases and potentially tiny exponents. The original-modulus objection is also sound for the specific proposal to put **every** label into the modulus, since that includes the anchor itself.
- **The analytic precedent is a derivation.** Exposition lines 51 and 414 and digest line 43 compress the passage from cumulative Thorner–Zaman to an interval lower bound with \(A=3\). The supplied literature notes give the needed relative-error and exceptional-zero calculations, including how the endpoint errors fit below the interval main term. The grader’s sources identify the 2017 paper as Jaswal’s antecedent and the archive and Rodgers as sources for the actual short-interval input. The 2019 route is a separate specialization. The Perron and contour account at exposition line 15 is more detailed than the supplied Lean package and trace can verify. [lit.md](<local>/lit.md:284) · [sources.md](<local>/sources.md:17)
- **The literature labels mostly describe analogies.** Hooley, Poonen, and Xie support component comparisons. They do not establish priority or precedent for this particular pair-selection argument. The bounded-neighborhood and prime-power root comparisons are direct. I found no explicit novelty claim. The search record’s statement that the exact assertion did not appear in the reviewed sources is limited to that screened search.
- **No distinctive evidence of borrowing.** The shared inequalities, minimum-valuation choice, and anchor step are all visible in the Lean package. I found no distinctive Rodgers wording or fact uniquely attributable to his write-up in either output. The more detailed upstream account at exposition line 15 has uncertain provenance within the supplied files.

## 4. Faithfulness to Lean

**The main statement is faithful.** Theorem 15 expands `ModAt`, `NormOne`, `BB`, and `ShortNorm` correctly. Its logical form is `ShortNorm → …`, even though the package’s `premises` metadata is empty. `ShortNorm` has one positive triple \(A,c,c'\) uniform in \(d,M,X,h\) over the stated conductor and interval ranges. The root uses only \(h=1\), gives a threshold uniform in \(N,d,k,r\) for fixed \(\varepsilon\) and the chosen constants, and has no separate RH, GRH, or `SmallOne` premise. The archive supplies `ShortNorm` upstream. Replacing the indexed `Fin 2` pair with \(a,b\) is equivalent, and the exposition correctly distinguishes the pool’s open left endpoint from the conclusion’s closed endpoint. [units4.json](<local>/units4.json:694) · [scope.json](<local>/scope.json:180)

**The central propositions match.** Propositions 7–10 preserve the hypotheses and constants for the fixed-exponent, fixed-label, and anchor counts, including where Lean assumes `RootsOfUnityCount` and `BBCount` and where it discharges them. Proposition 11 correctly works for a finite set of natural-number bases and uses the strict \(20r^3<Y^{3/20}\) comparison. Propositions 12–14 match the numerical conductor check, conditional pool bound, and eventual \(21x^{15}\) estimate. The sharper estimates in the remarks are valid extensions beyond those Lean statements.

## Verdict

An expert would understand from the exposition why the conditional prime-selection proof works, including how the minimum valuation turns a large primary component into a sparse set of possible partners. The digest alone also conveys that argument, including why the surviving prime is distinct, although it takes several items to reconstruct the uniform pool estimate. Neither explains why the larger proof needs two primes with this particular disjointness property. The single best change is to state the residue-characteristic case split immediately after introducing \(BB\), and connect the resulting usable prime to the local type for residual irreducibility.
