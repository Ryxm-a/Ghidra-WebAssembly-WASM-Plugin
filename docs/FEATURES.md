# Feature matrix

This matrix distinguishes implemented project capabilities from areas that still need stronger validation.

| Area | State | Notes |
| --- | --- | --- |
| Core WASM loading | Supported | Module/section loader |
| WASM 1.0 instructions | Supported | Core processor definition |
| SIMD | Supported | `VectorOps.sinc` |
| Threads / atomics | Supported | `AtomicOps.sinc`, shared-memory handling |
| memory64 | Supported | Dedicated WebAssembly64 language/compiler definitions |
| Call/branch XREFs | Supported | Analysis integration |
| Table/global function references | Supported | Static references where recoverable |
| C-stack recovery | Supported | Compiler-generated stack pointer model |
| Positive-growing C stack | Supported | `pos-stack` compiler spec |
| P-code | Supported | Used for Ghidra analysis/decompilation |
| DWARF language mapping | Present | `WebAssembly.dwarf` |
| Multiple returns | Needs validation | Do not advertise as complete |
| Function inlining | Known limitation | Can confuse stack/local state |
| Very large modules | Functional but performance-sensitive | Initial context setup can be expensive |

## Support policy

“Supported” should mean more than “the parser accepts the bytes.” New features should ideally be covered by a small reproducible module that exercises loading, disassembly and P-code/decompilation as applicable.
