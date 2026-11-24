The exposition captures **all eight keyed insights**. The digest captures **seven of eight**. It puts the central selection argument first and explains why a second prime survives. Its substantive omission is what the surviving pair does for each residual characteristic.

## 1. Exposition against the key

| Key insight | Grade | Evidence in `assembled-v10.md` |
|---|---|---|
| 1. Generator congruent to one | Captured | Line 410 gives the integral-basis expression and says “the equations specify the generator … of norm \(p\), congruent to 1 modulo \(N\mathcal O_K\).” Lines 402–406 derive the rational congruence and exhibit a prime satisfying it without the generator. Line 11 connects the congruence to splitting in the host. |
| 2. Uniform dyadic candidate pool | Captured | Line 418 says “the proof uses the assumed estimate at \(h=1\).” Lines 420–424 explain why “the threshold is independent of \(d,N,Y\)” and obtain \(c'Y/(D^A\log Y)\ge Y^{9/10}\) from \(\log D\le10t^2\) and \(\log Y\ge8t^5\). This gets both the size and the quantifier dependence right. |
| 3. At most \(3r+1\) exceptions | Captured | Line 161 says “four of them would have product greater than \(m>n\),” although their product divides \(n\). Lines 178–180 specialize to \(n=g^j-1\), start with the base singleton and add at most three labels per exponent. |
| 4. Minimum valuation gives one large common modulus | Captured | Line 267 says “Taking the minimum gives the largest common modulus. A minimizing base \(g_0\) certifies \(M^4>g_0^j\ge Y\).” Line 269 then gives “at most \(2j\) root classes” with at most \(Y/M+1\) points each. Lines 205–226 explain the factor two. |
| 5. Two unions bound overlap with one prime | Captured | Line 293 says “The base \(g=\ell\) … costs at most one” before summing over partner exponents. Line 315 says “The subsets for these labels cover \(S\), so summing gives” the product bound. Lines 311 and 338 explain why a small forward count alone fails and why counting all integers suffices. |
| 6. Exponent gap leaves a second prime | Captured | Line 356 gives \(Q\le20r^3Y^{3/4}<Y^{9/10}\le |G|\). Line 358 explains distinctness without spending another unit of margin: “The anchor belongs to that subset, so the selected candidate is distinct.” |
| 7. Scale absorbs losses and gives comparable primes | Captured | Line 483 says “The prescribed value 8 satisfies both tests,” after separating the logarithmic window test from the \(3/20\)-power test. Lines 443–446 give the Taylor-term argument, and line 487 gives “\(Y<a,b\le2Y\),” hence comparability within a factor of two. Comparability itself is implicit, and the key’s particular downstream rank inequality is absent. |
| 8. A usable local test in every residual characteristic | Captured | Line 13 says “The choice can depend on \(\ell\). Since \(g_i\) itself is a label, this also gives \(\ell\ne g_i\).” It identifies prime-to-\(\ell\) root separation and residual irreducibility. That captures the purpose of disjointness. The key goes one step further by explaining how the fourth-root cutoff helps construct good finite-field types. |

**Counts:** 8 captured, 0 buried, 0 missed, 0 wrong. These grades credit the mathematical insight even where a downstream example is absent.

Two additions deserve credit. First, line 471 explains why demanding coprimality of the shifted products would defeat the construction: both exponent-one factors are divisible by \(N\). This explains why the proof tests the *size* of a shared primary part. Second, lines 271 and 295 observe that the common modulus actually exceeds \(Y^{j/4}\). For \(j\ge4\) each root class then contributes at most one integer, yielding the stronger, unused overlap bound \(O(rY^{3/4}+r^3)\).

## 2. Digest

I grade each item’s main idea and count distinct key insights for recall. Two items can correctly develop different parts of the same insight.

| Digest item | Class | Key and standalone assessment |
|---|---|---|
| 1. Delete collisions at the original modulus | **a** | Keys 5–7. Stands alone as a conditional selection argument. It defines eligibility and labels, gives both counts, accounts for the anchor, and checks the scale. |
| 2. Minimum valuation | **a** | Key 4. Stands alone. The minimizer explains both common divisibility and the lower bound on the modulus. The example with 9 and 13 shows exactly why the maximum fails. |
| 3. Uniform dyadic count | **a** | Key 2. Stands alone for the conductor test and explains why varying \(d,N\) matter. Item 6 finishes the conversion to a power lower bound. |
| 4. Three labels per exponent | **a** | Key 3. Stands alone by the four-factor contradiction. Its supporting link at line 51 targets `assembled-v7.md`, absent from the supplied directory, but the argument is complete on the page. |
| 5. Sum over the partner’s exponent | **a** | Key 5. Stands alone for the reverse count. It specifies the exceptional event, its per-exponent bound and the separate singleton. The “anchor” enters only to explain why its witness can be forgotten. |
| 6. Budget one tenth for losses | **a** | Key 2. Stands alone for paying the denominator uniformly, including arbitrarily large \(k\). |
| 7. Count generators in the required class | **a** | Key 1. Stands alone. It gives the coordinates and an explicit counterexample to selecting by rational congruence. The host application is absent. |
| 8. Two cyclic cosets at 2 | **a** | An explicit component of key 4. Stands alone, including the modulo-8 example showing why \(j\) roots would be false. It repeats part of item 2. |

**Precision is \(8/8=100\%\). Recall is \(7/8=87.5\%\).** Item 1 earns key 7 through its scale argument, though it leaves comparability implicit. No item earns key 8. **The ranking is design-first for the selection proof:** item 1 gives the decision to count at \(N\) and delete afterward, and item 2 gives the arithmetic reason deletion is cheap. The ranking gives the special case at 2 a separate slot while leaving out the reason two primes are wanted.

## 3. False reasons, literature status and provenance

The clearest mathematical overstatement is digest line 63. It says a gcd bound \(e^{\delta n}\) “would need” \(\delta\le\log Y/(4r)\) at \(i=1,j=r\). That cutoff is **sufficient**. Since the gcd is an integer, even a bound slightly above \(Y^{1/4}\) can rule out a collision if it stays below \(\lfloor Y^{1/4}\rfloor+1\). Exposition line 287 makes the distinction correctly. The objection to applying a fixed-base, large-exponent theorem survives.

The enlarged-modulus objection at exposition line 475 and digest line 7 is valid for the stated proposal of incorporating *every* label, including the anchor. It would overreach as a reason that every congruence strategy must fail. Also, digest line 9’s “dyadic norm count is assumed in Lean” compresses two steps. The root assumes the full `ShortNorm` estimate. The clean \(Y^{9/10}\) count is derived.

The \(A=3\) claim at digest line 43 has identifiable support as **the search author’s specialization** of a cumulative 2019 Thorner–Zaman estimate. `lit.md` lines 284–290 give the endpoint-error, exceptional-zero and degree-two-ideal argument. `sources.md` line 17 identifies a distinct 2017 antecedent. Neither warrants attributing the exact pair theorem or Lean’s proof of `ShortNorm` to Thorner–Zaman. The Hooley, Poonen, Xie and hypergraph comparisons support analogies or individual techniques. I found no priority claim for the exact construction.

**No distinctive wording or fact establishes use of the excluded write-up.** There is a traceability gap worth distinguishing from leakage. `scope-levels.json` stops at level 5 and explicitly leaves the irreducibility connection beyond its cap. Exposition line 13 agrees with key 8, but the supplied trace does not independently verify its detailed Lean citation chain. Similarly, the host-level discharge of `ShortNorm` is documented more directly in the supplied material than the detailed upstream Perron argument at line 17. Those limits affect verification of attribution, not the selection proof.

## 4. Faithfulness to Lean

**The root is conditional on `ShortNorm`.** The implication is explicit at `units4.json` line 302 and exposition lines 38–49 and 456–467. Lines 23–31 state the full hypothesis with uniform positive constants, the conductor restriction, and the range of relative lengths \(h\). Only \(h=1\) is used here. The archive supplies that premise separately at the host level. RH and GRH are not hypotheses of this implication.

The exposition correctly expands `ModAt`, places \(x_0\) before \(x,N,d,k,r\), retains unbounded \(k\ge1\), and translates `Fin 2 → ℕ` into two distinct primes. It preserves `NormOne`, `BB` disjointness, and the closed exported interval. Line 487 correctly records the stronger strict lower endpoint obtained from membership in the candidate pool.

The central propositions also preserve their dependencies. Propositions 7–8 assume the root-count bound, Proposition 9 assumes both incidence inputs, and Proposition 10 discharges them. Proposition 11 selects from an arbitrary finite set of integers. Proposition 13 supplies the norm primes conditionally for **every** \(Y>0\) with \(\log Y\ge8x^\varepsilon\). Proposition 14 supplies the independent exponential comparison. I found no change to a load-bearing hypothesis, inequality or conclusion in this chain.

## 5. Verdict

An expert could reconstruct why the proof works from either text. The exposition also explains why the output has the form the application needs. The digest alone explains how to find the pair, but a reader could finish it without knowing why shared exceptional labels matter. The single most effective change would be to replace digest item 8, whose root-count content already appears in item 2, with the local application: for each residual characteristic choose the prime whose exceptional set omits it, explain how self-exception guarantees \(\ell\ne g_i\), and connect prime-to-\(\ell\) root separation at that prime to residual irreducibility.
