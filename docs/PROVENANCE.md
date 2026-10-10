# Research provenance and AI use

**Author / Project curator: Congyue Mao.** No institutional affiliation is asserted.

Congyue Mao initiated, directed, organized, and curated this project and manages its release. Mathematical exploration, proof development, Lean formalization, and preparation of the English manuscript were conducted predominantly using generative AI systems. The existing manuscript specifically discloses **GPT-6 Astra** under the author's direction. This name is preserved as the author's recorded disclosure, not as an independently established runtime model identity. No other model, undocumented prompt history, or unverified human proof contribution is attributed here.

AI systems are not coauthors and cannot undertake human academic review or responsibility. The project's AI-assisted checking and editorial review must be distinguished from Lean kernel checking of formal proof terms. Neither is evidence of external human peer review. This release makes no claim of journal acceptance, endorsement, awards, or independently established priority.

## Mathematical context

The manuscript develops original-graph conflict-clique bounds, classifies twenty-edge conflict cliques as complete doubled-five-cycle components, and uses private-neighbourhood exchange and independent-set counting to obtain the prescribed-edge-set inequality. The local-exchange literature, including Fürst, Leichter and Rautenbach's *Locally Searching for Large Induced Matchings* ([2018](https://doi.org/10.1016/j.tcs.2018.02.006)), provides methodological context; it is not an additional lemma assumed by the formal proof.

[Joos and Nguyen (2016)](https://doi.org/10.1137/140986980) prove whole-graph induced-matching bounds for graphs of maximum degree four, including the eighteen-fold edge bound when doubled-five-cycle components are excluded. That precedent and its exceptional graph are relevant context. Applying a whole-edge-set result after deleting unselected edges would not preserve the original-graph conflict semantics required here. This release does not claim an exhaustive literature search or that 19.5 is optimal. The manuscript also distinguishes Hall ratio from fractional chromatic number.

## Source archives and fixed versions

The [formalization archive](https://github.com/congyuemao/strong-edge-lean-verification) remains the complete historical record. Three fixed commits identify the relevant stages:

| Commit | Role |
| --- | --- |
| `1160b4529436efa82d579a2f7e4b97e57ae5d9f0` | Completed formal proof and archived build/audit evidence; source for all Lean files and environment files. |
| `13183f9aec2fd3a35971329f3bc01b72de5db3a8` | Complete English proof manuscript before the authorship revision. |
| `860b5e44588d1bbc1eceed8748c67b29693a9d99` | Selected manuscript source, including Congyue Mao's authorship and the AI disclosure; latest inspected archive HEAD. |

All 79 Lean source/configuration/launcher files are byte-identical across these stages and in this release. `strong_edge_lean_starter/` maps to `lean/`; the archived `output/pdf/packing195_unconditional_manuscript.{md,pdf}` maps to `manuscript/packing195.{md,pdf}`. The sole Markdown edit removes the separate title-page `@credit` line. The full end-of-manuscript AI disclosure and every other source byte remain intact. The PDF was regenerated from that edited source using temporary copies of the archived renderer.

The [original research archive](https://github.com/congyuemao/strong-edge-colouring-research), inspected at `a2cac8df6aac108ea1c286f67bd1a144972a6d2a`, retains the original exploration, bilingual notes, computations, abandoned approaches, and sealed file manifests. None of those historical research files is copied here.

This separate repository presents the finished manuscript and a self-contained Lean source package. The two archives were left unchanged. [SOURCE_MANIFEST.json](SOURCE_MANIFEST.json) records per-file source commits, paths, SHA-256 hashes, and transformations; [VERIFICATION.md](VERIFICATION.md) records the checks and their limits. No repository-wide licence has been selected; licensing remains the author's separate decision.
