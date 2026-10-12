# mdci.build.feature-java.compile

A build feature for the distro source pipeline: compiles the Java sources of cached projects, and declares the jar and classpath build tools.

Maintainer notes: `MAGIC.md`.

- `CompileCachedJavaProject.fn.sh` — compile Java sources for one cached project.
- `CompileCachedJavaRepository.fn.sh` — compile Java sources for a whole cached repository.

## What it provides

- Build tools (`make/*.inf`): `pack.jar`, `pack.java.jar` (`ru.myx.distro.make.FolderPackBuilder`), `classpath.jar`, `classpath.java.jar` (`ScanClasspathJavaBuilder`), `classpath.use.jars` (`ScanClasspathJarsBuilder`).
- A source-process builder, `builders/source-process/2301-compile-java.sh`. It compiles, in parallel, every changed project that provides `source-process:compile-java`.
- The two commands above, through `Declares: custom-commands-path:sh-scripts`.

## What it uses

- `javac` and `java` on `PATH`.
- `myx.common` (`lib/prefix`, `lib/parallel`) for the builder.
- The class `ru.myx.distro.prepare.MakeCompileSources`, compiled from `myx/myx.distro-system` source by `sh-lib/RunJavaClassSource.include`.
- `MMDAPP` and `MDSC_SOURCE` set. Output goes to `$MMDAPP/.local/output-cache/`.

## Commands

| command | does |
|---|---|
| `CompileCachedJavaProject <project>` | compiles one project; also `--project-from-env` (`MDSC_PRJ_NAME`) and `--project-from-pwd` |
| `CompileCachedJavaRepository <repository>` | compiles every project in a repository, such as `myx` or `lib` |

Each takes `--help`. The help text is in `sh-lib/help/`.
