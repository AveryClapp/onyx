# Onyx

*A build system that reads your code instead of making you describe it.*

## What

Onyx builds C++ projects by analyzing your source files. No `CMakeLists.txt`, no `BUILD` files, no build configuration language to learn. Your code is the spec.

```bash
$ onyx build
Analyzing dependencies...
Building 47 targets (cached 45)
Done in 1.2s
```

## Why

C++ developers maintain the same dependency graph in two places: once in `#include` directives, once in build files. Onyx eliminates the second copy. Your includes already declare what depends on what. Onyx reads them directly.

## Features

**Incremental builds that are correct.**
Content-addressable cache keyed on source content, compiler flags, and dependency versions. Rebuilds only what actually changed. `onyx why-rebuild foo.o` explains exactly why something was recompiled.

**Zero config for standard projects.**
Conventional directory layout → Onyx infers libraries, executables, and tests automatically. Non-standard structures are handled through a minimal TOML escape hatch.

**Integrated package management.**
PubGrub version solver with full semantic versioning support. Declare dependencies in `onyx.toml`, Onyx handles resolution, fetching, and integration.

**Explainable builds.**
Every decision Onyx makes is queryable. Build traces show the full chain from source change to recompilation, not just the final result.

**Build-through-deploy.**
Onyx knows exactly what changed, which artifacts are affected, and what the minimal deployment unit is. Instead of handing off to a blind CI/CD pipeline that rebuilds and redeploys everything, Onyx generates minimal deployment artifacts containing only what changed. The build system is the only system with full knowledge of your dependency graph. It should own the full pipeline from source to deployment.

```bash
$ onyx deploy --target staging
3 files changed, 1 shared object affected
Generating minimal patch artifact (48KB vs 2.1GB full image)
Pushing to staging cluster...
Deployed in 4.2s
```

## Status

Early development. The goal is self-hosting: Onyx builds Onyx.

## Design

Onyx is written in modern C++ and uses libclang for source analysis, SQLite for the build database, and a from-scratch implementation of the PubGrub dependency resolution algorithm. Builds are content-addressed and reproducible by construction.

---

*Build systems should be compilers, not configuration languages.*
