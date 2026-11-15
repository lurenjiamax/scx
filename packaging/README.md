# Thor LAVD main build

Base: upstream main, `8820f95ed56da7bae2966477fa457cb488a7207d`.
It already includes the five upstream fixes previously carried from Pocknix:
`6d31ddd`, `d762220`, `02ff6a5`, `e6aab93`, `0745c74`.
They were skipped as already applied during rebase, not applied a second time.

The native ARM64 recipe builds the workspace except development/self-test
members and experimental schedulers requiring a separate nightly Rust BPF
toolchain. The removed upstream scx_rustland binary is not retained. It uses installed Rust and a
checksum-pinned mbx 1.30.0 build wrapper, with automatic cache GC disabled.
No unit tests are invoked. Thor retains its existing LAVD launch arguments.
The bundled libbpf C build pre-includes system Linux types: its private shim
lacks `__u128`, required by ARM64 linux-api-headers 7.3 signal/ptrace structs.
No system headers or Cargo registry sources are modified.

Build on ARM64 with prerequisites installed:

```sh
cd packaging
makepkg --nocheck
```

Package identity: scx-scheds 1.1.4.r883.g8820f95e-1. Installation and live scheduler
acceptance remain outstanding until explicitly recorded by the integrator.
