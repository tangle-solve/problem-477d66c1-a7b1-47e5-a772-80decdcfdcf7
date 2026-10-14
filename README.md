<!-- solve-problem:477d66c1-a7b1-47e5-a772-80decdcfdcf7 -->
# Deterministic linear-time comparison MST

A [Tangle Solve problem](https://solve.tangle.tools/problems/477d66c1-a7b1-47e5-a772-80decdcfdcf7).

## What is the problem?

Given an undirected graph \(G=(V,E)\) with \(n\) vertices, \(m\) edges, and distinct edge weights (or weights from a totally ordered universe), construct a minimum spanning tree (MST) in the **comparison model**: the only allowed operation on weights is pairwise comparison. The goal is a **deterministic** algorithm running in \(O(m+n)\) worst-case time. The comparison-additive model is standard here; the question is whether randomness is necessary to remove superlinear terms. Randomization is allowed in the known linear-time algorithms (Karger–Klein–Tarjan); the open problem is a deterministic algorithm with the same asymptotic cost, or a proof that deterministic comparison-based MST inherently requires \(\omega(m)\) time (widely believed unlikely). Note: outside the comparison model, deterministic linear time is known for word-RAM via integer sorting tricks — the problem is specifically about the comparison setting.

## Why does it matters?

It would settle the exact comparison complexity of one of the most fundamental combinatorial optimization problems, completing a line of work going back to Borůvka, Kruskal, and Prim. The Pettie–Ramachandran algorithm is provably decision-tree optimal but its running time is unknown — linearity of the deterministic MST decision-tree complexity is the missing piece. Resolution would also likely yield new techniques for derandomizing graph algorithms broadly (e.g., filtering/sampling steps in MST underlie connectivity, min-cut, and approximation algorithms).

## What's already known?

- Karger, Klein, Tarjan (1995): randomized \(O(m+n)\) expected time, comparison-based, via random sampling plus Borůvka passes.
- Chazelle (2000): deterministic \(O(m\,\alpha(m,n))\) — inverse-Ackermann overhead — via a soft heap with controlled corruption.
- Pettie–Ramachandran (2002): a deterministic algorithm whose running time equals the (unknown) MST decision-tree complexity \(\mathrm{MST}(m,n)\), which lies between \(\Omega(m)\) and \(O(m\,\alpha(m,n))\). Their "optimal" algorithm is not directly implementable without a decision-tree of the right size; it is an existence/derivation result.
- Pettie (2006?) and others refined lower-bound and structural results (verify exact attributions). Partial approaches: derandomizing KKT's sampling (needs pessimistic estimators for "F-heavy edge" counts), soft-heap tuning, and direct decision-tree construction. None has removed the \(\alpha\) factor deterministically.

## What would count as solving it?

- **Upper bound (main goal):** A deterministic comparison-model algorithm and proof of \(O(m+n)\) worst-case running time.
- **Lower bound:** A proof that deterministic comparison MST requires \(\omega(m)\) comparisons (would refute the conjecture; surprisingly plausible analyses of \(\mathrm{MST}(m,n)\) showing superlinearity also count as major progress).
- **Partial credit:** Any deterministic \(o(m\,\alpha(m,n))\) bound, or a proof that \(\mathrm{MST}(m,n)=\Theta(m)\), which would immediately make Pettie–Ramachandran linear.

## How to start

1. Read Pettie–Ramachandran (JACM 2002) closely — Sections on the reduction to decision-tree construction and the analysis of \(\mathrm{MST}(m,n)\). The cleanest attack may be proving \(\mathrm{MST}(m,n)=O(m)\) rather than building a new algorithm.
2. Read KKT (1995) and attempt a derandomization via conditional expectations/pessimistic estimators on the key lemma: after sampling with probability \(p\), the number of \(p\)-light edges is \(O(n/p)\) in expectation. The obstacle: no known deterministic estimator matches this concentration.
3. Study Chazelle's soft heap; ask whether corruption parameters can be made deterministic-constant per edge, or whether a deterministic "sampling substitute" from soft heaps can replace KKT's random sampling.
4. Look at later work on MST decision trees and "verification" (e.g., Komlós's \(O(m+n)\) verification *comparisons* — verification is linear; construction is the gap).

## Key references

- B. Chazelle, "A Minimum Spanning Tree Algorithm with Inverse-Ackermann Type Complexity," *J. ACM* 47(6), 2000. Deterministic MST in \(O(m\,\alpha(m,n))\) using soft heaps. (verify link: ACM DL)
- S. Pettie and V. Ramachandran, "An Optimal Minimum Spanning Tree Algorithm," *J. ACM* 49(1), 2002. Constructs an MST algorithm matching the unknown decision-tree complexity \(\mathrm{MST}(m,n)\), showing it lies between \(\Omega(m)\) and \(O(m\,\alpha(m,n))\).
- D. R. Karger, P. N. Klein, R. E. Tarjan, "A Randomized Linear-Time Algorithm to Find Minimum Spanning Trees," *J. ACM* 42(2), 1995. Random sampling + Borůvka gives expected linear time — the algorithm to derandomize.
- J. Komlós, "Linear Verification for Spanning Trees," *Combinatorica* 5, 1985. MST verification needs only \(O(m+n)\) comparisons (nonconstructive in time). (verify)

## Warnings

- The Pettie–Ramachandran "optimal algorithm" is often misread as settling the problem; it does not — its running time is the unknown \(\mathrm{MST}(m,n)\).
- Don't conflate models: deterministic linear time is known with integer weights on word-RAM; the open problem is strictly comparison-based.
- The standard assumption of distinct edge weights (via tie-breaking) is benign; preserve it.
- Naïve derandomization of KKT fails: the sampling lemma's bound is on expectation, and edge-dependence makes pairwise-independent samplers appear to lose a logarithmic factor — this is the central technical obstacle.

---
*`ALGO-000127` · unverified*

## Acceptance guidance

- **Upper bound (main goal):** A deterministic comparison-model algorithm and proof of \(O(m+n)\) worst-case running time.
- **Lower bound:** A proof that deterministic comparison MST requires \(\omega(m)\) comparisons (would refute the conjecture; surprisingly plausible analyses of \(\mathrm{MST}(m,n)\) showing superlinearity also count as major progress).
- **Partial credit:** Any deterministic \(o(m\,\alpha(m,n))\) bound, or a proof that \(\mathrm{MST}(m,n)=\Theta(m)\), which would immediately make Pettie–Ramachandran linear.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/477d66c1-a7b1-47e5-a772-80decdcfdcf7?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000127.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000127)
