# Building from source

## Current packaged-source layout

The current release repository contains the Java source archive at:

`lib/ghidra-wasm-plugin-src.zip`

alongside the compiled extension artifacts. A future normalization will move that archive back into a conventional `src/main/java` tree after the source archive has been extracted and verified byte-for-byte against the shipped JAR.

The archive should **not** be reconstructed from decompiled bytecode: preserving the authored source and history is more important than making the tree look conventional.

## Extension data

Processor/language definitions are already source-visible under `data/languages/`, including SLEIGH sources for standard WebAssembly, SIMD, atomics and the WebAssembly64 variant.

## Reproducibility goal

A normalized checkout should eventually support:

```bash
export GHIDRA_INSTALL_DIR=/path/to/ghidra
gradle buildExtension
```

and produce an installable extension ZIP in `dist/`.

Until the Java source archive is promoted to the source tree, use the prebuilt GitHub Release for normal installation.

## Why the repository is not silently unpacking the ZIP

The GitHub integration used for this repository overhaul can safely edit UTF-8 repository files but cannot decode/download the binary source ZIP through its content API. Moving source therefore requires a verified binary extraction step rather than guessing or reconstructing files.
