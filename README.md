<!-- solve-problem:cf30dc94-e430-45ac-a7f3-0caa85ba1dcb -->
# Superlinear explicit XOR-circuit lower bounds

A [Tangle Solve problem](https://solve.tangle.tools/problems/cf30dc94-e430-45ac-a7f3-0caa85ba1dcb).

## What is the problem?

Let M be an n×n matrix over GF(2). A **linear circuit** (XOR-circuit) computes the linear map x ↦ Mx using two-input XOR gates: starting from input variables x₁,…,x_n, each gate computes the XOR of two previously computed values, and the outputs must be exactly the n rows of M (as GF(2) combinations of inputs). The cost is the number of gates, i.e., the number of pairwise additions needed to compute a basis of the row space of M.

Counting shows almost all n×n matrices require gates proportional to n²/log n, but no *explicit* matrix (one computable/definable in polynomial time, or from a standard explicit family) is known to require more than (3 + o(1))n gates — in fact the best unconditional explicit lower bounds for unrestricted linear circuits are barely superlinear or just linear (verify exact constants; known results give ~3n for general linear circuits and 3n log n only under depth/gram restrictions). The problem: **exhibit an explicit family {Mₙ} of GF(2) matrices and prove that any XOR circuit computing Mₙx uses ω(n) gates.** Even (3+ε)n for any fixed ε>0, or 4n, would be major progress; ω(n) is the stated target.

Ambiguity note: "explicit" is not formalized in the census; the standard convention is polynomial-time computability of M (or membership in a complexity class like P/poly-family with succinct description).

## Why does it matter?

Linear circuits measure the true cost of matrix-vector multiplication over GF(2), which underlies error-correcting encoders, cryptographic diffusion layers (AES MDS matrices, hash functions), and MPC/FHE linear layers. Superlinear lower bounds for unrestricted linear circuits are a necessary stepping stone toward superlinear bounds for general Boolean circuits (any Boolean circuit contains linear "skeletons" per Valiant), and connect directly to matrix rigidity, which would yield depth-2 and communication-complexity lower bounds. Progress here breaks a ~45-year-old barrier in low-level complexity.

## What's already known?

- **Counting/shannon bound:** almost every matrix needs Ω(n²/log n) gates (size of circuit space vs. number of matrices).
- **Valiant (1977):** introduced the rigidity connection — if M requires ω(n log log n) gates even after allowing depth ~log n, then M is Valiant-rigid, giving TC⁰ and communication lower bounds. The linear-circuit question is the depth-unrestricted special case.
- **Restricted models:** cancellation-free circuits (no gate's sum cancels to a shorter vector) have tight bounds: Ruppel (3n − 3 for cancellation-free general linear circuits), Jukna & Schnitger, and the "gram density" / dependence programs of Chazelle. These fail because general circuits can exploit cancellations.
- **Unrestricted bounds:** the best known explicit lower bound is 3n − o(n) (Lupanov-type upper bounds of ~(2.5)n match half the gap); recently Boyar, Find, Peralta and others refined four-rows-at-a-time arguments. Every known technique (gate-elimination, entropy/linear algebra arguments) saturates at a constant factor of n.
- **Rigidity route:** strong rigidity (Lokam) is false for random matrices w.h.p. (implying rigidity alone can't reach n²/log n via random examples), but explicit rigid matrices also remain open — the two problems are entangled.

## What would count as solving it?

Any of the following constitutes progress/solution:
1. **Target:** an explicit poly-time family Mₙ and a proof that every unrestricted linear circuit for Mₙ uses ω(n) gates (even n·log* n or n + n/log log n would count as superlinear; the census target is ω(n)).
2. **Milestone:** an explicit family with lower bound (3+ε)n or cn for any c > 3 (verify the current record constant before claiming novelty).
3. **Conditional:** a proof that some natural explicit matrix (e.g., rigidity-based candidates) requires superlinear gates if and only if / under some plausible hypothesis.
4. **Negative/structural:** a proof that linear circuits can simulate any n×n matrix in 3n + o(n) gates (matching Lupanov-style upper bounds), which would close the problem in the negative direction for constant-factor goals.

A referee requires: full definition of the explicit family, a complete gate-counting argument valid for circuits with arbitrary cancellations and arbitrary fan-out.

## How to start

1. **Read Valiant (1977)** first — understand exactly why rigidity implies linear-circuit lower bounds and where the depth restriction enters; the unrestricted model is strictly harder.
2. **Read the cancellation-free literature (Ruppel; Jukna–Schnitger; Chazelle's dependence programs)** to internalize why those proofs break under cancellation, and look for an invariant that survives cancellation (e.g., a potential function on the span of computed vectors).
3. **Study the 3n lower-bound technique** (Boyar–Find–Peralta-style four-row arguments, "verify") and attempt to push the constant: the obstacle is that after eliminating a few gates, the adversary can restructure the circuit with cancellations.
4. **Candidate matrices:** Vandermonde, DFT over GF(2ᵏ), Cauchy/MDS matrices used in crypto, and error-correcting generator matrices — test heuristically which resist known 2.5n–3n constructions (Lupanov/Thompson style).

## Key references

- L. Valiant, *Graph-Theoretic Arguments in Low-Level Complexity*, MFCS 1977 (LNCS 53). Introduces matrix rigidity and proves that rigid matrices need superlinear-size, log-depth linear circuits. https://link.springer.com/chapter/10.1007/3-540-08353-7_59
- Ramya C., survey on matrix rigidity (per census; "verify" exact title/venue). Surveys rigidity-based approaches and their limits, with the associated bibliography for linear-circuit lower bounds.
- J. Ruppel, cancellation-free linear circuit lower bounds (3n−3) — "verify" citation (his Master's thesis, U. Lübeck). Tight bounds once cancellations are forbidden.
- S. Jukna & G. Schnitger, *On the optimality of linear size circuits*, STACS 1991. Proves Ω(n log n) for a restricted gram/dependence model, showing where restrictions bite.
- Boyar, Find, Peralta, *Four measures of nonlinearity* and related papers — "verify" — current best explicit unconditional linear-circuit lower bounds near 3n and small-circuit heuristics.
- Lokam, *Spectral methods for matrix rigidity*, etc. — "verify" — the rigidity machinery a solver may need.

## Warnings

- **Cancellation is the whole difficulty:** any argument that implicitly assumes each gate adds rank/weight information fails; unrestricted circuits exploit cancellation, which is why cancellation-free results (3n−3, Ω(n log n) in gram models) do not transfer.
- **Random matrices won't work explicitly:** they give the counting bound but are not explicit; also known rigidity upper bounds show random matrices are not maximally rigid (Alman–Williams, "verify").
- **Don't conflate depth:** Valiant's rigidity→lower bound requires depth O(log n); an ω(n) bound for unrestricted depth does not follow from any known rigidity result.
- **Check the current record constant** (3n vs. anything newer) before claiming a first superconstant-factor improvement; the field moves slowly but the census record may be stale.
- "Explicit" is ambiguous — state your definition (P-computability is standard) and match it against prior work.

---
*`ALGO-000039` · unverified*

## Acceptance guidance

Any of the following constitutes progress/solution:
1. **Target:** an explicit poly-time family Mₙ and a proof that every unrestricted linear circuit for Mₙ uses ω(n) gates (even n·log* n or n + n/log log n would count as superlinear; the census target is ω(n)).
2. **Milestone:** an explicit family with lower bound (3+ε)n or cn for any c > 3 (verify the current record constant before claiming novelty).
3. **Conditional:** a proof that some natural explicit matrix (e.g., rigidity-based candidates) requires superlinear gates if and only if / under some plausible hypothesis.
4. **Negative/structural:** a proof that linear circuits can simulate any n×n matrix in 3n + o(n) gates (matching Lupanov-style upper bounds), which would close the problem in the negative direction for constant-factor goals.

A referee requires: full definition of the explicit family, a complete gate-counting argument valid for circuits with arbitrary cancellations and arbitrary fan-out.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/cf30dc94-e430-45ac-a7f3-0caa85ba1dcb?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000039.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000039)
