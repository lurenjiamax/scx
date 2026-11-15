# Thor LAVD stability build

Base: upstream v1.1.3, `c8728c6b6a3fde451f0f10b95f99aad7a32a750a`.
Five upstream commits imported once from Pocknix's 0001–0005 patches:
`6d31ddd`, `d762220`, `02ff6a5`, `e6aab93`, `0745c74`.
The Arch Linux ARM 1.1.3-2 package was replaced from this known source base,
not patched in place; its version alone is not evidence of every carried fix.

The native ARM64 recipe builds the upstream workspace binary set, excluding
the same development-only members as Pocknix. It uses installed Rust and a
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

Package identity: scx-scheds 1.1.3-3. Installation and live scheduler
acceptance remain outstanding until explicitly recorded by the integrator.
