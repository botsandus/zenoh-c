# Coordinated Zenoh wrapper candidate

Based on upstream Zenoh-C 1.10.2 (`363554eef1a52b1c59a37fc2c8aa87ec1aa8e52e`).
All 32 core workspace packages resolve to public core revision
`0acbd21e9358c50e4b129111f024b7576c589889` in `botsandus/zenoh`.
The root manifest, CMake template and opaque-type generator use the same pin.
Keep these in sync: opaque-type layouts are part of the C ABI.

Build with Rust 1.93.0 or newer, shared-memory and unstable APIs enabled. The
legacy 1.75 fallback is rejected because it selects a different dependency set.
CMake builds use the committed lockfile and `--locked`.

```sh
cmake -S . -B build -DZENOHC_BUILD_WITH_SHARED_MEMORY=ON -DZENOHC_BUILD_WITH_UNSTABLE_API=ON
cmake --build build -j4
ctest --test-dir build --output-on-failure
```

Use Zenoh-C++ 1.10.2 (`20eb0bef670e150d3750ca0739dcb28cd7909e2e`) with these
headers and this native library. This is a test candidate, not fleet qualification.
