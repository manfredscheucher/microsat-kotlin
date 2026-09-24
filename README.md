# microsat-kotlin

A [Kotlin Multiplatform](https://kotlinlang.org/docs/multiplatform.html) port of the
**microSAT** SAT solver (Marijn Heule). Plain Kotlin, no FFI and no native library, so it
runs on any Kotlin target (JVM, Android, native, browser).

The smallest of the four. It uses integer VMTF (no floating-point activities), so the trace matches the C on the tested instances without any float-order caveats.

It implements the `SatSolver` interface from
[ksat-common](https://github.com/manfredscheucher/ksat-common), which is pulled in as a
git submodule (mounted at `common/`). Package namespace is `org.bytefred.ksat`.

## Byte-for-byte port

This is a line-by-line port of the original C/C++ solver, verified against it trace by
trace (same decisions, propagations and conflicts in the same order), not just on the
final SAT/UNSAT answer. That verification harness — the instrumented C reference, the
test CNFs, the golden traces and the shadow tests — lives in the main repo, together with
the benchmarks, the `Ksat` facade and the docs:
**[sat-solvers-kotlin](https://github.com/manfredscheucher/sat-solvers-kotlin)**.

This repo is just the solver source, so it can be reused on its own.

## Build

Requires a JDK and the Gradle wrapper in this repo. `common/` must be checked out
(clone with `--recursive`, or `git submodule update --init`).

```bash
./gradlew compileKotlinJvm   # or build for all targets
```

## License

MIT, see [LICENSE](LICENSE). This port is a derivative work of the MIT-licensed original
(Marijn Heule); the original license text is preserved in [LICENSE](LICENSE).
