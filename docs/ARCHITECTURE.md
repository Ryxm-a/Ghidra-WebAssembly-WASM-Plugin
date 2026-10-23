# Architecture

## Pipeline

```text
WASM binary
  -> module parser / loader
  -> sections + types + imports/exports
  -> functions + tables + memories + globals
  -> pre-analysis
  -> contextual SLEIGH disassembly
  -> P-code
  -> Ghidra analysis + decompiler
```

## Why pre-analysis exists

WebAssembly is a typed stack machine with structured control flow. Some operands and branch semantics cannot be represented usefully by decoding an opcode in isolation. The pre-analyzer walks functions first and establishes context consumed by the processor definition.

## Register model

WebAssembly machine state is mapped into register-like constructs suitable for Ghidra. The implementation models function inputs/outputs, locals and the WASM value stack separately. This leaves Ghidra's conventional stack machinery available for recovering compiler-generated C stacks.

## Linear memory

The extension includes conventional WebAssembly and WebAssembly64 language definitions. The latter models memory64's wider linear-memory address space.

## Tables and indirect calls

Tables are commonly the lowered representation of function pointers. The loader/analyzers establish references where they can be determined statically; helper scripts improve naming and resolution for compiler-specific patterns such as Emscripten dyncalls.

## Threads and atomics

The language definitions include the `0xFE` atomic instruction family and shared-memory handling, including atomic loads/stores, read-modify-write operations, wait/notify and fences.

## C-stack recovery

Compiler-generated WebAssembly frequently maintains a conventional stack pointer in a global. The analyzer can recover that model while keeping the WebAssembly value stack represented independently.

## Pressure points

Large modules require substantial context setup and can make initial analysis expensive. Function inlining is difficult because an inlined callee shares decompiler state with its caller. Multi-value return behavior also needs stronger regression coverage.
