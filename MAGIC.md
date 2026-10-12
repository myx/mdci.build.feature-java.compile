# MAGIC.md — build.feature-java.compile

Maintainer notes. Users read `README.md`. How the packages compose: `../MAGIC.md`.

## The project path is written into the scripts

- Both `sh-scripts/*.fn.sh` source their help and `sh-lib/RunJavaClassSource.include` from `$MDSC_SOURCE/myx/mdci-packages-myx/build.feature-java.compile/…`, a literal path.
- Moving or renaming this project breaks `--help` and compilation until those paths change too.

## How a project opts into the builder

- `2301-compile-java.sh` runs `Distro ListDistroProvides --select-changed --filter-and-cut "source-process:"` and keeps the lines ending in ` compile-java`. So a project is compiled only when it provides `source-process:compile-java` and has changed.
- `RunJavaClassSource` compiles the tool class itself with `javac` from `myx/myx.distro-system/java` before running it, into `$MMDAPP/.local/output-cache/distro/myx/myx.distro-system/java`.

## This project has its own `.git`

- It is its own git repository inside `mdci-packages-myx`, like `setup.feature-monit` and `setup.feature-myx.common`.
