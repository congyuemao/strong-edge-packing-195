# A Corrected 19.5 Bound for Induced Matchings in Prescribed Edge Sets

Congyue Mao

## Main Result

Let $G$ be a finite undirected simple graph with $\Delta(G)\leq 4$. For every prescribed edge set $F\subseteq E(G)$, there exists an induced matching $M\subseteq F$ in $G$ such that

$$
2|F|\leq 39|M|+t_G(F).
$$

Here $t_G(F)$ counts the connected components of the **original graph** $G$ that are isomorphic to $C_5[2]$ and whose **entire twenty-edge sets** lie in $F$. The graph $C_5[2]$ replaces each vertex of a five-cycle by an independent pair and each cycle edge by all four edges between the corresponding pairs. A partially selected component contributes zero. In particular, $t_G(F)=0$ gives $|F|\leq 19.5|M|$.

All strong conflicts are evaluated in the full original graph: edges outside $F$ can still witness a conflict between two candidate edges. On $G=C_5[2]$ with $F=E(G)$, a largest induced matching has one edge, and the corrected inequality reads $40=39+1$.

## Manuscript

Read the [complete English proof (PDF)](manuscript/packing195.pdf). Its [editable source](manuscript/packing195.md) retains the original typesetting directives; the PDF is the formatted reading version. The manuscript gives the structural bounds, component classification, private-neighbourhood argument, and a correspondence with the formal development.

## Lean Formalization

The principal declaration is

`StrongEdge.induced_matching_packing195_with_connected_component_count`

in [lean/StrongEdge/TightComponents.lean](lean/StrongEdge/TightComponents.lean). The [Lean project](lean/README.md) preserves all 75 archived Lean source files and the pinned environment. It assumes maximum original degree four and the usual finite-type and decidability instances, with no additional structural hypotheses.

A fresh release build, five axiom audits (376 entries), and three regression runs passed on 10 October 2026; only `propext`, `Classical.choice`, and `Quot.sound` occur in the audited dependencies. [VERIFICATION.md](docs/VERIFICATION.md) records the commands and results. Lean checks the formal statements and proof terms; it does not automatically verify every sentence or formula in the English manuscript.

## Reproduce

With `elan` and `lake` available, run from the repository root:

```sh
cd lean
lake exe cache get
lake build
lake env lean StrongEdge/Audit195Unconditional.lean
```

The toolchain and dependencies are pinned. [Full reproduction instructions](docs/VERIFICATION.md) include all five axiom audits and three regression files, Windows commands, and the distinction between archived evidence and this release's checks.

## Research Provenance and AI Use

Mathematical exploration, proof development, Lean formalization, and manuscript preparation were conducted predominantly using generative AI; the manuscript discloses GPT-6 Astra under Congyue Mao's direction. [PROVENANCE.md](docs/PROVENANCE.md) explains the author's role, source commits, and the preserved [formalization archive](https://github.com/congyuemao/strong-edge-lean-verification) and [research archive](https://github.com/congyuemao/strong-edge-colouring-research). AI review and kernel verification are distinct from external human peer review.

## Scope / Related Work

The twenty-edge conflict-clique rigidity theorem identifies complete $C_5[2]$ components and explains the correction term. [Joos and Nguyen](https://doi.org/10.1137/140986980) established an eighteen-fold whole-edge-set bound when these exceptional components are absent; that statement does not directly address arbitrary prescribed edge sets with original-graph conflicts. This release concerns the latter problem.

The result is an induced-matching packing, or conflict-graph independence, bound. It is not a proof of the integer strong edge-colouring bound $\chi'_s(G)\leq20$, nor of a weighted or fractional colouring analogue. No optimality claim for 19.5, exhaustive literature priority claim, or external human peer-review claim is made.
