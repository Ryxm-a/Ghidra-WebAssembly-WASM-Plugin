# Release process

## Before release

1. Confirm the target Ghidra version.
2. Build the extension from the authoritative source tree/archive.
3. Smoke-test installation in a clean Ghidra environment.
4. Import representative memory32 and memory64 modules.
5. Exercise atomics/SIMD samples where applicable.
6. Review `CHANGELOG.md`.
7. Verify `extension.properties`.
8. Ensure the release ZIP name clearly includes the target Ghidra version.

## Release notes

Release notes should state:

- target Ghidra version;
- user-visible fixes/features;
- known compatibility limitations;
- whether processor/language definitions changed;
- whether re-analysis/re-import is recommended.

Avoid claiming complete support for a WebAssembly proposal unless the relevant execution/analysis paths have regression coverage.
