# Ghidra-WebAssembly-WASM-Plugin
WebAssembly analysis and decompilation support for Ghidra, developed and maintained for Ghidra 12.1.4.
# Ghidra WebAssembly Plugin

A WebAssembly (`.wasm`) analysis extension for Ghidra, bringing disassembly, control-flow analysis, and decompilation support to WebAssembly binaries.

## Features

- WebAssembly module loading
- Instruction disassembly and analysis
- Control-flow analysis
- Function references and cross-references
- Ghidra decompiler integration

## Compatibility

**Target version: Ghidra 12.1.4**

Compatibility with other versions may vary.

## Installation

1. Download the latest extension ZIP from [Releases](../../releases).
2. Open Ghidra and select **File → Install Extensions**.
3. Click **+** and select the downloaded ZIP.
4. Enable the extension if necessary and restart Ghidra.
5. Import your `.wasm` file and begin analysis.

## Building

Set `GHIDRA_INSTALL_DIR` to your Ghidra installation directory, then run:

```powershell
.\gradlew.bat buildExtension
```

The generated extension ZIP will be available in the `dist` directory.

## License

See the `LICENSE` file for details.

## Credits

Based on the original [Ghidra WebAssembly Plugin](https://github.com/garrettgu10/ghidra-wasm-plugin).
