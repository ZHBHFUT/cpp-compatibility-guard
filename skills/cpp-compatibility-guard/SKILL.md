---
name: cpp-compatibility-guard
description: Use when C++ changes may break existing callers, binaries, plugins, persisted data, build environments, runtime behavior, or numerical results, especially after editing public headers, exported interfaces, layouts, virtual functions, enums, serialization, CMake, dependencies, or algorithms.
---

# C++ Compatibility Guard

Derive the project's real compatibility contract, inspect the active change, and distinguish proven compatibility from unverified assumptions.

## Establish the Contract

1. Read every applicable `AGENTS.md`, then the top-level `CMakeLists.txt`, `CMakePresets.json`, `vcpkg.json`, test documentation, and compatibility or versioning policies. Record missing files.
2. Extract the supported language standards, compiler versions, platforms, toolchains, public interfaces, ABI policy, persisted formats, behavior guarantees, regression baselines, and tolerances.
3. If a compatibility target needed for the requested review is not declared, ask the user. Do not invent a minimum compiler, ABI promise, file-format guarantee, or numerical tolerance.

## Review the Change

1. Inspect the current Git diff and its callers. Identify touched public headers, exported symbols, layouts, virtual functions, enums, serialization paths, CMake usage requirements, dependencies, observable behavior, and numerical algorithms.
2. Classify each finding:
   - **Source:** old callers can still compile within the declared language and compiler limits.
   - **ABI:** old binaries can still link or load; check symbols, calling conventions, object layout, vtables, alignment, packing, runtime libraries, and types crossing shared-library boundaries.
   - **Data:** old JSON, binary, HDF5, or other persisted data remains readable; check field names, enum values, defaults, versions, and migration paths.
   - **Build:** declared CMake, generators, presets, toolchains, SDKs, triplets, and dependency versions remain supported; check `PUBLIC`, `PRIVATE`, and `INTERFACE` propagation.
   - **Behavior:** externally observable results remain within the declared contract.
   - **Numerical:** regression values, conservation metrics, convergence histories, or engineering quantities remain within declared tolerances.
3. Do not equate source compatibility with ABI compatibility, or one successful build with matrix-wide compatibility.

## Report Before Editing

State the compatibility break or risk, evidence, affected consumers, severity, verification status, files expected to change, and the smallest repair. Diagnose without editing unless the user asked for a fix.

## Repair and Verify

1. Apply only an approved root-cause repair. Prefer preserving an old overload, adding compatible readers or defaults, versioning an intentional ABI break, or using an existing compatibility adapter.
2. Keep compatibility workarounds localized. Do not degrade the whole modern code path to satisfy one legacy target.
3. Use existing presets, toolchains, fixtures, API tests, ABI checks, old data, behavior tests, and numerical baselines. Do not invent a parallel build system.
4. Mark every unavailable compiler, platform, binary consumer, fixture, or baseline as **UNVERIFIED**. Never report it as passing.

## Guardrails

- Never hide incompatibility by deleting public functionality, weakening warnings, skipping tests, ignoring failures, silently rewriting old data, or lowering the mainline standard.
- Never overwrite unrelated user changes or destructively clean build artifacts without permission.
- Do not add dependencies or install missing tools without explaining the exact need and obtaining permission.

## Final Report

```text
Compatibility verdict: PASS | CONDITIONAL | FAIL
Risk level: LOW | MEDIUM | HIGH | CRITICAL
Contract used:
Findings:
Verification matrix:
- source:
- ABI:
- data:
- build:
- behavior:
- numerical:
Commands executed:
Files changed:
Unverified items:
```
