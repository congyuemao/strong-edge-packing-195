# Lean formalization of corrected 19.5 packing

The main declaration is `StrongEdge.induced_matching_packing195_with_connected_component_count` in [StrongEdge/TightComponents.lean](StrongEdge/TightComponents.lean). It states that every candidate edge set in a finite simple graph of maximum degree four contains an original-graph induced matching satisfying the corrected 19.5 inequality.

The 75 Lean files, including [StrongEdge.lean](StrongEdge.lean), all dependency modules, five axiom audits and three regression modules, are copied byte for byte from the verified source snapshot. No mathematical sources were edited or removed.

Use Lean `leanprover/lean4:v4.35.0-rc4` and mathlib commit `49fd9dee36e7bbf345fe7981d2de6aeeb591f75b`. [lean-toolchain](lean-toolchain), [lakefile.toml](lakefile.toml), and [lake-manifest.json](lake-manifest.json) retain their original bytes. Do not run a dependency upgrade or replace the manifest.

With `elan`/`lake` installed, run here:

```sh
lake exe cache get
lake build
lake env lean StrongEdge/Audit195Unconditional.lean
```

On Windows, the unchanged [lean.ps1](lean.ps1) forwards arguments to Lake:

```powershell
.\lean.ps1 build
.\lean.ps1 env lean StrongEdge/Audit195Unconditional.lean
```

The launcher uses `lake` from `PATH`, optionally preferring a matching installation in `../.tools/lean-4.35.0-rc4-windows/bin`. No compiler, dependency checkout, cache, or precompiled project object is part of this release. The optional local `.tools` location is not required when `elan` or the correct toolchain is on `PATH`.

See [VERIFICATION.md](../docs/VERIFICATION.md) for the complete audit and regression commands, actual results, and verification limits. The [manuscript PDF](../manuscript/packing195.pdf) is the mathematical reading entry point.
