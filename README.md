<div align="center">

# Ghidra WebAssembly

### Modern WebAssembly analysis & decompilation for Ghidra

**Disassemble. Decompile. Navigate. Understand.**

[![Ghidra](https://img.shields.io/badge/Ghidra-12.1.4-EA3B3B?style=for-the-badge)](https://github.com/NationalSecurityAgency/ghidra)
[![WebAssembly](https://img.shields.io/badge/WebAssembly-WASM-654FF0?style=for-the-badge&logo=webassembly&logoColor=white)](https://webassembly.org/)
[![Release](https://img.shields.io/github/v/release/Ryxm-a/Ghidra-WebAssembly-WASM-Plugin?style=for-the-badge)](https://github.com/Ryxm-a/Ghidra-WebAssembly-WASM-Plugin/releases/latest)
[![License](https://img.shields.io/github/license/Ryxm-a/Ghidra-WebAssembly-WASM-Plugin?style=for-the-badge)](LICENSE)

A maintained Ghidra extension for serious WebAssembly reverse engineering — with **memory64**, **threads/atomics**, SIMD, cross-references, C-stack recovery, P-code and Ghidra decompilation.

[**Download**](https://github.com/Ryxm-a/Ghidra-WebAssembly-WASM-Plugin/releases/latest) · [**Install**](#-installation) · [**Capabilities**](#-capabilities) · [**Architecture**](docs/ARCHITECTURE.md) · [**Report a bug**](https://github.com/Ryxm-a/Ghidra-WebAssembly-WASM-Plugin/issues/new/choose)

</div>

---

## Why this exists

WebAssembly is a typed stack machine, not a conventional native ISA. Useful reversing requires more than decoding bytes: structured control flow, value-stack context, tables, globals, linear memory, compiler-generated C stacks and function signatures all need to be represented in a form Ghidra can reason about.

**Ghidra WebAssembly turns a `.wasm` module into a navigable Ghidra program.**

Import a module and use the workflows you already know: disassembly, symbols, references, scripts, P-code and decompilation.

This project continues the open-source Ghidra WebAssembly lineage while maintaining a modern Ghidra build and extending support for newer WebAssembly capabilities.

## ✨ Capabilities

| Capability | Status |
| --- | :---: |
| WebAssembly module loading | ✅ |
| Disassembly + Ghidra decompilation | ✅ |
| WebAssembly 1.0 instruction set | ✅ |
| **memory64 / 64-bit linear-memory analysis** | ✅ |
| **Threads / atomics (`0xFE`)** | ✅ |
| Shared memories | ✅ |
| SIMD instructions | ✅ |
| Function-call & branch XREFs | ✅ |
| Table/global function-pointer XREFs | ✅ |
| C-stack recovery | ✅ |
| Positive- and negative-growing C stacks | ✅ |
| P-code analysis/emulation support | ✅ |
| DWARF language integration | ✅ |
| Dynamic-call/table helper scripts | ✅ |

### memory32 + memory64

The extension includes language definitions for conventional WebAssembly and **WebAssembly64**. The 64-bit variant models the wider linear-memory address space required by memory64 modules.

### Threads + atomics

The processor definitions include the `0xFE` atomic instruction family and shared-memory handling, including atomic loads/stores, read-modify-write operations, wait/notify and fences.

## 🚀 Installation

1. Open the [latest release](https://github.com/Ryxm-a/Ghidra-WebAssembly-WASM-Plugin/releases/latest).
2. Download the extension ZIP matching the supported Ghidra version — currently **Ghidra 12.1.4**.
3. In Ghidra choose **File → Install Extensions…**
4. Click **+** and select the ZIP.
5. Enable the extension and restart Ghidra.
6. Import a `.wasm` module.

> The current packaged release targets **Ghidra 12.1.4**. Ghidra extensions are version-sensitive; other releases may require a matching build.

## 🔬 Analysis pipeline

```text
.wasm
  │
  ▼
Module parser + loader
  │
  ├─ types / imports / exports
  ├─ functions / globals
  ├─ tables / memories
  └─ element / data segments
  │
  ▼
Wasm pre-analysis
  │
  ├─ value-stack context
  ├─ structured branch targets
  ├─ references
  └─ C-stack recovery
  │
  ▼
SLEIGH → P-code → Ghidra analysis → Decompiler
```

See **[Architecture](docs/ARCHITECTURE.md)** for the technical model.

## 🧰 Included scripts

| Script | Purpose |
| --- | --- |
| `analyze_dyncalls.py` | Analyze Emscripten-style dynamic-call helpers and improve indirect-call references/names |
| `rename_table_funcs.py` | Name functions using function-table positions |
| `emulate_writev.py` | Assist WASM emulation experiments |
| `spectest.py` | Specification-oriented test/support tooling |

## 🧠 Reversing tips

**C stack:** Emscripten/Clang-style programs commonly keep a conventional C stack pointer in a WebAssembly global. The analyzer attempts to detect it automatically. If needed, configure **C Stack Pointer** in Wasm Pre-Analyzer options before initial analysis.

**Stack direction:** the default compiler specification assumes a downward-growing C stack. For upward-growing targets, select the `pos-stack` compiler specification.

**Indirect calls:** WebAssembly tables frequently represent compiler-level function pointers. The included dyncall/table scripts can improve names and references for these patterns.

**Passive/runtime-positioned segments:** when a segment's destination cannot be determined statically, `WasmLoader` can be called from a Ghidra script with a known runtime offset.

## ⚠️ Known limitations

This project aims for useful, correct reverse engineering — not a claim that every WebAssembly proposal and compiler pattern decompiles perfectly.

- Ghidra function inlining can confuse WASM stack/local state.
- Changing the selected C-stack pointer after initial analysis is not seamless.
- Initial analysis of very large modules can be slow because substantial context is established before disassembly.
- Multiple return values are not yet considered fully validated.

A minimal redistributable reproducer is the fastest way to get an analysis problem fixed.

## 🏗️ Development

The repository currently contains the packaged extension plus its source archive. The project is being normalized into a conventional source-first development layout so builds, tests and releases can be reproduced directly from Git.

See [CONTRIBUTING.md](CONTRIBUTING.md), [Architecture](docs/ARCHITECTURE.md), and the [Roadmap](ROADMAP.md).

## 🌳 Lineage & attribution

This project builds on substantial GPL-licensed open-source work:

- [nneonneo/ghidra-wasm-plugin](https://github.com/nneonneo/ghidra-wasm-plugin) — principal upstream implementation.
- [garrettgu10/ghidra-wasm-plugin](https://github.com/garrettgu10/ghidra-wasm-plugin) — earlier disassembly/decompilation work.
- [andr3colonel/ghidra_wasm](https://github.com/andr3colonel/ghidra_wasm) — early loader work.
- [NSA Ghidra](https://github.com/NationalSecurityAgency/ghidra) — the reverse-engineering framework.

The goal is to move this tooling forward while keeping its lineage visible.

## 🤝 Contributing

Compatibility fixes, modern WASM support, SLEIGH/P-code improvements, performance work, test cases and documentation are welcome. Start with [CONTRIBUTING.md](CONTRIBUTING.md).

## 📄 License

GNU General Public License v3.0. See [LICENSE](LICENSE).

---

<div align="center">

### Reverse WebAssembly where you reverse everything else.

If the project helps your research, a ⭐ makes it easier for other reverse engineers to find.

**[Download](https://github.com/Ryxm-a/Ghidra-WebAssembly-WASM-Plugin/releases/latest)** · **[Issues](https://github.com/Ryxm-a/Ghidra-WebAssembly-WASM-Plugin/issues)** · **[Contribute](CONTRIBUTING.md)**

</div>
