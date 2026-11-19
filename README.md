# Common Expression Language (C++)

The Common Expression Language (CEL) C++ implementation provides a parser,
type checker, compiler, and runtime for evaluating CEL expressions. For language
semantics and specification details, see the [cel-spec][1] repository.

## Prerequisites & Building with Bazel

`cel-cpp` builds and tests with [Bazel](https://bazel.build/) using Bzlmod
(`MODULE.bazel`, Bazel version specified in `.bazelversion`).

Build all targets:

```bash
bazel build //...
```

Run the test suite:

```bash
bazel test //...
```

For compiler requirements (GCC/Clang on Linux, MSVC on Windows, Xcode on macOS)
and a reference Docker configuration, see [`codelab/README.md`](codelab/README.md)
and [`codelab/Dockerfile`](codelab/Dockerfile). To consume `cel-cpp` from another
Bazel project via `MODULE.bazel`, refer to the Bzlmod setup instructions in
[`codelab/README.md`](codelab/README.md#setting-up-a-bazel-project-with-cel-cpp).

## Codelab & Custom Functions

Step-by-step exercises live in [`codelab/`](codelab/README.md):

- Basic compilation and evaluation (`exercise1`–`exercise3`)
- Adding custom C++ extension functions (`codelab/exercise4.h`,
  `codelab/exercise4.cc`, and `codelab/network_functions.cc`)
- Custom struct/type integration (`codelab/exercise10.cc`)

Build and test the codelab with:

```bash
bazel build //codelab:all
```

## Architecture & API Guide

New integrations should use the modern `cel` APIs (`compiler/` for parsing and
type-checking, `runtime/` for `cel::RuntimeBuilder` and `cel::Runtime`, and
`common/value.h` for `cel::Value`):

- Compiler entrypoints: [`compiler/`](compiler/) (`Compiler`, `CompilerBuilder`)
- Runtime and evaluation guide: [`eval/README.md`](eval/README.md) (covers
  `cel::Runtime`, `cel::Value`, `cel::Activation`, `BindProtoToActivation`,
  `FunctionAdapter`, and migration from legacy `google::api::expr::runtime` APIs)

## License

Released under the [Apache License](LICENSE).

[1]: https://github.com/cel-expr/cel-spec
