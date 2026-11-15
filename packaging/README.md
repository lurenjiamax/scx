# Thor scx package

Build on ARM64 with the dependencies listed in `PKGBUILD`:

```sh
cd packaging
makepkg --nocheck
```

The recipe uses the installed Rust toolchain and a checksum-pinned mbx wrapper.
Thor selects the scheduler mode through `thorch-lavd-mode`.
