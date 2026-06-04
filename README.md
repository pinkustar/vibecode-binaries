# vibecode-binaries

Build factory for the prebuilt **Windows x64 engine binaries** the vibecode app
ships. Each binary is produced in CI, published as a GitHub release, and pinned
by URL + SHA-256 in vibecode's `engine/manifest.json`.

No forks, no source mirrors, no sync: each workflow **clones the upstream project
at a pinned ref**, builds it, and publishes a release zip + `.sha256`.

| Workflow | Builds | Upstream | License |
|---|---|---|---|
| `build-ffmpeg.yml` | minimal decode-only static `ffmpeg.exe` (~1.8 MB) | [FFmpeg](https://github.com/FFmpeg/FFmpeg) | LGPL-2.1 |
| `build-vibra.yml` | `vibra.exe` + runtime DLLs (Shazam fingerprinting CLI) | [BayernMuller/vibra](https://github.com/BayernMuller/vibra) | Apache-2.0 |

Both are `workflow_dispatch` (manual) with a ref/tag input, so every build is
deterministic and reproducible. Each workflow's configure/build steps double as
the corresponding build recipe — and, for ffmpeg's LGPL, the relink source.
