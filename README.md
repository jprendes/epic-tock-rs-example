# RISC-V Embedded PIC Tock OS Rust App Example

## Overview

lowRISC is working on a specification and [prototype toolchain implementation](https://github.com/lowRISC/llvm-project/commits/epic) of an Embedded PIC (ePIC) ABI for RISC-V.

This repository illustrates how to use the work-in-progress ePIC toolchain implementation to create relocatable RISC-V Tock OS applications. It builds a libtock-rs `console` example app with an ePIC configuration and runs it under QEMU. The example prints the addresses and values of some program symbols, to demonstrate the relocation capabilities.

## Building and Running

First you need to clone this repo and its submodules
```
git clone --recursive https://github.com/jprendes/epic-tock-rs-example.git
```

If you didn't clone recursively, you need to initialize the submodules:
```
git submodule update --init --recursive
```

Build requirements:

- LLVM build dependencies

The other dependencies are installed automatically. This example has been tested against Tock commit `935755eb3`.

Use `cmake -S . -B ./build -G Ninja` to configure the project and `cmake --build ./build` to build everything.

If you already have ePIC enabled LLVM and `rustc` builds, you can specify their locations with `LLVM_DIR` and `RUST_DIR`.
For example: `cmake -S . -B ./build -G Ninja -DLLVM_DIR=/path/to/epic-llvm -DRUST_DIR=/path/to/epic-rust`.
LLVM binaries will be searched in `${LLVM_DIR}/bin/` and rustc binaries will be searched in `${RUST_DIR}/bin`.

Use `cmake --build ./build -- run-console-hifive1` to run the app in hifive1, and `cmake --build ./build -- run-console-opentitan_earlgrey_cw310` to run the app in opentitan.

## Licensing

Unless otherwise noted, everything in this repository is covered by the Apache License, Version 2.0 (see [LICENSE](LICENSE) for full text).
