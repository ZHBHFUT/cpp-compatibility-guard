# cpp-compatibility-guard

Codex skill for preventing unintended C++ compatibility breaks.

It reviews changes across six dimensions:

- source compatibility;
- ABI compatibility;
- persisted-data compatibility;
- build and dependency compatibility;
- runtime behavior compatibility;
- numerical compatibility.

Compatibility targets come from each project's guidance, build files, policies, and tests. Missing targets are reported instead of guessed.

## Install

Install this repository as a Codex plugin, or copy `skills/cpp-compatibility-guard` into your Codex skills directory.

## Example

```text
Use cpp-compatibility-guard to check whether this refactor breaks existing callers, plugins, or project files.
```

See [`skills/cpp-compatibility-guard/SKILL.md`](skills/cpp-compatibility-guard/SKILL.md) for the complete workflow.
