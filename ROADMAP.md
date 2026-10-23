# Roadmap

The project is maintained around correctness and practical reverse-engineering value rather than feature-count claims.

## Current priorities

- Reproducible source-first builds for current Ghidra releases
- Regression coverage for memory64 and threads/atomics
- Large-module analysis performance
- Better validation of multi-value / multiple-return behavior
- Modern WebAssembly proposal coverage driven by real samples
- Better indirect-call and table analysis
- Improved decompiler readability
- Compatibility testing across supported Ghidra releases

## Quality bar

A feature should not be advertised as supported merely because its opcode parses. Where practical, support should be exercised through loading, disassembly, P-code and decompilation with a regression sample.

## Longer-term

Potential areas include richer proposal coverage, automated compatibility builds, benchmark corpora, improved symbol/type recovery and agent-accessible analysis workflows.

Roadmap items are directions, not promises or release dates.
