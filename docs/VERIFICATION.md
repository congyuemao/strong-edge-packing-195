# Verification and reproduction

## Formal endpoint

The main declaration is `StrongEdge.induced_matching_packing195_with_connected_component_count`, in [TightComponents.lean](../lean/StrongEdge/TightComponents.lean). Its signature, with explicit instance parameters, is:

```lean
theorem StrongEdge.induced_matching_packing195_with_connected_component_count
    {V : Type*} [Fintype V] [DecidableEq V]
    (G : SimpleGraph V) [DecidableRel G.Adj]
    [DecidableRel (StrongEdge.conflictGraph G).Adj]
    (hΔ : ∀ x, G.degree x ≤ 4) (F : Finset G.edgeSet) :
    ∃ M : Finset G.edgeSet, M ⊆ F ∧
      StrongEdge.IsInducedMatching G (M : Set G.edgeSet) ∧
      2 * F.card ≤ 39 * M.card + (StrongEdge.tightComponentsIn G F).card
```

The correction counts actual connected components of the original graph whose support is a doubled five-cycle and whose entire edge set lies in `F`. Partially selected components are not counted. The graph hypothesis is maximum degree at most four; there are no remaining `h20`, `h21`, `h22`, `h23`, or `no20` assumptions. Finiteness and decidability instances supply the usual finite combinatorial environment.

[Basic.lean](../lean/StrongEdge/Basic.lean) defines conflicts through the line graph of the whole original graph. Restricting to the candidates retains unselected original edges as possible conflict witnesses. [Packing195Unconditional.lean](../lean/StrongEdge/Packing195Unconditional.lean) performs tight-component removal; [TightComponents.lean](../lean/StrongEdge/TightComponents.lean) identifies its correction with the actual connected-component count. The zero-correction corollary is `StrongEdge.induced_matching_packing195_of_no_full_tight_component`.

## Pinned environment

| Item | Required version |
| --- | --- |
| Lean | `leanprover/lean4:v4.35.0-rc4` |
| Lean compiler commit | `c29b6dda4f7c20e3eeaa717c4e565663c5cfa364` |
| mathlib | `49fd9dee36e7bbf345fe7981d2de6aeeb591f75b` |
| Lake | The version bundled with the pinned Lean toolchain (`5.0.0-src+c29b6dd`) |

[lean-toolchain](../lean/lean-toolchain), [lakefile.toml](../lean/lakefile.toml), and [lake-manifest.json](../lean/lake-manifest.json) pin the environment, including the nine dependency commits. Their bytes are unchanged. Do not substitute a newer Lean or mathlib, run a dependency upgrade, or regenerate the manifest.

## Rebuild from a clean checkout

Install `elan`/`lake` using the [Lean version manager](https://github.com/leanprover/elan), or place the exact toolchain on `PATH`. With elan, entering `lean/` selects the pinned toolchain. Initial setup requires access to the toolchain release, dependency repositories, and optionally mathlib's compiled dependency cache. From the repository root, run:

```sh
cd lean
lake env lean --version
lake exe cache get
lake build
lake env lean StrongEdge/Audit.lean
lake env lean StrongEdge/Audit195.lean
lake env lean StrongEdge/Audit195Continuation.lean
lake env lean StrongEdge/Audit195Thresholds.lean
lake env lean StrongEdge/Audit195Unconditional.lean
lake env lean StrongEdge/Tests.lean
lake env lean StrongEdge/Tests195.lean
lake env lean StrongEdge/Tests195Unconditional.lean
```

`lake exe cache get` fetches matching compiled dependencies to avoid rebuilding mathlib. It does not provide compiled StrongEdge project files. It may download substantially more than the imports needed by this project. For a smaller download, this PowerShell alternative obtains the imported external modules from the source files:

```powershell
$modules = Get-ChildItem StrongEdge -Recurse -Filter *.lean |
    Select-String '^(?:public )?import (Mathlib\.[A-Za-z0-9_.]+)' |
    ForEach-Object { $_.Matches[0].Groups[1].Value } |
    Sort-Object -Unique
.\lean.ps1 exe cache get @modules
```

On Windows, the unchanged launcher can run every required check from `lean/`:

```powershell
.\lean.ps1 build
.\lean.ps1 env lean StrongEdge/Audit.lean
.\lean.ps1 env lean StrongEdge/Audit195.lean
.\lean.ps1 env lean StrongEdge/Audit195Continuation.lean
.\lean.ps1 env lean StrongEdge/Audit195Thresholds.lean
.\lean.ps1 env lean StrongEdge/Audit195Unconditional.lean
.\lean.ps1 env lean StrongEdge/Tests.lean
.\lean.ps1 env lean StrongEdge/Tests195.lean
.\lean.ps1 env lean StrongEdge/Tests195Unconditional.lean
```

Check each exit code before continuing (`$LASTEXITCODE` in PowerShell). The launcher returns Lake's exit code. The final audit prints both the endpoint's full type and its axiom dependencies. Acceptable dependencies are only `propext`, `Classical.choice`, and `Quot.sound`; an empty set is also acceptable. A successful wrapper or log-processing script alone is not a Lean proof check.

## What the checks establish

The build elaborates and kernel-checks StrongEdge's formal proofs against the pinned dependencies. The five audit files expose declarations and their transitive axiom dependencies, including the final unconditional theorem. Regression modules check the unselected conflict witness on a four-vertex path, earlier 19.5 cases, the abstract twenty-clique obstruction, and the actual doubled five-cycle, including its degree, edge count, component certificate and necessary correction. Their finite computations use kernel-checked `decide`.

SHA-256 comparisons and Python scripts check file identity, manuscript/PDF correspondence, numbered references, page geometry, and log contents. Those checks are not mathematical proofs. Neither Lean nor these scripts automatically verifies the English exposition. No external human peer review is claimed.

## Archived verification evidence

The [completion record at the verified source commit](https://github.com/congyuemao/strong-edge-lean-verification/blob/1160b4529436efa82d579a2f7e4b97e57ae5d9f0/strong_edge_lean_starter/PACKING195_UNCONDITIONAL.md) records a full build of **1,197 jobs**, **376 axiom-audit entries** (225 + 22 + 31 + 34 + 64), and **75 Lean files plus four environment/launcher files**. Its saved logs and manifests remain in the [original verification directory](https://github.com/congyuemao/strong-edge-lean-verification/tree/1160b4529436efa82d579a2f7e4b97e57ae5d9f0/strong_edge_lean_starter/verification). These are historical results, not a substitute for the new release run below.

## Actual release verification

**Status: VERIFIED AND PUBLISHED.**

The verified release is publicly available at [congyuemao/strong-edge-packing-195](https://github.com/congyuemao/strong-edge-packing-195).

This run took place on **10 October 2026, Australia/Sydney (UTC+11)**, on **Windows 11 x86_64, build 26200**, using the exact Lean/Lake binaries listed above. The existing pinned compiler installation was used read-only via `PATH`. No compiler files were copied into the release.

The new `lean/` directory started without `.lake/`, project objects, or dependency caches. Nine dependency repositories were fetched afresh from upstream at the commits in the unchanged manifest, using shallow Git fetches. The selective cache command obtained **1,111 matching dependency artifacts** from mathlib's cache (exit 0); it did not reuse the old archive's `.lake/` or `.cache/`. There were no StrongEdge build objects before the full build. Every StrongEdge module in the default build was elaborated anew. This checks the release against compiled standard dependencies, not a source rebuild of the entire Lean compiler and mathlib.

Times below use the timezone above. Every command ran from this release's `lean/` directory through the unchanged PowerShell launcher.

| Command | Started | Finished | Exit code | Result |
| --- | --- | --- | --- | --- |
| `.\lean.ps1 build` | 22:48:14 | 22:53:13 | 0 | 1,197 build jobs; no warnings |
| `.\lean.ps1 env lean StrongEdge/Audit.lean` | 22:53:13 | 22:53:23 | 0 | 225 axiom entries; allowed axioms only |
| `.\lean.ps1 env lean StrongEdge/Audit195.lean` | 22:53:23 | 22:53:37 | 0 | 22 axiom entries; allowed axioms only |
| `.\lean.ps1 env lean StrongEdge/Audit195Continuation.lean` | 22:53:37 | 22:53:51 | 0 | 31 axiom entries; allowed axioms only |
| `.\lean.ps1 env lean StrongEdge/Audit195Thresholds.lean` | 22:53:51 | 22:54:05 | 0 | 34 axiom entries; allowed axioms only |
| `.\lean.ps1 env lean StrongEdge/Audit195Unconditional.lean` | 22:54:05 | 22:54:19 | 0 | 64 axiom entries; allowed axioms only |
| `.\lean.ps1 env lean StrongEdge/Tests.lean` | 22:54:19 | 22:54:30 | 0 | regression checks passed |
| `.\lean.ps1 env lean StrongEdge/Tests195.lean` | 22:54:30 | 22:54:42 | 0 | regression checks passed |
| `.\lean.ps1 env lean StrongEdge/Tests195Unconditional.lean` | 22:54:42 | 22:55:00 | 0 | regression checks passed |

The five newly executed audits produced **376 entries covering 376 distinct declarations**, with dependencies limited to `propext`, `Classical.choice`, and `Quot.sound`. Each expected `#print axioms` declaration was matched against its new output. The final theorem's printed type was separately inspected and has only the degree bound and the usual finite/decidable instances shown above. No mathematical Lean source or lockfile was edited.

The PDF was regenerated and all **19 pages** rendered with Poppler and visually inspected. The title page names only **Congyue Mao**, the PDF Author metadata agrees, and the complete end-of-manuscript AI disclosure remains visible. All **37 numbered statements** and **28 numbered equations** have consistent references. Page numbers and safe-area checks pass on every page; extracted text on each page matches the source PDF except for the removed title-page credit line. The source-byte comparison confirms every mathematical formula and proof paragraph is unchanged. These are integrity and layout checks, not a new mathematical review of the English proof.

Release links, module imports, file hashes, and the file inventory were checked locally. All 79 copied formal-source/environment hashes match the fixed Git objects and the archived inventory. All tracked contents, HEADs, branches, refs, index bytes, and Git configuration in both original checkouts match their pre-work snapshots (328 research-archive files and 986 formalization-archive files). The release was subsequently published to GitHub with the author's authorization.

Raw logs, rendered review images, the exact temporary scripts, and a short build report are retained outside the release repository in the adjacent local `strong-edge-packing-195-work/` directory. No old verification log was substituted for a new run. The only intermediate failures were UTF-8 decoding errors in temporary Python packaging checks under Windows' default code page, before Lean verification began; rerunning those helpers with explicit UTF-8 succeeded. No Lean build, audit, or regression command failed.

## Source consistency and editorial changes

The formal source commit is `1160b4529436efa82d579a2f7e4b97e57ae5d9f0`. The selected manuscript commit is `860b5e44588d1bbc1eceed8748c67b29693a9d99`, following the complete-manuscript commit `13183f9aec2fd3a35971329f3bc01b72de5db3a8`. Git-object comparisons confirm that all 75 Lean sources and four environment/launcher files are byte-identical at all three commits and in this package. They also match the archived 79-entry SHA-256 inventory. **Mathematical source differences: none.** The historical inline source comments are preserved with the proof files; the release's current scope is stated in its new documentation.

Original source line endings are preserved. Git's whitespace lint also reports terminal blank lines already present in `StrongEdge/Bounds/High20.lean` and `StrongEdge/Bounds/High22Support.lean`; these were deliberately retained to preserve the verified bytes. They are formatting observations, not Lean build warnings.

The source archive's PDF and Markdown match its saved build hashes. The only edit to the release Markdown is deletion of `@credit Proof completed using GPT-6 Astra` from the title-page metadata. The full AI disclosure at the end is unchanged. The PDF was rebuilt from that source in a separate temporary directory using the archived `build_packing195.py` and `build_manuscript.py`, with existing local typesetting dependencies and installed fonts. Generators, font files, temporary images and build dependencies are not release files.

[SOURCE_MANIFEST.json](SOURCE_MANIFEST.json) contains actual per-file SHA-256 values and source mappings for all release files except itself. Generated documentation is identified separately from copied sources. The manifest cannot hash its own bytes; its Git commit provides the enclosing identity. `.gitattributes` disables newline conversion so clean checkouts preserve these byte hashes on Windows as well as Unix.

To check the manifest from the repository root with Python 3:

```python
from pathlib import Path
import hashlib, json
root = Path.cwd()
manifest = json.loads((root / "docs/SOURCE_MANIFEST.json").read_text(encoding="utf-8"))
for item in manifest["files"]:
    path = root / item["release_path"]
    assert hashlib.sha256(path.read_bytes()).hexdigest() == item["release_sha256"], path
print("All listed release hashes match.")
```

## Limits

This is a corrected induced-matching packing theorem for arbitrary candidate edge sets. It does not prove the integer strong edge twenty-colour conjecture, optimality of 19.5, a general weighted or fractional colouring analogue, or a polynomial-time matching algorithm. It does not independently validate every exploratory note in either historical archive. The PDF's source uses custom typesetting directives; the PDF is the formatted reading version. No licence is added pending the author's decision.
