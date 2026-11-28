The exposition captures **7 of the 8 key insights**. The digest has **100% item precision and 87.5% key recall**. Both explain why a second prime survives. Their common omission is why the application needs two primes whose exceptional sets are disjoint.

## 1. Exposition against the key

Line numbers in this section refer to `assembled-v9.md`. I count an insight as captured when its main mathematical mechanism is explicit, even if a downstream example is absent.

| Key insight | Grade | Evidence and assessment |
|---|---|---|
| 1. Generator congruent to one | **Captured** | L408 says “the equations specify the generator … of norm \(p\), congruent to 1 modulo \(N\mathcal O_K\).” L400–404 derives the rational congruence and exhibits \(d=N=103,\ p=619\) as a counterexample to its converse. L11 connects the generator and splitting to the host. |
| 2. Uniform dyadic pool | **Captured** | L416 says “the assumed estimate at \(h=1\),” and L422 gives “\(c'Y/(D^A\log Y)\ge Y^{9/10}\).” L412–422 explains why a fixed-field threshold is insufficient and how \(\log D\le10t^2\) and \(\log Y\ge8t^5\) handle every admissible modulus and window. |
| 3. At most \(3r+1\) exceptions | **Captured** | L159 says “four of them would have product greater than \(m>n\).” The product divides \(n=g^j-1\). L176–180 unions the layers and includes the base singleton. |
| 4. Minimum valuation supplies a common large modulus | **Captured** | L265 says “A minimizing base \(g_0\) certifies \(M^4>g_0^j\ge Y\).” L267 uses that *every* base is a root modulo this same \(M\). L203–224 and L267 give the cyclic-group argument, the factor two at 2, and the spacing bound. |
| 5. Two unions bound overlap | **Captured** | L291 says “The base \(g=\ell\) can carry the label without any exceptional witness and costs at most one.” It sums over the partner’s exponents. L313–317 then sums over the anchor’s labels because “the subsets for these labels cover \(S\).” This bounds all colliding integers. |
| 6. The count gap leaves a second prime | **Captured** | L354 gives “\(Q\le20r^3Y^{3/4}<Y^{9/10}\le |G|\).” L350 and L356 explain why any anchor works and why its survivor is distinct. |
| 7. Prescribed scale absorbs losses and gives comparable primes | **Captured** | L479 says “all larger \(k\) help both comparisons.” L481–485 checks \(\log Y\) and \(Y^{3/20}\) separately, including the strict inequality. L441–445 supplies the Taylor term. The common window makes \(g_i\le2g_j\) immediate, although the text leaves that consequence implicit and omits the key’s downstream rank example. |
| 8. A usable local test in every residue characteristic | **Missed** | The nearest passage, L11, says disjointness is carried into “the cyclic host’s local-type data.” That identifies where the certificate goes. It never explains the choice for each residual \(\ell\), how the valuation cutoff controls collisions of prime-to-\(\ell\) parts, or how the good type at the surviving place is used for residual irreducibility. The level-five scope trace explicitly leaves that connection beyond its cap. |

**Counts:** 7 captured, 0 buried, 1 missed, 0 wrong. For item 8, the purpose itself is absent, even though the host and local types are mentioned.

Two additions deserve credit. First, the norm congruence forces both exponent-one shifts to be divisible by \(N\). This explains why asking for coprime shifted products would defeat the construction and why testing the *size* of a primary component matters (L469). Second, retaining \(M>Y^{j/4}\) gives at most one point per root class for \(j\ge4\), improving the deletion estimate to \(O(rY^{3/4}+r^3)\) (L269, L293). This is a genuine refinement beyond the key. The proof only needs the coarser estimate.

## 2. Digest

I grade the mathematical idea named by each heading. Repeated coverage earns item precision but counts only once toward recall.

| Digest item | Class | Key and stand-alone assessment |
|---|---|---|
| 1. Delete collisions at the original modulus | **a** | Keys 5–7. Stands alone as a selection argument conditional on the stated pool. It defines labels, fixes an arbitrary anchor, compares counts, and pays the polynomial loss at the prescribed scale. |
| 2. Use the minimum valuation | **a** | Key 4. Stands alone. The minimizer certifies size and the minimum certifies divisibility for every base. The maximum-valuation counterexample makes the distinction concrete. |
| 3. Count uniformly in a dyadic interval | **a** | Key 2. Stands alone for the conductor-range check. The cutoff \(25/(2c^2)\) pays for that check alone. Item 6 supplies the separate density-loss calculation. |
| 4. Three labels per exponent | **a** | Key 3. Stands alone through the four-factor contradiction, union, and singleton. Its link to `assembled-v7.md` points outside the supplied files, but the argument is complete on the page. |
| 5. Sum over the partner’s exponent | **a** | Key 5. Stands alone for the reverse count, including the base-label case. Item 1 performs the outer union over the anchor’s labels. |
| 6. Budget one tenth for losses | **a** | Key 2. Stands alone as an estimate in the stated conductor range. It accounts for \(\log\log Y\) even when \(k\) is unbounded. |
| 7. Count generators in the required residue class | **a** | Key 1. Stands alone. It gives both coordinate divisibilities and disproves the progression-only substitute. |
| 8. Count roots in two cyclic cosets at 2 | **a** | An explicit component of key 4. Stands alone, including the small modulus and the example showing why \(j\) roots would be too few. Its contribution to recall is already covered by item 2. |

**Precision** is \(8/8\). **Recall** is \(7/8\), crediting key 7 because item 1 gives the scale and explains the polynomial absorption. **The ranking is design-first for the selection proof.** The first item states the decisive count-and-delete move, and the second explains how the required spacing is obtained. The last item spends a full slot on a detail already present in item 2 while the purpose of the pair gets none.

## 3. Reasons, literature, and provenance

I found no false inference in the core selection proof. Two qualifications matter.

- Digest L7 presents putting the anchor labels into a second norm modulus as an “obvious approach” and gives conductor size as the objection. The inequality is correct, but the proposal has a prior defect. Adding \(\ell\) forces the partner to be \(1\bmod\ell\), which does not enforce avoidance of a large \(\ell\)-part. The exposition itself explains this at L473. Likewise, digest L63’s gcd comparison concerns labels with power witnesses on both sides. A singleton collision needs separate treatment, as L61 allows.
- Exposition L51 says a Thorner–Zaman specialization “gives the premise with \(A=3\).” The cited result is cumulative and counts prime ideals. L414 explains the dyadic specialization. The full premise also allows shrinking \(h\), for which the endpoint errors must be small **relative to the interval main term**. `lit.md` L284–290 supplies that additional argument. Thus \(A=3\) is a claimed corollary with a local derivation, not a verbatim published theorem or a step in the Lean selection proof. `sources.md` independently identifies the 2017 cumulative ray-class antecedent and the archive’s short-interval result. It does not independently verify the 2019 specialization. Similarly, the scope files identify the archive theorem supplying `ShortNorm`, but do not independently establish every Perron and contour detail narrated at exposition L15.

The Hooley, Poonen and hypergraph comparisons support analogies at the stated level. They establish neither priority nor a prior proof of this exact pair assertion. The search limits its absence claim to the sources reviewed. **I found no positive sign of excluded-write-up use** in either output. The minimum valuation, the arbitrary first prime, the constants 20 and 21, and the factorial threshold are independently recoverable from the supplied Lean. The distinctive downstream explanation in the key is precisely what both outputs lack.

## 4. Faithfulness to Lean

**`typePrimesN` explicitly assumes `ShortNorm`.** Its declaration starts `ShortNorm → ∀ eps`, and its proof passes `hS` to `normPrimesN`. The empty top-level `premises` array does not override that signature. Exposition L19–49 correctly states the uniform analytic hypothesis with its conductor and relative-length restrictions, and then the root with the expanded `ModAt` conditions. For fixed \(\varepsilon>0\) and witnesses to `ShortNorm`, one \(x_0\) works for all admissible \(N,d,k,r\). There is no root hypothesis \(k\le r\), no upper bound on \(k\), and no explicit RH or GRH premise. The archive separately supplies `ShortNorm`. Digest L9’s “dyadic norm count is assumed in Lean” compresses this distinction. The raw estimate is assumed by the root, and the \(Y^{9/10}\) pool is proved from it.

The central propositions preserve the packaged statements. Propositions 7–9 retain the root-count and label-count dependencies, Proposition 10 discharges them, and Proposition 11 works for an arbitrary finite candidate set under the strict size gap. Propositions 12–14 preserve the conductor loss, uniform window condition, and exponential bound. The two named primes faithfully unpack `Fin 2 → ℕ`. L485 correctly distinguishes membership in the floor-defined candidate interval \((Y,2Y]\) from the exported closed lower bound.

## 5. Verdict

An expert could reconstruct why the selection works from either text. The exposition proves both incidence bounds and the digest puts their decisive use first. Neither explains why this particular disjointness certificate is worth constructing. The single highest-value change is to put the residual-characteristic argument beside the initial selection summary: for each \(\ell\), choose \(g_i\) with \(\ell\notin BB(r,g_i)\). The singleton ensures \(g_i\ne\ell\), and the valuation bounds control collisions of prime-to-\(\ell\) parts, making the good local type available for the residual irreducibility test. That connects the proof’s most distinctive condition to the task it performs.
