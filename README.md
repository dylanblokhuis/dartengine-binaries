# Dart Engine Binaries

Prebuilt Dart VM engine shared libraries (JIT and AOT) for macOS, built from the
[Dart SDK](https://github.com/dart-lang/sdk).

Dart Engine is a way to easily embed Dart into your own app by using the
DartEngine_* symbols. Although its currently hard to get the full dev tooling
fully setup like hot reloading, I'd recommend to use
https://github.com/fuzzybinary/dart_shared_library in development and use
DartEngine in production for maximum performance.

## Downloads

Go to [Releases](https://github.com/YOUR_ORG/dartengine-binaries/releases) and
pick a version. Each release includes:

| Asset                             | Description              |
| --------------------------------- | ------------------------ |
| `libdart_engine_jit_shared.dylib` | Dart VM engine, JIT mode |
| `libdart_engine_aot_shared.dylib` | Dart VM engine, AOT mode |

These are built on **macOS** (`.dylib`); architecture matches the runner (e.g.
ARM64 on current GitHub-hosted macOS).

## How releases are built

When you
[publish a release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-your-repository)
(e.g. tag `v3.11.0`):

1. A GitHub Action runs on `macos-latest`.
2. The workflow fetches the Dart SDK (via depot_tools) and checks out the **same
   tag** as your release if it exists in the Dart SDK; otherwise the latest Dart
   SDK release tag.
3. It adds a `libdartengine` build group to the SDK’s `BUILD.gn` and runs the
   build.
4. The two `.dylib` files are uploaded as assets to that release.

So each release here is tied to a Dart SDK version (by tag) and contains the
corresponding engine shared libraries.

## Versioning

Use release tags that match the Dart SDK when possible (e.g. `v3.11.0` for Dart
SDK 3.11.0). That way the workflow will build from the same Dart version and the
artifacts align with that SDK.

## License

The built libraries are produced from the Dart SDK; their license is the same as
the [Dart SDK license](https://github.com/dart-lang/sdk/blob/main/LICENSE).
