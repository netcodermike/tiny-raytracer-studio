# Tiny Raytracer Studio

Render a small sphere scene with adjustable light position and PNG export.

[![Build and verify](https://github.com/netcodermike/tiny-raytracer-studio/actions/workflows/verify.yml/badge.svg)](https://github.com/netcodermike/tiny-raytracer-studio/actions/workflows/verify.yml)

**Language:** C++ · **Platform:** Windows, macOS, Linux desktop · **App type:** Scene renderer with material/light controls

First-release learning implementation, with explicit scope below. This is one independently runnable app, not a placeholder in a combined repository.

## Features

- Native Qt image window
- Sphere intersections
- Diffuse/specular light and hard shadows
- PNG render export

## Requirements

C++17, CMake 3.16+, and Qt 6 Widgets. Ubuntu: sudo apt-get install qt6-base-dev. On other systems install the matching Qt compiler kit and set CMAKE_PREFIX_PATH.

## Quick start

```sh
git clone https://github.com/netcodermike/tiny-raytracer-studio.git
cd tiny-raytracer-studio
cmake -S . -B build
cmake --build build --config Release
# Linux/macOS: ./build/app
# Windows MSVC: .\build\Release\app.exe
```

Commands run from the repository root. Lines marked for a particular operating system apply only there. Language tools are prerequisites, not installed by the app. Close desktop windows normally; terminal/server apps stop with Ctrl+C unless their usage notes say otherwise.

## Example workflow

Render light x=2, export PNG, then compare with x=-3 to inspect highlight/shadow movement.

## Architecture, configuration, and data

main.cpp traces one ray per pixel through a fixed 640×400 scene containing two spheres and a large ground sphere. It selects nearest positive intersections, computes normal/light directions, checks shadow occlusion, and combines ambient/diffuse/specular terms. A text field controls light x from -5 to 5. Tests verify known hit/miss distances and nonuniform image output.

## Verification

Build with the quick-start command where needed, then run:

```sh
ctest --test-dir build -C Release --output-on-failure
```

Manual acceptance: Render light x=2, export PNG, then compare with x=-3 to inspect highlight/shadow movement. Also test malformed inputs and an unwritable output destination.

See [validation record](docs/VALIDATION.md) for observed checks and their limits. CI results verify only what the workflow runs; they do not establish native GUI correctness or production readiness.

## Limitations and next steps

Fixed scene/camera/materials/resolution, one sample per pixel, no reflections, refraction, recursion, anti-aliasing, physically based color, or scene import. Rendering blocks the UI briefly. PNG export replaces the chosen file.

## Troubleshooting

Use the exact platform/toolchain above. Preserve originals and use synthetic fixtures first. Errors are displayed in the UI or stderr. A headless machine can run the model tests but cannot verify native GUI/audio behavior. Output paths are chosen explicitly; keep backups of important data.

## Source map

- `CMakeLists.txt`
- `main.cpp`

## Development and license

Read [contributing](CONTRIBUTING.md) before changing the app, and [security/privacy](SECURITY.md) before supplying private data. Use synthetic fixtures for tests. No telemetry, paid API key, or account is required by the app itself. Dependencies, when present, are stated in Requirements.

[MIT license](LICENSE), copyright 2026 netcodermike.
