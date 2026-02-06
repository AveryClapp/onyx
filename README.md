# onyx

*A build system that reads your code instead of making you write yaml*

## what

onyx builds C++ projects by analyzing your source files. no `CMakeLists.txt`, no `BUILD` files, no build configuration at all for most projects.

```bash
$ onyx build
analyzing dependencies...
building 47 targets (using cache for 45)
done in 1.2s
```

## why

because maintaining a dependency graph in two places (your includes + your build files) is insane.

your `#include` directives already declare what depends on what. onyx just reads them.

## features that actually matter

**incremental builds that work**  
content-addressable cache + proper dependency tracking = rebuilds only what changed  
`onyx why-rebuild foo.o` explains exactly why something recompiled

**zero config for normal projects**  
conventional directory layout? onyx infers libraries, executables, tests  
need weird stuff? minimal TOML for escape hatches

**package management that doesn't suck**  
pubgrub version solver, semantic versioning that works  
`onyx.toml` declares deps, onyx handles the rest

**builds you can understand**  
every decision is explainable, every rebuild justified  
build traces show *why*, not just *what*

## status

early development. bootstrapping onyx with onyx.

## why does c++ not have this already

good question.

---

*build systems should be compilers, not configuration languages*
