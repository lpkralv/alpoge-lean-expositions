# Two primes with prescribed norm generators and disjoint exceptional labels

## The idea in brief

Count primes with the prescribed norm generator throughout one dyadic interval, choose any one as an anchor, and show that too few integers can share a label with it to exhaust the prime count. A rational congruence alone does not certify the generator, and a bound on how many labels each prime carries does not control how often a single label recurs. The decisive bound comes from counting the bases that carry one fixed exceptional label at one fixed exponent. They all satisfy a root equation modulo a common prime power whose size makes each residue class sparse.

The gcd estimate of Bugeaud, Corvaja and Zannier fixes both bases and takes a common exponent sufficiently large. Here the primes must be chosen in a moving interval, and a shared label can arise at different exponents, even at exponent one. The proof counts eligible primes at the prescribed modulus, fixes any one of them, and deletes every integer in the interval that shares one of its labels. Factorization limits the labels on the chosen prime, and spacing in prime-power residue classes limits the integers carrying each label, so at most $20r^3Y^{3/4}$ integers are deleted. For large $x$ this is less than the guaranteed count of $Y^{9/10}$ eligible primes. [Bugeaud, Corvaja and Zannier](https://link.springer.com/article/10.1007/s00209-002-0449-z)

## Scope: what this theorem does not do

Theorem 15 uses the uniform short-interval count $\mathsf S$ at relative interval length one to guarantee at least $Y^{9/10}$ candidates and leaves its proof to the analytic prime-counting development, which supplies it for the cyclic host directly and for the field host through `shortNorm` (`normPrimesN.lean:149–157`, `NormPrimesImagQuadShortIntervalLowerBound.lean:98`, `NormPrimesImagQuadShortIntervalLowerBoundStatement.lean:8`, `ExistsHostWithPrimesCyclicTwoPower.lean:99`, `HostOfField.lean:15`). Both constructions use the positive scale exponent $\varepsilon$ and the eventual threshold $x_0$ at their chosen scale $x$, substituting the rank parameters for $k\ge1$ and $1\le r\le x^5$ so the dyadic window grows with the scale and the label cutoff fits the collision bound (`levelData.lean:46–54`, `ExistsHostWithPrimesCyclicTwoPower.lean:103–142`, `typePrimesN.lean:102–124`). Both hosts take $N=Q_Sqd$, where the discriminant parameter $d$ must be prime, satisfy $d\equiv3\pmod4$ and be at least $100$ for the count, while $N>0$ and $d\mid N$ give $d\le N$ and the bound on $\log N$ controls the conductor and keeps $N^{C_8}$ below the type-prime window (`hostOfFieldOf.lean:191–198`, `ExistsHostWithPrimesCyclicTwoPower.lean:125–142`, `normPrimesN.lean:131–154`, `levelData.lean:55–77`). The two indexed primes and their distinctness become level data, with the lower endpoint $(k e^{x^\varepsilon})^8$ excluding the two auxiliary primes and the upper endpoint $2(k e^{x^\varepsilon})^8$ combining with $k\le r\le x^5$ to give $\log g_i\le9x^\varepsilon$ on the cyclic route, where positivity and these logarithm bounds let a separate application of $\mathsf S$ produce a prime $T$ with a generator congruent to one modulo $N(g_0g_1)^2$ (`hostOfFieldOf.lean:210–215`, `ExistsHostWithPrimesCyclicTwoPower.lean:147–174`, `ExistsHostWithPrimesCyclicTwoPower.lean:189–193`, `levelPrimeN.lean:92–145`). The norm equation and the two divisibilities $N\mid\eta$ and $2N\mid\xi-2-\eta$ give the field host an integral generator of norm $g_i$ congruent to one modulo $N$, and give both constructions the rational congruence $g_i\equiv1\pmod N$ used with primality to classify the field-host primes as split and prove complete splitting for the cyclic host (`NormOneIffOfSqrt.lean:74–100`, `NormOneModEqOneAndOfDvd.lean:10–23`, `hostOfFieldOf.lean:208–219`, `hostOfFieldOf.lean:237–238`, `ExistsHostWithPrimesCyclicTwoPower.lean:196`, `InhabitedAtLargeScale.lean:204–205`). Disjointness at cutoff $r$ is the certificate that a label on either prime is absent from the other, and the archive carries it into the field host's arithmetic conditions and the cyclic host's local-type data (`hostOfFieldOf.lean:224–227`, `InhabitedAtLargeScale.lean:205`, `RankRecordRowDimensionZero.lean:271`). Uses of individual exceptional-exponent witnesses or of the two cross-prime non-memberships as separate certificates were not traced.

For each residual characteristic $\ell$, disjointness lets the proof choose a type prime $g_i$ with $\ell\notin\mathcal B_r(g_i)$. The choice can depend on $\ell$. Since $g_i$ itself is a label, this also gives $\ell\ne g_i$. At the chosen prime, the good-tuple hypothesis makes the prime-to-$\ell$ part injective on the roots of each local label polynomial. The residual irreducibility proof uses this root separation (`StatementT.lean:19–24`, `MemMaximalIdealIff.lean:215–225`, `ResidualIrreducibleOfTheoremThreePrime.lean:179–204`).

## Where the hypothesis comes from

The cyclic host uses the uniform count $\mathsf S$ directly, and the field host receives the same count through `shortNorm`. For each admissible $d,M$, the archive builds a family from the ray classes of $K=\mathbb Q(\sqrt{-d})$ modulo $M\mathcal O_K$, with the size of the ray class group bounded by $D=4dM^2$. It applies truncated Perron summation and a contour estimate, then uses character orthogonality to extract the cumulative prime-ideal weight in the identity ray class at $X$ and $X(1+h)$. The difference has main term $hX$ before division by the ray class number, and the possible single exceptional real zero costs at most $hX(1-\delta/2)$, where $\delta$ is an absolute positive constant times a negative power of $D$. Taking $c$ small enough in both the conductor and interval-length conditions absorbs the endpoint errors into the remaining margin and gives identity-class weight at least an absolute positive constant times $hX/D^A$. An identity-class ideal of rational prime norm has an integral generator congruent to one modulo $M\mathcal O_K$, and its two coordinates give the norm equation and divisibilities in $\mathsf S$. Shrinking $c$ again lets the proof absorb the $O(\sqrt X)$ weight at higher prime powers and divide by the $O(\log X)$ weight bound per rational prime to obtain the uniform count. The proofs of the zero estimates, the Perron and contour estimates, and the shifted quadratic-form parametrization used to build the family are **not traced**.

## Main theorem

Say that $p$ has the prescribed norm representation at $d,N$ if there are integers $\xi,\eta$ with $\xi^2+d\eta^2=4p$, $N\mid\eta$, and $2N\mid\xi-2-\eta$. For $g\ge2$, let $\mathcal B_r(g)$ consist of $g$ and every prime $\ell$ for which $\ell^{v_\ell(g^j-1)}>g^{j/4}$ for some integer $1\le j\le r$, where $v_\ell$ is the prime valuation. Let $\mathcal P_{d,M}(X,Z)$ consist of the primes in $(X,Z]$ with the prescribed norm representation at $d,M$. The counting hypothesis $\mathsf S$ is the following assertion.

$$
\begin{gathered}
\exists A,c,c'\in\mathbb R,\ A,c,c'>0\ \ \forall d,M\in\mathbb N\ \ \forall X,h\in\mathbb R:\\
d\text{ prime},\quad d\equiv3\pmod4,\quad d\ge100,\quad M\ge3,\quad X\ge1,\quad
\log(4dM^2)\le c\sqrt{\log X},\quad e^{-c\sqrt{\log X}}\le h\le1\\
\Longrightarrow\quad
\left|\mathcal P_{d,M}(X,X(1+h))\right|
\ge \frac{c'hX}{(4dM^2)^A\log X}.
\end{gathered}
$$

**Theorem 15.**

$$
\begin{gathered}
\mathsf S\quad\Longrightarrow\quad
\forall\varepsilon\in\mathbb R,\ \varepsilon>0\ \exists x_0\in\mathbb R\
\forall x\in\mathbb R,\ x\ge x_0\
\forall N,d,k,r\in\mathbb N:\\
d\text{ prime},\quad d\equiv3\pmod4,\quad d\ge100,\quad
N>0,\quad d\mid N,\quad
\log N\le3x^{\varepsilon/5}(\log x)^2,\quad
k\ge1,\quad 1\le r\le x^5\\
\Longrightarrow\quad
\exists a,b\text{ distinct primes in }[Y,2Y],\quad Y=(k e^{x^\varepsilon})^8,\\
a,b\text{ each have the prescribed norm representation at }d,N,\qquad
\mathcal B_r(a)\cap\mathcal B_r(b)=\varnothing.
\end{gathered}
$$

The short-interval lower bound $\mathsf S$ is an analytic premise with absolute constants. The primality, congruence, divisibility, range and positivity conditions on $\varepsilon,x,d,N,k,r$ specify the parameters of the theorem. The premise makes no explicit RH or GRH assumption. The archive proves the full range of $\mathsf S$ with an existential exponent $A$ (`NormPrimesImagQuadShortIntervalLowerBound.lean:98–147`). Decision 2 discusses the dyadic specialization of the cumulative estimate of Thorner and Zaman. [Thorner and Zaman, Theorems 3.3 and 5.1](https://msp.org/ant/2019/13-5/ant-v13-n5-p02-s.pdf)

The classical representation theorems of Weber and Briggs establish infinitude for a fixed primitive positive definite binary quadratic form. The identity ray class imposes the congruence on a generator. Fixed-field Chebotarev estimates give density, Balog and Ono reach short intervals for a fixed extension, and a least-prime estimate controls the first occurrence. A uniform result of Thorner and Zaman supplies the analytic comparison used in Decision 2. Bounded-gap results for Chebotarev sets address a different pair condition. [Weber](https://link.springer.com/article/10.1007/BF01443599) · [Briggs](https://www.cambridge.org/core/services/aop-cambridge-core/content/view/52E50F7ED4AF4D35D1D2EE52AA141903/S0008414X00023786a.pdf/an-elementary-proof-of-a-theorem-about-the-representation-of-primes-by-quadratic-forms.pdf) · [Milne, *Class Field Theory*, Ch. V](https://www.jmilne.org/math/CourseNotes/CFT.pdf) · [Balog and Ono, Theorem 2](https://uva.theopenscholar.com/files/062_8.pdf) · [Thorner and Zaman, least represented prime](https://msp.org/ant/2017/11-5/ant-v11-n5-p04-s.pdf) · [Thorner and Zaman, Theorem 5.1](https://msp.org/ant/2019/13-5/ant-v13-n5-p02-s.pdf) · [Thorner, bounded gaps](https://arxiv.org/pdf/1401.6677)

Effective Chebotarev in terms of the full extension discriminant can require a larger starting point than the conductor range here. Prime-ideal estimates under GRH give another route in varying ray class fields, and upper-bound sieve estimates for represented primes control possible excess in short intervals. The argument here uses the lower-bound premise for the original modulus. [Lagarias and Odlyzko, Theorems 1.1 and 1.3](https://aareyanmanzoor.github.io/assets/articles/lagarias-odlyzko-dyslexic.pdf) · [Grenié, Molteni and Perelli, Theorem 2](https://www.cambridge.org/core/services/aop-cambridge-core/content/view/BFCFB1977DDA0C3A7EAE38BCF5A9E4C8/S0025579316000310a.pdf/primes-and-prime-ideals-in-short-intervals.pdf) · [Zaman, §8](https://arxiv.org/pdf/1710.08914)

## Why the proof is built this way

Decision 1 in Proposition 13 uses a count with the generator congruence, since the corresponding rational progression contains ineligible primes. Decision 2 in Proposition 13 uses a dyadic lower bound uniform in the modulus, since a fixed-field asymptotic leaves its threshold dependent on the field. Decision 3 in Proposition 12 absorbs the conductor and logarithm into a power of the window start, since fixed positive density does not follow from the conductor-dependent lower bound. Decision 4 in Theorem 15 removes colliding integers after counting, since incorporating all the anchor labels into a modulus puts it outside the conductor range. Decision 5 in Proposition 9 counts labels in both directions, since even small label sets can all share one label. Decision 6 in Proposition 8 allows separate witness exponents, since a same-exponent gcd estimate for fixed bases does not control the required mixed-exponent collisions. Decision 7 in Proposition 7 keeps a large common prime power, since reducing modulo its prime leaves too many integers in the permitted classes. Decision 8 in Theorem 15 tests the size of a primary component, since the prescribed norm congruence forces both primes to share a divisor at exponent one.

1. Propositions 1 and 2 use primary factorization to bound the number of labels that can occur on one base.
2. Propositions 3–6 give the root and spacing bounds for counting integers in a common prime-power modulus.
3. Propositions 7 and 8 use these bounds first for one witness exponent and then for all exponents that could give the fixed label.
4. Propositions 9–11 sum over one anchor's labels and select a disjoint pair whenever the available count exceeds the resulting bound.
5. Propositions 12 and 13 use $\mathsf S$ to supply that count uniformly at the original modulus.
6. Proposition 14 and Theorem 15 show that the prescribed window is large enough for both the analytic count and the elementary selection.

## Notation

| Symbol | Meaning |
|---|---|
| $\mathbb N$, $\mathbb Z$, $\mathbb R$, $\mathbb Q$ | Nonnegative integers, integers, reals, and rationals, respectively |
| $\varepsilon$ | Positive real exponent parameter of the theorem |
| $x$ | Real size parameter |
| $x_0$ | Eventual threshold for $x$ |
| $k$ | Natural multiplier in the window start |
| $E$ | Exponential $e^{x^\varepsilon}$ |
| $e$ | Base of the natural logarithm |
| $Y$ | Start of the dyadic window $[Y,2Y]$, equal to $(kE)^8$ in the main theorem |
| $X$ | Generic lower endpoint in the prime-counting hypothesis |
| $Z$ | Generic upper endpoint for the norm-prime set |
| $h$ | Relative interval length in the prime-counting hypothesis |
| $r$ | Upper cutoff for positive witness exponents |
| $j$ | Positive power exponent, including the second witness when there are two |
| $i$ | First witness exponent in the mixed-exponent comparison |
| $f$ | Common exponent $\operatorname{lcm}(i,j)$ |
| $\delta$ | Exponent coefficient in the gcd comparison |
| $d$ | Prime parameter of the quadratic norm form |
| $N$ | Prescribed congruence modulus in the main application |
| $M$ | General positive integer modulus |
| $p$ | Prime considered for the prescribed norm representation |
| $\xi$, $\eta$ | Integer coordinates in the norm equation $\xi^2+d\eta^2=4p$, with $M\mid\eta$ and $2M\mid\xi-2-\eta$ for modulus $M$ |
| $u$, $v$ | Integer coefficients in $\xi=2+\eta+2Nu$, $\eta=Nv$ |
| $K$ | Imaginary quadratic field $\mathbb Q(\sqrt{-d})$ |
| $\mathcal O_K$ | Ring of integers of $K$ |
| $\mathcal P_{d,M}$ | Set-valued function with $\mathcal P_{d,M}(X,Z)$ the primes in $(X,Z]$ with the prescribed norm representation at $d,M$ |
| $\ell$ | Natural label, required to be prime when exceptional |
| $\ell_0$ | Hypothetical label common to an entire family |
| $v_\ell$ | Prime valuation on positive integers, zero when the argument is indivisible by $\ell$ |
| $n$ | Positive integer whose primary components are counted |
| $m$ | Integer compared with the fourth powers of the primary components of $n$ |
| $q$ | Alternative positive integer power in the primary-component test |
| $g$ | Integer base |
| $g'$ | Second integer base in the spacing estimate |
| $g_0$ | Minimizing base in a finite family, with the quantity minimized specified in the proof |
| $a$ | First selected base or anchor |
| $b$ | Second selected base |
| $\mathcal E_j$ | Exceptional-label function, with $\mathcal E_j(g)=\{\ell:\ell\text{ prime},\ g^j<\ell^{4v_\ell(g^j-1)}\}$ for $g\ge2$ and $j\ge1$ |
| $\mathcal B_r$ | Label-set function, with $\mathcal B_r(g)=\{g\}\cup\bigcup_{1\le j\le r}\mathcal E_j(g)$ for $g\ge2$ |
| $w$ | Exponent of a prime-power modulus |
| $s$ | Least exponent giving a prime power above the spacing threshold |
| $z$ | Group element or residue tested for being a power root |
| $y$ | Real argument in an elementary analytic inequality |
| $\Gamma$ | Finite group in a root count |
| $H$ | Cyclic subgroup of $\Gamma$ |
| $J$ | Kernel of the power map on $\Gamma$ |
| $T$ | Finite set counted in a spacing or fixed-label bound |
| $S$ | Finite set of bases colliding with an anchor |
| $G$ | Finite set of candidates for the disjoint pair |
| $Q$ | Anchor collision bound $(3r+1)(1+2r^2(Y^{3/4}+1))$ |
| $\mathsf F$ | Forward label bounds, the assertion of Proposition 2 |
| $\mathsf R$ | Uniform prime-power root bounds, the assertion of Proposition 5 |
| $\mathsf S$ | Uniform lower-bound hypothesis, stated in the overview |
| $A$ | Positive conductor-loss exponent |
| $c$ | Positive constant in the conductor and interval tests |
| $c'$ | Positive coefficient of the prime-count lower bound |
| $D$ | Conductor parameter $4dN^2$ |
| $W$ | Positive real conductor parameter in the numerical estimate |
| $L$ | Logarithm $\log Y$ |
| $t$ | Auxiliary scale, instantiated as $x^{\varepsilon/5}$ |
| $\theta$ | Generic exponent in a lower bound for the count |
| $\sigma$ | Alternative exponent of the conductor comparison scale $t$ |
| $C$ | Positive coefficient in the comparison $L\ge Ct^\sigma$ |
| $b_*$ | Coefficient used in place of 10 in the coarse conductor bound |
| $\beta$ | Possible exceptional real zero in the analytic comparison |
| $\rho$ | Exceptional-zero density factor, $\rho(Y)=1-Y^{\beta-1}$ when the zero is present and $\rho(Y)=1$ otherwise |
| $\nu$ | Natural Taylor degree |
| $\mu$ | Alternative exponent in the window start $(kE)^\mu$ |
| $\kappa$ | Fixed exponent in the alternative polynomial bound on $r$ |
| $\lambda$ | Arbitrary positive comparison exponent in the logarithmic growth fact |
| $\log$, $\exp$ | Natural logarithm and exponential |
| $\gcd$, $\operatorname{lcm}$ | Greatest common divisor and least common multiple |
| $\lfloor\cdot\rfloor$, $\lceil\cdot\rceil$ | Floor and ceiling |
| $\lvert\cdot\rvert$, $[\Gamma:H]$ | Cardinality of a finite set and index of a subgroup |
| $O$, $o$, $\gg$ | Big-O, little-o, and lower bound up to a positive multiplicative constant |

All logarithms, divisions and valuations in the arguments are taken in their ordinary domains. A shared label can come either from the base singleton or from a prime in one of the exceptional sets.

## Proposition 1. Large primary components

$$
\begin{gathered}
\forall n,m\in\mathbb N,\quad 0<n<m\ \Longrightarrow\\
\{\ell:\ell\text{ prime},\ m<\ell^{4v_\ell(n)}\}
\text{ is finite and has cardinality at most }3.
\end{gathered}
$$

**Proof.** A prime not dividing $n$ has valuation zero, so the inequality for it would read $m<1$, impossible for $m>n\ge1$. All qualifying primes lie among the finitely many prime divisors of $n$. In particular there are none at $n=1$. The product of the primary components coming from any distinct prime divisors divides the positive integer $n$. Each qualifying primary component exceeds $m^{1/4}$, so four of them would have product greater than $m>n$. This explains the bound of three and also why the same fourth power will yield a modulus of at least the fourth-root scale in Proposition 7. With a positive integer $q$ in place of 4 the same product argument gives at most $q-1$ such primes, and the spacing argument gives exponent $1-1/q$. For a growing power margin against $Y^{9/10}$ at fixed $r$ one needs $q<10$ in this comparison. The case $n=0$ lies outside the positive-integer factorization argument.

**Remarks.** The fourth power is one choice in that range. The strict component inequalities would even allow $m=n\ge1$, whereas the conclusion is needed here only at the consecutive values $n=g^j-1$ and $m=g^j$.

## Proposition 2. Labels carried by a base

$$
\begin{gathered}
\forall g\in\mathbb N,\quad g\ge2\ \Longrightarrow\\
\bigl(\forall j\in\mathbb N,\ j\ge1:\ 
\mathcal E_j(g)\text{ is finite and }|\mathcal E_j(g)|\le3\bigr)
\quad\text{and}\quad
\bigl(\forall r\in\mathbb N:\ 
\mathcal B_r(g)\text{ is finite and }|\mathcal B_r(g)|\le3r+1\bigr).
\end{gathered}
$$

**Proof.** The subtraction in $g^j-1$ gives the divisibility condition for a root of unity and makes the positive integer to be factored smaller than $g^j$, so Proposition 1 applies with $n=g^j-1$ and $m=g^j$. For instance, at $g=2,j=1$ the subtracted input is 1 and yields no exceptional prime. Using the input 2 would declare $\ell=2$ exceptional since $2<2^4$, although $2$ is zero modulo 2. At $g=1$ or $j=0$ the subtracted input is zero and the positive-integer argument does not apply.

At $r=0$, the witness range is empty and $\mathcal B_0(g)=\{g\}$. Increasing $r$ to $r+1$ adds just the layer $\mathcal E_{r+1}(g)$, since every witness either belonged to the previous range or equals $r+1$. The layer has at most three elements. Induction gives the total bound, allowing overlaps with the old layers and the singleton.

**Remarks.** Only the total bound is used downstream, and the separate per-exponent bound supplies the induction step. Taking the finite union over all exponents at once also gives $1+3r$.

## Proposition 3. Power roots and a cyclic subgroup

$$
\forall\text{ finite abelian groups }\Gamma\
\forall\text{ cyclic subgroups }H\le\Gamma\
\forall j\in\mathbb N,\quad j\ge1\ \Longrightarrow\
|\{z\in\Gamma:z^j=1\}|\le[\Gamma:H]j.
$$

**Proof.** The roots form the kernel $J$ of the $j$-th power map on $\Gamma$. Under the quotient map to $\Gamma/H$, the image of $J$ has size $[J:J\cap H]$. Each occupied coset contains exactly $|J\cap H|$ roots, and the cyclic group $H$ has at most $j$ such roots by the classical cyclic root count. Thus $|J|\le[\Gamma:H]j$. At $j=0$ the kernel is the whole group and the proposed bound would be zero.

**Remarks.** The group bound is stated for arbitrary cyclic subgroups of finite abelian groups, though only the index-two subgroup generated by 5 is needed. The index $[J:J\cap H]$ divides $[\Gamma:H]$ since it is the size of the image subgroup in $\Gamma/H$. Taking $H=\Gamma$ recovers the cyclic bound.

## Proposition 4. Roots modulo a power of two

$$
\forall w,j\in\mathbb N,\quad
w\ge1,\ j\ge1\ \Longrightarrow\
|\{z\in\mathbb Z/2^w\mathbb Z:z^j=1\}|\le2j.
$$

**Proof.** The bound $j$ for odd prime powers cannot be carried over to powers of two. All four odd residues square to 1 modulo 8, giving equality in $2j$ when $w=3,j=2$. Counting all units gives a bound of $2j$ only when $j\ge2^{w-2}$ for $w\ge2$, so we count roots within a cyclic subgroup and its other coset. Every root is a unit since $j>0$. For $w\ge2$ the unit group has order $2^{w-1}$ and 5 has order $2^{w-2}$, so the cyclic subgroup generated by 5 has index two. Proposition 3 bounds the number of roots by $2j$ for every positive $j$. [Gauss, *Disquisitiones Arithmeticae*, Arts. 89–90](https://en.wikisource.org/wiki/Translation:Disquisitiones_Arithmeticae/Third_Section#Article_89)

Root count — precedent found. The proof applies the cyclic-subgroup index bound of Proposition 3 to the signed powers of 5 in Gauss’s description of the units. [Gauss, Arts. 89–91](https://en.wikisource.org/wiki/Translation:Disquisitiones_Arithmeticae/Third_Section)

For $w=1$ the unit group is trivial, so the cyclic bound suffices on its own. At $w=2$ the subgroup generated by 5 is trivial, and the full unit group is cyclic of order two. At the excluded $w=0$ the modulus is 1 and there is one residue, which is a root. At the excluded $j=0$ every residue is a root and the claimed bound would be zero.

**Remarks.** Any cyclic subgroup of index two would give the same bound. The order formula makes the subgroup generated by 5 explicit.

## Proposition 5. Roots modulo prime powers

$$
\begin{gathered}
\forall\ell,w,j\in\mathbb N,\quad \ell\text{ prime},\ w\ge1,\ j\ge1
\ \Longrightarrow\\
\bigl(\ell\ne2\ \Longrightarrow\ |\{z\in\mathbb Z/\ell^w\mathbb Z:z^j=1\}|
       \le j\ell^{v_\ell(j)}\bigr)
\quad\text{and}\quad
|\{z\in\mathbb Z/\ell^w\mathbb Z:z^j=1\}|\le2j.
\end{gathered}
$$

**Proof.** At an odd prime the units modulo $\ell^w$ are cyclic, and all roots are units. The cyclic root count gives at most $j$ roots, implying both bounds in that case. At $\ell=2$ use Proposition 4. [Gauss, *Disquisitiones Arithmeticae*, Arts. 89–90](https://en.wikisource.org/wiki/Translation:Disquisitiones_Arithmeticae/Third_Section#Article_89)

**Remarks.** The reverse count uses only the $2j$ bound, which holds for all primes. The displayed odd-prime bound is weaker than the cyclic bound available in its proof.

## Proposition 6. Spacing in one residue class

$$
\begin{gathered}
\forall Y\in\mathbb R\ \forall M\in\mathbb N\ \forall\text{ finite }T\subseteq\mathbb N,\quad
Y\ge0,\ M>0,\ T\subseteq[Y,2Y],\\
(\forall g,g'\in T,\ g\equiv g'\pmod M)
\quad\Longrightarrow\quad |T|\le Y/M+1.
\end{gathered}
$$

**Proof.**

Heuristic: With one possible point every $M$ integers, the spacing count has leading scale $Y/M$ when the window is long compared with the modulus.

If $T$ is empty the bound holds immediately. Otherwise let $g_0=\min T$. Subtracting the minimum and dividing by $M$ makes the spacing explicit. The coordinate $(g-g_0)/M$ is a nonnegative integer for every $g\in T$, and distinct points give distinct coordinates. The difference $g-g_0$ is at most $Y$, so there are at most $\lfloor Y/M\rfloor+1$ coordinates. The $+1$ counts the coordinate zero of the minimum, the only coordinate when $T$ is a singleton. Using $g/M$ without shifting the origin preserves the spacing but gives a shifted coordinate interval. Ignoring congruence would give only $\lfloor Y\rfloor+1$. At $Y=0$ the interval is the singleton $\{0\}$, which attains the bound. At $M=0$ the normalization would be undefined.

**Remarks.** The argument uses just the length of the interval. When $M>Y$ a class has at most one point, and when $M=Y>0$ a two-point class must consist of both endpoints. One could also sum the adjacent gaps, each at least $M$.

## Proposition 7. Bases sharing an exceptional prime at one exponent

$$
\begin{gathered}
\mathsf R\ \Longrightarrow\
\forall Y\in\mathbb R\ \forall\ell,j\in\mathbb N\ \forall\text{ finite }T\subseteq\mathbb N,\\
Y\ge2,\quad j\ge1,\quad
T\subseteq[Y,2Y],\quad (\forall g\in T,\ \ell\in\mathcal E_j(g))
\ \Longrightarrow\ |T|\le 2j(Y^{3/4}+1).
\end{gathered}
$$

Here $\mathsf R$ is the assertion of Proposition 5.

**Proof. Decision 7.** Modulo a prime $\ell$, the condition $g^j\equiv1\pmod\ell$ gives $\gcd(j,\ell-1)$ root classes, so spacing bounds the number of integers satisfying it by $\gcd(j,\ell-1)(\lfloor Y/\ell\rfloor+1)$. For fixed $\ell,j$ the exponent of $Y$ is still 1. At $\ell=2,j=1$ every prime in $(Y,2Y]$ is odd, and the odd class alone contains $Y/2+O(1)$ integers, more than the guaranteed $Y^{9/10}$ for sufficiently large $Y$. A large common power of $\ell$ reduces the cost per class to $Y^{3/4}+1$ with the uniform bound $2j$ on the number of classes. The example modulo 8 in Proposition 4 shows why the factor two matters. [Gauss, *Disquisitiones Arithmeticae*, Arts. 89–90](https://en.wikisource.org/wiki/Translation:Disquisitiones_Arithmeticae/Third_Section#Article_89)

Heuristic: A common modulus of size at least $Y^{1/4}$ leaves a spacing cost of order at most $Y^{3/4}$ in each class, so a bounded number of root classes gives that same power of $Y$ at fixed $j$.

The empty set gives count zero and supplies no minimizing candidate. For nonempty $T$, exceptionality implies that $\ell$ is prime. A common modulus $M=\ell^w$ needs $w\le\min_{g\in T}v_\ell(g^j-1)$ for all the power divisibilities, and $M\ge Y^{1/4}$ suffices for the spacing bound. Taking the minimum gives the largest common modulus. A minimizing base $g_0$ certifies $M^4>g_0^j\ge Y$, and $w=0$ would instead require $g_0^j<1$, an impossibility. The maximum valuation can lose candidates. At $Y=8,\ell=2,j=1$, the bases 9 and 13 are both exceptional with valuations 3 and 2 respectively, but 13 is not 1 modulo 8.

Thus every $g\in T$ is a root of $z^j=1$ modulo $M$. By $\mathsf R$ there are at most $2j$ root classes. Proposition 6 gives at most $Y/M+1\le Y^{3/4}+1$ points in each, and summing gives the bound.

**Remarks.** Choosing the least positive integer $s$ with $\ell^s>Y^{j/4}$ before inspecting the candidates also works, since every qualifying valuation is at least $s$. This choice gives the same spacing bound using the same classical prime-power unit groups. Keeping the stronger inequality $M^4>g_0^j\ge Y^j$ gives at most $Y^{1-j/4}+1$ points per class for $j=1,2,3$, and at most one when $j\ge4$. The uniform estimate drops that dependence to simplify the sum over exponents.

Common prime power — partial precedent. Bugeaud, Evertse and Győry count polynomial roots by residue classes for specified primary parts. Here the minimum realized valuation gives one modulus for all the bases at a given exponent. [Bugeaud, Evertse and Győry, Theorem 2.3 and Lemma 3.2](https://irma.math.unistra.fr/~bugeaud/travaux/BuEvGy-AAdef.pdf)

## Proposition 8. Bases sharing a fixed label

$$
\begin{gathered}
\mathsf R\ \Longrightarrow\
\forall Y\in\mathbb R\ \forall\ell,r\in\mathbb N\ \forall\text{ finite }T\subseteq\mathbb N,\\
Y\ge2,\quad T\subseteq[Y,2Y],\quad
(\forall g\in T,\ \ell\in\mathcal B_r(g))
\ \Longrightarrow\ |T|\le1+2r^2(Y^{3/4}+1).
\end{gathered}
$$

**Proof. Decision 6.** Selecting distinct primes $a,b$ first and using a same-exponent gcd estimate would have to handle an exceptional label with two possibly different witnesses $i,j$. Such a label gives a divisor $\ell^{\min(v_\ell(a^i-1),v_\ell(b^j-1))}>Y^{\min(i,j)/4}$ of $\gcd(a^f-1,b^f-1)$ at $f=\operatorname{lcm}(i,j)$. Since the gcd is an integer, an upper bound $e^{\delta f}<\lfloor Y^{\min(i,j)/4}\rfloor+1$ rules out the collision. In particular, it suffices to take $\delta\le\log Y\cdot\gcd(i,j)/(4\max(i,j))$. At $i=1,j=r$ this sufficient cutoff is $\log Y/(4r)$, which tends to zero along $k=1,\varepsilon=1,r=\lfloor x^5\rfloor$. Also $f$ can equal 1, the bases vary, and collisions through a base label would still need separate treatment. The estimates of Bugeaud, Corvaja and Zannier concern fixed multiplicatively independent bases and sufficiently large exponents, and the extension to different exponents discussed by Corvaja works in a fixed finitely generated group. The reverse count instead allows every second witness $1\le j\le r$ independently of how the label arose at the anchor. [Bugeaud, Corvaja and Zannier](https://link.springer.com/article/10.1007/s00209-002-0449-z) · [Corvaja, Theorems 2–3](https://www.kurims.kyoto-u.ac.jp/~kyodo/kokyuroku/contents/pdf/1710-01.pdf)

Independent witnesses — partial precedent. Poonen treats independent coordinates for fixed polynomials. Here one fixes the shared label and sums a uniform bound over the entire range of second exponents. [Poonen, Lemma 5.1](https://math.mit.edu/~poonen/papers/sqfree.pdf)

Heuristic: There are $r$ possible second exponents and the number of root classes at each is of order at most $r$. The resulting count has scale at most $r^2Y^{3/4}$, apart from the possible base label itself.

The base $g=\ell$ can carry the label without any exceptional witness and costs at most one. Every other base lies in a subset counted by Proposition 7 for at least one exponent $j$ from 1 to $r$. Each subset has size at most $2j(Y^{3/4}+1)\le 2r(Y^{3/4}+1)$, and summing over the $r$ exponents gives $1+2r^2(Y^{3/4}+1)$. At $r=0$ the exceptional union is empty and only the possible base $g=\ell$ contributes. For a nonprime label, including 0 or 1, only that same base contribution can occur.

**Remarks.** Summing the individual bounds directly gives $1+r(r+1)(Y^{3/4}+1)$, with the same powers of $r$ and $Y$. Keeping the exponent-dependent spacing gives $1+2Y^{3/4}+4Y^{1/2}+6Y^{1/4}+r(r+1)$ for $r\ge3$, since each $j\ge4$ costs at most $2j$. After summing over the anchor's labels this yields $O(rY^{3/4}+r^3)$ in place of $O(r^3Y^{3/4})$. The argument allows composite bases, although the final application uses only primes.

## Proposition 9. Collisions with one anchor

$$
\begin{gathered}
\mathsf F\ \text{and}\ \mathsf R\ \Longrightarrow\\
\forall Y\in\mathbb R\ \forall r,a\in\mathbb N\ \forall\text{ finite }S\subseteq\mathbb N,\\
Y\ge2,\quad r\ge1,\quad a\in[Y,2Y],\quad S\subseteq[Y,2Y],\quad
(\forall g\in S,\ \mathcal B_r(g)\cap\mathcal B_r(a)\ne\varnothing)\\
\Longrightarrow\quad |S|\le (3r+1)\bigl(1+2r^2(Y^{3/4}+1)\bigr).
\end{gathered}
$$

Here $\mathsf F$ and $\mathsf R$ are the assertions of Propositions 2 and 5.

**Proof. Decision 5.** The forward bound $3r+1$ alone allows sets of the form $\{g,\ell_0\}$ with one common label $\ell_0$, so every ordered pair can collide, even among a number of bases of order $Y$.

Heuristic: At fixed $r$ the count per label grows at most like $Y^{3/4}$, and an anchor contributes at most $3r+1$ labels. Allowing $r$ to vary gives a total scale of at most $r^3Y^{3/4}$.

Fix one anchor and list its at most $3r+1$ labels by $\mathsf F$. For each such label the reverse count in Proposition 8 gives at most $1+2r^2(Y^{3/4}+1)$ bases. It is this reverse bound that drops the exponent from 1 to $3/4$ for fixed $r$, below the available $9/10$. The subsets for these labels cover $S$, so summing gives
$$
Q=(3r+1)\bigl(1+2r^2(Y^{3/4}+1)\bigr)
$$
as an upper bound, including the anchor itself whenever it is in $S$. Counting all bad ordered pairs in a candidate set $G$ would now also work, since there are at most $|G|Q$ and this is less than $|G|^2$ when $Q<|G|$. Fixing one anchor saves that summation. Thorner's bounded-gap theorem for primes in a fixed Chebotarev set supplies neither a pair in each prescribed interval nor a restriction on shared labels. [Thorner, Theorem 1.1](https://arxiv.org/pdf/1401.6677)

Selection by incidence counts — precedent found. In a hypergraph, the size of an edge and the maximum number of edges through a vertex bound the number of edges meeting it. Here the edges are the candidate label sets, and both incidence bounds come from arithmetic. [Balliu et al., §1](https://arxiv.org/pdf/2211.01945)

**Remarks.** The argument uses the total label bound in $\mathsf F$. It extends to $r=0$, when a collision forces $g=a$ and the product bound is 1.

## Proposition 10. Unconditional collision bound

$$
\begin{gathered}
\forall Y\in\mathbb R\ \forall r,a\in\mathbb N\ \forall\text{ finite }S\subseteq\mathbb N,\\
Y\ge2,\quad r\ge1,\quad a\in[Y,2Y],\quad S\subseteq[Y,2Y],\quad
(\forall g\in S,\ \mathcal B_r(g)\cap\mathcal B_r(a)\ne\varnothing)\\
\Longrightarrow\quad |S|\le (3r+1)\bigl(1+2r^2(Y^{3/4}+1)\bigr).
\end{gathered}
$$

**Proof.** Propositions 2 and 5 establish $\mathsf F$ and $\mathsf R$, so Proposition 9 applies.

**Remarks.** The bound is for arbitrary integer bases in the interval, which makes it independent of the source of the candidates.

## Proposition 11. Selection of a disjoint pair

$$
\begin{gathered}
\forall Y\in\mathbb R\ \forall r\in\mathbb N\ \forall\text{ finite }G\subseteq\mathbb N,\\
Y\ge2,\quad r\ge1,\quad 20r^3<Y^{3/20},\quad G\subseteq[Y,2Y],\quad Y^{9/10}\le |G|\\
\Longrightarrow\quad
\exists a,b\in G,\quad a\ne b,\quad
\mathcal B_r(a)\cap\mathcal B_r(b)=\varnothing .
\end{gathered}
$$

**Proof.** The count is positive, so fix any anchor $a\in G$. If there is no disjoint pair, each candidate distinct from $a$ meets the anchor's label set. The candidate $a$ also meets that set, since $a$ belongs to $\mathcal B_r(a)$ by its defining singleton. Thus the whole of $G$ would satisfy the collision hypothesis in Proposition 10.

Heuristic: For fixed $r$, the leading term of $Q$ grows as $2r^2(3r+1)Y^{3/4}$, and $Y^{9/10}$ supplies a factor $Y^{3/20}$ beyond the spacing scale. When $r$ varies, that factor must pay a coefficient of order $r^3$.

For $r\ge1$ and $Y\ge2$, we have $3r+1\le4r$ and $1+2r^2(Y^{3/4}+1)\le5r^2Y^{3/4}$. Thus the exact collision bound satisfies $Q\le20r^3Y^{3/4}<Y^{9/10}\le |G|$, a contradiction. The sufficient condition is equivalently $Y>(20r^3)^{20/3}$ or $r<20^{-1/3}Y^{1/20}$, so a fixed lower cutoff for $Y$ cannot suffice in this comparison when $r$ is unbounded. At $r=0$, outside this comparison, all label sets are singletons and $Y^{9/10}>1$ already supplies two disjoint ones.

**Remarks.** Equivalently, apply the collision bound to the subset that meets the anchor and choose a candidate outside it. The anchor belongs to that subset, so the selected candidate is distinct. Using the exact $Q$ in this comparison gives more room than the bound $20r^3Y^{3/4}$.

## Proposition 12. The conductor test and the loss in the count

$$
\begin{gathered}
\forall A,c,c',t,W,Y\in\mathbb R,\quad
A>0,\quad c>0,\quad t\ge10000,\quad t\ge50A,\quad t\ge13/c^2,\quad
40e^{-t/20}\le c',\\
W>1,\quad\log W\le10t^2,\quad Y>0,\quad 8t^5\le\log Y\\
\Longrightarrow\quad
Y\ge1,\quad \log W\le c\sqrt{\log Y},\quad
Y^{9/10}\le\frac{c'Y}{W^A\log Y}.
\end{gathered}
$$

**Proof. Decision 3.** One could carry the raw lower bound all the way to the final selection. With $D=4dN^2$, $L=\log Y$ and $t=x^{\varepsilon/5}$ in the application, the ratio of the lower bound to $20r^3Y^{3/4}$ is $c'Y^{1/4}/(20r^3D^A L)$. Its logarithm tends to infinity uniformly: $A\log D\le10At^2$, $3\log r\le15\log x$, $L\ge8t^5$, and $\log L/L$ tends to zero uniformly above that lower endpoint. Dropping the conductor loss to claim a fixed positive multiple of $Y/\log Y$ would require more: for $d=103$ even $N=103\lfloor x\rfloor$ is admissible eventually at fixed $\varepsilon>0$, and then $D^{-A}$ tends to zero. Absorbing the full denominator into $Y^{1/10}$ now keeps the conductor out of the selection. The raw exponent margin before losses is $1/4$, and the margin after this step is $9/10-3/4=3/20$.

Heuristic: At the least permitted $L$, the logarithmic conductor can be of order $t^2$ whereas $\sqrt L$ has order $t^{5/2}$. For fixed $A,c,c'>0$, the loss $A\log W+\log L-\log c'$ is $o(L)$ uniformly over $L\ge8t^5$, so the lower-bound expression has the scale $Y^{1-o(1)}$.

For the exact argument, $L=\log Y\ge8t^5>0$, so $Y>1$. The conductor comparison is equivalent to $L\ge(\log W/c)^2$. At the worst allowed endpoints $\log W=10t^2$ and $L=8t^5$, it requires $100t^4\le8c^2t^5$, or $t\ge25/(2c^2)$. Thus a cutoff independent of $c$ cannot guarantee the comparison at these endpoints as $c$ tends to zero. The slightly larger $13/c^2$ is sufficient.

The conductor comparison alone does not pay for $W^A L/c'$. For $Y^{9/10}$ the exact remaining test is $A\log W+\log L-\log c'\le L/10$. In general, to get $Y^\theta$ from this expression one needs $\theta\le1-(A\log W+\log L-\log c')/L$. At $\log W=10t^2$ with $t,L$ fixed, the test for $9/10$ is $c'\ge L\exp(10At^2-L/10)$, which fails for arbitrarily large $A$ or arbitrarily small positive $c'$. The assumption $t\ge50A$ makes $A\log W\le t^3/5$. The bound $40e^{-t/20}\le c'$ is equivalent to $t\ge20\log(40/c')$ for $c'>0$, and gives $-\log c'\le t/20$.

The inequality $\log(L/40)\le L/40-1$ gives $\log L\le38+L/40$ since $\log40\le39$. An upper bound for $\log L$ obtained by evaluating at $L=8t^5$ would fail as soon as $L>8t^5$, so we allocate the fixed fraction $L/40$ for all $L$. The other terms obey $38+t^3/5+t/20\le3t^5/5\le3L/40$ for $t\ge10000$, since each of the three summands is at most $t^5/5$. This proves the test, and exponentiating and dividing by the positive denominator proves the lower bound. At $L=0$ the logarithm $\log L$ is undefined and the counting denominator vanishes. The hypotheses exclude that value and imply $c'>0$. At $W=1$ the conductor test would be automatic and $W^A=1$, and at $A=0$ only the loss $L/c'$ would remain.

**Remarks.** With the coarse conductor bound, $L\ge C t^\sigma$ for fixed $C>0$ suffices for the conductor comparison when $\sigma>4$, or when $\sigma=4$ and $C\ge100/c^2$. The worst endpoints fail eventually for $\sigma<4$. The count loss already fits when $\sigma>2$ with $A,c'>0$ fixed. The power 5 leaves room in both estimates, and $t\ge3$ would suffice in the inequality $38+t^3/5+t/20\le3t^5/5$ with the other hypotheses retained. The asymptotic comparison with $Y^{1-o(1)}$ also permits any fixed count exponent strictly between $3/4$ and 1.

## Proposition 13. The uniform dyadic norm-prime count

$$
\begin{gathered}
\mathsf S\ \Longrightarrow\
\forall\varepsilon\in\mathbb R,\ \varepsilon>0\ \exists x_0\in\mathbb R\
\forall x\in\mathbb R,\ x\ge x_0\
\forall N,d\in\mathbb N\ \forall Y\in\mathbb R:\\
d\text{ prime},\quad d\equiv3\pmod4,\quad d\ge100,\quad
N>0,\quad d\mid N,\quad
\log N\le3x^{\varepsilon/5}(\log x)^2,\quad
Y>0,\quad 8x^\varepsilon\le\log Y\\
\Longrightarrow\quad Y^{9/10}\le|\mathcal P_{d,N}(Y,2Y)|.
\end{gathered}
$$

**Proof. Decision 1.** Counting primes in the rational progression $p\equiv1\pmod N$ would enforce a necessary condition. In the norm equations write $\eta=Nv$ and $\xi=2+\eta+2Nu$ with $u,v\in\mathbb Z$. Expansion gives
$$
p=1+N(2u+v)+N^2\bigl(u^2+uv+(d+1)v^2/4\bigr).
$$
Since $d\equiv3\pmod4$, the last bracket is integral. The converse fails even for admissible modulus data: at $d=N=103$, the prime $p=619=1+6\cdot103$ satisfies the rational congruence. If $\eta\ne0$, then $d\eta^2\ge103^3=1092727>2476=4p$. If $\eta=0$, then $\xi^2=4p$ would make $p$ a square. This is a failure of the proposed membership implication, independent of the eventual size of the prime window.

The shift by 2 gives $\xi\equiv2\pmod d$, and the expansion gives $p\equiv1\pmod d$ since $d\mid N$. The homogeneous congruence $2N\mid\xi-\eta$ would force $d\mid\xi$ and $d\mid\eta$, so $d^2\mid4p$, impossible for the allowed odd prime $d$ and prime $p$. At $N=1$ the two congruences agree modulo 2. At $N=0$ the prescribed divisibilities force $\eta=0$ and $\xi=2$, giving $p=1$.

In $K=\mathbb Q(\sqrt{-d})$ the equations specify the generator $(\xi-\eta)/2+\eta(1+\sqrt{-d})/2$ of norm $p$, congruent to 1 modulo $N\mathcal O_K$. The identity ray class encodes this generator congruence. The fixed-form infinitude results of Weber and Briggs give the earlier representation theorem. [Milne, *Class Field Theory*, Ch. V](https://www.jmilne.org/math/CourseNotes/CFT.pdf) · [Weber](https://link.springer.com/article/10.1007/BF01443599) · [Briggs](https://www.cambridge.org/core/services/aop-cambridge-core/content/view/52E50F7ED4AF4D35D1D2EE52AA141903/S0008414X00023786a.pdf/an-elementary-proof-of-a-theorem-about-the-representation-of-primes-by-quadratic-forms.pdf)

Generator congruence — precedent found. Ray class reciprocity supplies the identity class. Here its generator condition becomes the two divisibilities on the integer coordinates. [Milne, Ch. V, §§1 and 3](https://www.jmilne.org/math/CourseNotes/CFT.pdf)

**Decision 2.** For fixed $d,N$, one can subtract cumulative prime counts at $Y$ and $2Y$. The logarithmic-integral difference is asymptotic to $Y/\log Y$, but the starting point of a fixed-field estimate can depend on $d,N$. Already at $k=1$ we need one $x_0$ for every admissible $d,N$ at $Y=\exp(8x^\varepsilon)$. A bound for the first represented prime also permits the dyadic interval to contain no represented prime. Balog and Ono cover the length for a fixed extension. [Balog and Ono, Theorem 2](https://uva.theopenscholar.com/files/ken-ono/files/062_8.pdf) · [Thorner and Zaman, least represented prime](https://msp.org/ant/2017/11-5/ant-v11-n5-p04-s.pdf)

Put $D=4dN^2$. The uniform Chebotarev comparison of Thorner and Zaman illustrates how this quantifier dependence can be addressed. For the identity class the possible exceptional zero $\beta$ reduces the size of the main term by a factor of order $\rho(Y)=1-Y^{\beta-1}$, with $\rho(Y)=1$ in the absence of such a zero. The relative error at both endpoints retains the same factor and tends uniformly to zero when $\log D\le c\sqrt{\log Y}$. Subtraction therefore preserves an interval main term of order $Y\rho(Y)/\log Y$ before the ray class degree is included. The exceptional-zero bound gives $\rho(Y)\gg D^{-2}$ in the conductor range, while the ray class degree is $O(D)$. This accounts for the loss $D^3$ in a specialization of their estimate. Removing degree-two ideals costs $O(\sqrt Y)$, absorbed by the dyadic lower bound in that range, and each rational prime is counted at most twice. [Thorner and Zaman, Lemma 2.4 and Theorems 3.3 and 5.1](https://msp.org/ant/2019/13-5/ant-v13-n5-p02-s.pdf) · [Stark](https://gdz.sub.uni-goettingen.de/download/pdf/PPN356556735_0023/PPN356556735_0023.pdf)

The proof uses the assumed estimate at $h=1$, for which $e^{-c\sqrt{\log Y}}\le h$ is automatic and $h\le1$ holds with equality. At $h=0$ its lower-bound expression would be zero for $Y>1$, but the lower restriction on $h$ is positive. The denominator $D^A\log Y$ must be paid for: omitting it would ask for $c'Y$ at $h=1$, a stronger lower bound when $D^A\log Y>1$. At $Y=1$ the logarithmic denominator vanishes, and since $D>1$ the conductor test also fails there.

Fix a triple $A,c,c'$ from $\mathsf S$. Put $t=x^{\varepsilon/5}$. Choose $x_0\ge1$ so that for every $x\ge x_0$ we have $t\ge10000$, $t\ge50A$, $t\ge13/c^2$, $40e^{-t/20}\le c'$, and $(\log x)^2\le t$. These bounds follow from growth of a positive power of $x$ and the logarithmic and exponential comparisons in the routine facts. No threshold for these conditions can be uniform down to $\varepsilon=0$, since at fixed $x\ge1$ the power $t$ tends to 1 as $\varepsilon\to0^+$. The threshold is independent of $d,N,Y$.

Heuristic: The natural conductor estimate has order at most $t(\log x)^2$, while the conductor allowance at the least permitted window is already of order $t^{5/2}$. There is room to bound the conductor logarithm by the simpler expression $10t^2$.

Indeed $d\mid N$ and $N>0$ give $N\ge d\ge100$. Consequently $D>1$ and $\log D=\log4+\log d+2\log N\le\log4+9t(\log x)^2\le10t^2$, using $t\ge10000$. Also $\log Y\ge8x^\varepsilon=8t^5$. Proposition 12 with $W=D$ gives the conductor test and the numerical lower bound $c'Y/(D^A\log Y)\ge Y^{9/10}$. Since $N\ge3$ and $Y>1$, the dyadic instance of $\mathsf S$ applies at $d,N,Y$ and supplies the desired count.

Absorbing the conductor loss — partial precedent. The published estimates allow a polynomial loss in the conductor. The proof budgets one tenth of the exponent for this loss and the logarithm together, leaving a margin of $3/20$ for deletion. [Thorner and Zaman, Theorems 3.3 and 5.1](https://msp.org/ant/2019/13-5/ant-v13-n5-p02-s.pdf)

**Remarks.** In $\log4+9t^2\le10t^2$ the coefficient 10 can be replaced by any $b_*>9$ once $t\ge\sqrt{\log4/(b_*-9)}$. The sufficient conductor cutoff then becomes $b_*^2/(8c^2)$. Using the sharper bound before this relaxation, the conductor test would follow from $\log Y\ge((\log4+9t(\log x)^2)/c)^2$, of order $t^2(\log x)^4$ for fixed $c,\varepsilon>0$. Thus $\log Y\ge C t^\sigma$ for fixed $C>0$ and any $\sigma>2$ eventually suffices for this test. The fifth power in Proposition 12 is a convenient margin.

## Proposition 14. An exponential bound for the cutoff in the selection

$$
\forall\varepsilon\in\mathbb R,\quad \varepsilon>0\ \Longrightarrow\
\exists x_0\in\mathbb R\
\forall x\in\mathbb R,\ x\ge x_0:\quad
x\ge1,\qquad 21x^{15}\le e^{x^\varepsilon}.
$$

**Proof.**

Heuristic: For fixed $\varepsilon>0$, $x^\varepsilon$ grows faster than $15\log x$, so the exponential eventually exceeds the stated polynomial. A single Taylor term of degree $\nu$ will already do so if $\varepsilon\nu>15$.

Take $\nu=\lceil16/\varepsilon\rceil$, which gives $\varepsilon\nu\ge16$. For $x\ge21\nu!$ one has $x\ge1$ and
$$
e^{x^\varepsilon}\ge \frac{(x^\varepsilon)^\nu}{\nu!}
\ge\frac{x^{16}}{\nu!}\ge21x^{15}.
$$
The Taylor degree must grow as $\varepsilon$ decreases, since it needs $\varepsilon\nu>15$. The factorial in the chosen threshold comes from using a single Taylor term. Dependence on $\varepsilon$ is necessary even for the inequality itself, because at each fixed $x\ge1$ the left-hand exponential tends to $e<21x^{15}$ as $\varepsilon\to0^+$. At $\varepsilon=0$ it stays equal to $e$ for $x>0$.

**Remarks.** A Taylor degree with $\varepsilon\nu>15$ suffices as soon as $x\ge\max\{1,(21\nu!)^{1/(\varepsilon\nu-15)}\}$, and there is no upper bound on the degree. If $\varepsilon\nu\le15$, one term cannot pay the factor 21 for any $x\ge1$. Choosing $\varepsilon\nu\ge16$ gives the simpler threshold $21\nu!$. Any coefficient greater than 20 could play the role of 21. At the chosen window exponent even 20 would suffice because $Y^{3/20}>ke^{x^\varepsilon}$ there.

## Theorem 15. The two norm primes

$$
\begin{gathered}
\mathsf S\quad\Longrightarrow\quad
\forall\varepsilon\in\mathbb R,\ \varepsilon>0\ \exists x_0\in\mathbb R\
\forall x\in\mathbb R,\ x\ge x_0\
\forall N,d,k,r\in\mathbb N:\\
d\text{ prime},\quad d\equiv3\pmod4,\quad d\ge100,\quad
N>0,\quad d\mid N,\quad
\log N\le3x^{\varepsilon/5}(\log x)^2,\quad
k\ge1,\quad 1\le r\le x^5\\
\Longrightarrow\quad
\exists a,b\text{ distinct primes in }[Y,2Y],\quad Y=(k e^{x^\varepsilon})^8,\\
a,b\text{ each have the prescribed norm representation at }d,N,\qquad
\mathcal B_r(a)\cap\mathcal B_r(b)=\varnothing.
\end{gathered}
$$

**Proof. Decision 8.** One might try to make the products of all the numbers $a^j-1$ and $b^j-1$, respectively, coprime. The generator congruence makes this impossible: Proposition 13's norm expansion gives $a\equiv b\equiv1\pmod N$. Since $r\ge1$, both products contain their exponent-one factor and their gcd is divisible by $N\ge d\ge100$. In particular, $d$ would be a shared label for every pair under that stronger requirement. The size test at exponent one requires $v_d(g-1)>\log g/(4\log d)$ for $d$ to be exceptional. The forced congruence gives $v_d(g-1)\ge v_d(N)$. For sufficiently large $x$, the component forced by $N$ lies below the threshold, since $d^{v_d(N)}\le N<g^{1/4}$ by the modulus and window bounds. The identity-ray-class description thus explains the forced residue, and the primary-component test is what lets us keep that residue. [Milne, *Class Field Theory*, Ch. V](https://www.jmilne.org/math/CourseNotes/CFT.pdf)

Primary-component threshold — partial precedent. Xie studies large primary components of cyclotomic values. Here the fourth-root cutoff gives three labels per exponent while allowing both bases to be 1 modulo the prescribed modulus. [Xie, Theorem 3.2](https://arxiv.org/pdf/2611.00075)

**Decision 4.** One might choose a first norm prime $a$ and incorporate every forbidden label into a modulus $M$ for the second prime. The label $a$ itself belongs to $\mathcal B_r(a)$, so such a product modulus has $M\ge a\ge Y$. This gives $\log(4dM^2)>2\log Y$, whereas the conductor test asks for $\log(4dM^2)\le c\sqrt{\log Y}$, impossible for $\log Y\ge c^2/4$ and $Y>1$. Moreover, adding a prime factor $\ell$ to that modulus forces the second prime to be 1 modulo $\ell$, though the issue is the size of the valuation of its power minus one. After omitting the base label, the remaining label set can be empty. Any additional congruences imposed for those labels would need a prime count that includes them. The uniform ray-class estimate concerns one class in its conductor range. We use the original modulus alone and bound all colliding integers, which requires no prime count in auxiliary progressions. [Thorner and Zaman, Theorem 5.1](https://msp.org/ant/2019/13-5/ant-v13-n5-p02-s.pdf)

Deletion at the original modulus — partial precedent. Hooley bounds remaining exclusions after a preliminary count that already imposes small-prime tests. Here the preliminary count uses only the prescribed norm modulus, and the exclusions depend on the chosen anchor. [Hooley](https://www.degruyterbrill.com/document/doi/10.1515/crll.1967.225.209/html) · [Moree, §5](https://guests.mpim-bonn.mpg.de/moree/surva.pdf)

Fix $\varepsilon>0$ and take $x_0$ to be the maximum of the thresholds in Propositions 13 and 14. The first gives the needed prime count when $\log Y\ge8x^\varepsilon$ and the second makes $20r^3\le20x^{15}<e^{x^\varepsilon}$ for every allowed $r$, uniformly in $k\ge1$. Any larger common threshold works. At the excluded $k=0$ the window would be $[0,0]$ and contain no prime. At $\varepsilon=0$ and $k=1$ the window would stay at $Y=e^8$ while the allowed $\log N$ grows as $3(\log x)^2$. Fixing $d=103$ and a multiple $N$ with $dN^2>8e^8$ would force $\eta=0$ for any norm representation in that window, since $d\eta^2\le4p\le8e^8$. Then the norm equation excludes prime $p$.

Heuristic: For fixed $\varepsilon>0$, already at $k=1$ the window grows exponentially in $x^\varepsilon$, whereas the collision coefficient is at most of order $x^{15}$. The count exponent leaves a power of the window to absorb that coefficient, and all larger $k$ help both comparisons.

Put $E=e^{x^\varepsilon}$. For a window start $Y=(kE)^\mu$, the count test $\log Y=\mu(\log k+x^\varepsilon)\ge8x^\varepsilon$ is guaranteed uniformly in $k\ge1$ by $\mu\ge8$, with equality at $\mu=8,k=1$. For $kE>1$, the comparison $kE\le Y^{3/20}$ requires $\mu\ge20/3$. The prescribed value 8 satisfies both tests. Take $Y=(kE)^8$. Since $E\ge21x^{15}$ and $x\ge1$, we have $Y\ge kE\ge21>2$. Also $Y^{3/20}=(kE)^{6/5}\ge kE$, so the exact comparison is
$$
20r^3\le20x^{15}<E\le kE\le Y^{3/20}.
$$
Proposition 13 gives $|\mathcal P_{d,N}(Y,2Y)|\ge Y^{9/10}$. Apply Proposition 11 to $G=\mathcal P_{d,N}(Y,2Y)$ to obtain the distinct primes $a,b$ with disjoint label sets. Both have the prescribed representations. Membership gives $Y<a,b\le2Y$, which implies the closed interval condition of the theorem.

**Remarks.** All $\mu\ge8$ work with the same comparisons, with no upper restriction from either test. A direct comparison of $Y^{3/20}$ with $20r^3$ on the collision side would eventually work for any fixed $\mu>0$. Any fixed polynomial restriction $r\le x^{\kappa}$ with $\kappa\ge0$ also suffices in the theorem's argument, upon comparing the exponential with $20x^{3\kappa}$.

## Routine and classical facts

- For a positive integer $n$, unique prime factorization gives $n=\prod_{\ell\mid n,\ \ell\text{ prime}}\ell^{v_\ell(n)}$. A product over any subset of those primes divides $n$.
- In a finite monoid every solution of $z^j=1$ with $j>0$ is a unit. In a finite cyclic group $\Gamma$, the number of solutions is $\gcd(j,|\Gamma|)\le j$.
- The units modulo an odd prime power are cyclic. Modulo $2^w$ for $w\ge2$ their number is $2^{w-1}$ and 5 has order $2^{w-2}$. Modulo 2 the unit group is trivial. [Gauss, *Disquisitiones Arithmeticae*, Arts. 89–90](https://en.wikisource.org/wiki/Translation:Disquisitiones_Arithmeticae/Third_Section#Article_89)
- The cardinality of a finite union is at most the sum of the cardinalities. The cardinality of a finite set equals the sum of the sizes of its nonempty fibers under any map.
- For $y>0$ one has $\log y\le y-1$. As $x\to\infty$, $\log x=o(x^\lambda)$ for each fixed real $\lambda>0$, and $x^\lambda\to\infty$.
- For $z\ge0$ and $\nu\in\mathbb N$, $e^z\ge z^\nu/\nu!$ by the Taylor series for the exponential. For $c'>0$, $40e^{-t/20}\le c'$ for $t\ge20\log(40/c')$.
- For the prime $d\equiv3\pmod4$, the integers of $K=\mathbb Q(\sqrt{-d})$ are $\mathbb Z[(1+\sqrt{-d})/2]$. A prime ideal in the identity ray class modulo $M\mathcal O_K$ has a generator congruent to 1 modulo that ideal modulus. [Milne, *Class Field Theory*, Ch. V](https://www.jmilne.org/math/CourseNotes/CFT.pdf)

## Concordance

| Displayed result | Lean declaration | Location in the supplied material |
|---|---|---|
| Counting hypothesis | `UpperTheory.T3.ShortNorm` | Slice 1-1 definition |
| Proposition 1 | `GlobalTheory.exceptional_primes_finite_card_le` | Slice 1-11 |
| Proposition 2 | `GlobalTheory.exceptional_set_count` | Slice 1-10 |
| Proposition 3 | `GlobalTheory.card_pow_eq_one_le_index_mul` | Slice 1-14 |
| Proposition 4 | `GlobalTheory.card_pow_eq_one_two_pow_le` | Slice 1-13 |
| Proposition 5 | `GlobalTheory.rootsOfUnityCount` | Absorbed declaration, outline step 1-12 |
| Proposition 6 | `GlobalTheory.card_class_in_dyadic_le` | Slice 1-9 |
| Proposition 7 | `GlobalTheory.card_exc_fixed_le` | Slice 1-8 |
| Proposition 8 | `GlobalTheory.card_mem_BB_fixed_le` | Slice 1-7 |
| Proposition 9 | `GlobalTheory.choiceCount_of` | Slice 1-6 |
| Proposition 10 | `GlobalTheory.choice_count` | Absorbed declaration, outline step 1-5 |
| Proposition 11 | `UpperTheory.T3.exists_pair_disjoint` | Slice 1-4 |
| Proposition 12 | `UpperTheory.T3.core_sqrt` | Slice 1-2 |
| Proposition 13 | `UpperTheory.T3.normPrimesN` | Slice 1-1 |
| Proposition 14 | `UpperTheory.T3.poly_le_exp` | Slice 1-3 |
| Theorem 15 (key result, displayed in the overview and above its proof) | `UpperTheory.T3.typePrimesN` | Slice 1 |
