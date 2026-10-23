# Contributing

Thanks for helping improve Ghidra WebAssembly.

## What helps most

High-value contributions include minimal `.wasm` reproducers for incorrect analysis, Ghidra compatibility fixes, modern WebAssembly proposal support, SLEIGH/P-code correctness fixes, performance improvements for large modules, regression tests and documentation.

## Reporting analysis bugs

Please include:

- Ghidra version and plugin release/commit;
- target language (WebAssembly or WebAssembly64);
- compiler/toolchain when known;
- expected versus actual behavior;
- relevant analyzer settings;
- the smallest redistributable reproducer you can provide.

Do not publish proprietary samples. Reduce them or create a synthetic equivalent.

## Pull requests

Keep changes focused and explain the WebAssembly semantics being implemented or corrected. Describe how the change was validated and add a regression case when practical.

For SLEIGH/P-code changes, verify both disassembly and decompiler behavior. For loader/parser changes, include malformed-input handling where relevant.

## Attribution

This repository extends GPL-licensed Ghidra WebAssembly projects. Preserve applicable copyright and attribution notices in inherited files.
