<div align="center">
  <img
    src="https://github.com/user-attachments/assets/f0e9902a-68a0-4cb0-9854-643064db10a3"
    alt="Coffee Talk Tokyo Vita"
    width="320"
  />

  <h1>Coffee Talk Tokyo Vita</h1>

  <p><em>I'll have a medium iced latte, no sugar please.</em></p>

  <p>
    An unofficial native backport of <strong>Coffee Talk Tokyo</strong>
    to the <strong>PlayStation Vita</strong>, bringing Tokyo's cozy
    late-night café experience to Sony's handheld.
  </p>
  <p>
    <img src="https://img.shields.io/badge/STATUS-WORK_IN_PROGRESS-orange?style=for-the-badge" alt="Work in progress">
    <img src="https://img.shields.io/badge/PLATFORM-PS_VITA-003791?style=for-the-badge&logo=playstation&logoColor=white" alt="PS Vita">
    <img src="https://img.shields.io/badge/UNITY-2017.4.10f1-222222?style=for-the-badge&logo=unity&logoColor=white" alt="Unity 2017.4.10f1">
    <img src="https://img.shields.io/badge/SCOPE-DEMO%20%2B%20FULL-yellow?style=for-the-badge" alt="Demo and full game development">
  </p>
  <p>
    <a href="https://github.com/WolffsRoom/CoffeeTalkTokyoVita/releases">Releases</a> ·
    <a href="https://github.com/WolffsRoom/CoffeeTalkTokyoVita/issues">Report an issue</a> ·
    <a href="https://wolffsroom.github.io/WolffsRoomSite/">Wolff's Room</a>
  </p>
</div>

CoffeeTalkTokyoVita aims to bring the original visual novel and coffee-brewing experience to the PlayStation Vita by backporting the game's Unity project from **Unity 6** to **Unity 2017.4.10f1**, an engine version with a native PSP2 build target.

Rather than recreating the game in a different engine or streaming the PC version, the project adapts the original scenes, C# gameplay logic, dialogue systems, animations, UI and asset formats to the legacy Unity runtime.

> [!IMPORTANT]
> Development is now split into two independent native Vita backports: **Coffee Talk Tokyo Demo** and **Coffee Talk Tokyo** (full game).
>
> The demo has reached gameplay on real Vita hardware. The full game is still undergoing compatibility migration and has not yet produced a validated Vita build.
>
> This is an experimental, unofficial fan project. No proprietary game data, decompiled game code, or licensed Unity/PlayStation SDK binaries are distributed by this repository. Obtain the original game from its official source.

---

## Project Status

| Edition | Development version | Title ID | Status |
| :--- | :---: | :---: | :--- |
| **Coffee Talk Tokyo Demo** | v0.19 | `CTTK01001` | Native VPK built; latest changes awaiting hardware testing |
| **Coffee Talk Tokyo** | v0.1 | `CTTK02001` | Full game migration in progress; no validated VPK yet |

The two editions use separate project directories and application IDs, allowing independent installations and save data. Version numbers refer to development builds, not necessarily public releases.

### Demo — v0.19

The native demo has reached the café, dialogue and smartphone recipe interface on real Vita hardware. Recent development focuses on stability, physical controls and performance.

- Native PSP2 / IL2CPP build at 960 × 544.
- 34 music tracks through a native OGG Vorbis streaming plugin.
- BC1/DXT1, BC3/DXT5, RGB565 and RGBA4444 texture optimizations.
- Native on-screen keyboard for barista name entry.
- Physical gamepad navigation, touchscreen interaction and right-stick camera movement.
- Improved virtualized recipe list handling and music app text rendering.
- Reduced auxiliary camera and Latte Art simulation workloads.
- Low-latency audio effects and per-state frame-time/memory logging.

The v0.19 development VPK is approximately **173 MB**, down from approximately 195 MB in v0.18. The build and package audits passed; the latest fixes still require physical hardware verification.

### Full game — v0.1

The full PC game is being adapted in a separate Unity 2017 project, using the demo's compatibility work as a starting point.

| Migration milestone | Status |
| :--- | :--- |
| Original full-game scenes and dialogue resources | Recovered |
| 10 original scenes and 16 day-localization CSV files | Preserved |
| 47 original OGG music tracks | Prepared for native streaming |
| 7,448 sprite assets | Converted to legacy geometry |
| 71 TextMeshPro font assets | Converted; visual verification pending |
| PSP2 and desktop C# diagnostics | Passed |
| Unity scene import and reference validation | In progress |
| Native full-game VPK | Pending |
| Complete campaign and save/load tests on Vita | Pending |

The goal is a faithful **1:1 backport**, keeping the original gameplay and presentation wherever possible while adapting the implementation to the Vita's hardware and legacy engine. Some visual effects and performance-sensitive systems still require compromises and further testing.

---

## What Has Been Done

### 1. Unity Engine Backport

- Recovered the original demo's Unity scenes and serialized assets into a development project.
- Migrated the project to Unity 2017.4.10f1, preserving asset GUIDs and scene references where possible.
- Adapted approximately 1,470 C# scripts and integrated all eight recovered demo scenes.
- Replaced unsupported modern C# and Unity API calls with legacy-compatible equivalents.
- Converted plugin importer metadata and repaired incompatible managed-library references.
- Validated the eight scenes without missing script components in the Unity editor.

### 2. Asset Loading and Scene Management

The modern project uses Addressables and asset-loading APIs that are not available in the Vita-era Unity runtime.

- Adapted scene transitions to use locally packaged scenes through Unity's SceneManager.
- Reworked initialization and local asset references for the legacy engine.
- Preserved the original demo content selection, dialogue flow and gameplay systems.
- Separated desktop-only platform services from the standalone offline demo.
- Implemented local settings and save-data paths.

### 3. Sprite Rendering and Texture Compatibility

Unity's serialized sprite data changed substantially between the original and target engine versions.

- Converted recovered sprite vertex channels and buffers to Unity 2017's layout.
- Restored UV coordinates for more than 1,350 sprites using their original texture transforms.
- Preserved atlas dimensions, sprite geometry, pivots and original pixel-art assets.
- Adapted the Pixel Perfect Camera package to avoid unavailable engine APIs.
- Corrected the resolution selection logic so the Vita's 960 × 544 framebuffer is retained across scene transitions.

The latest sprite and camera changes are still being visually tested.

### 4. Shaders, Spine and Visual Effects

- Restored essential built-in Unity UI and sprite shaders to the build.
- Adapted the base rendering of twelve recovered custom shaders, including Spine and AllIn1SpriteShader materials.
- Reworked premultiplied-alpha handling and import settings for fifty character texture atlases.
- Corrected legacy Spine mesh disposal in the editor.
- Adapted cursor textures and software cursor rendering to eliminate desktop cursor artifacts.

Some recovered shaders contain only simplified placeholder implementations rather than their original shader logic. Advanced lighting, blur, blending and other effects must still be restored or adapted for the Vita's GPU.

### 5. UI and Text Rendering

- Migrated TextMeshPro to a legacy-compatible version.
- Converted recovered font assets and glyph atlases while retaining multilingual text support.
- Restored Unity UI component references and normalized zero-scale Canvas objects.
- Converted modern text alignment and wrapping fields to their Unity 2017 equivalents.
- Preserved the original menus, dialogue boxes, smartphone interface and brewing UI.

### 6. Audio, Video and Controls

- Native OGG Vorbis streaming for music instead of embedding large decoded PCM tracks.
- Streaming for long ambient audio, with smaller mono PCM effects for responsive brewing and smartphone interactions in the latest demo build.
- H.264 introduction videos adapted for native Vita playback.
- Native Vita keyboard integration, gamepad navigation and touchscreen support.
- Right analog stick camera movement independent of UI navigation.

### 7. Performance and Memory

- On-demand loading for selected gallery, character and localization resources.
- Texture compression using Vita-compatible 4-, 8- and 16-bit formats.
- Reduced auxiliary portrait render targets and scheduled camera updates.
- Lower-cost Latte Art fluid simulation while retaining the original gameplay system.
- Bounded audio-source pool and frame-time/memory checkpoints.

These changes target improved stability and smoother gameplay, not a verified locked 60 FPS. Actual performance and visual fidelity remain under hardware testing.

---

## How It Works

```text
Original PC game / demo (Unity 6)
          |
          v
   Asset and scene recovery
          |
          v
   Unity 2017 compatibility layer
   +----------------+----------------+----------------+
   |                |                |                |
   C# / libraries   Sprites / UI     Audio / video    Input / saves
   |                |                |                |
   Legacy APIs      Spine / TMP      Local assets     Vita controls
   +----------------+----------------+----------------+
          |
          v
   Unity 2017.4.10f1 project
          |
          +--> Windows diagnostic build
          |
          +--> PSP2 / IL2CPP target
                        |
                        v
                  PlayStation Vita
```

The intended Vita build runs natively through Unity's PSP2 runtime. It does not emulate Windows, execute the original PC executable or require a PC to stream gameplay.

The Windows diagnostic build is used to isolate asset, serialization and engine compatibility problems before testing them on the handheld.

---

## Screenshots

Screenshots will be added after visual regression testing. Windows development captures and real PlayStation Vita captures will be identified separately.

---

## Controls

The Vita input scheme combines physical controls with the original touch/pointer-based interface.

| Input | Function |
| :--- | :--- |
| D-pad / Left analog stick | UI and ingredient navigation |
| Right analog stick | Camera movement |
| Cross | Confirm / advance dialogue |
| Circle | Back / cancel |
| Touchscreen | Pointer-based interaction |

Context-specific shortcuts and the complete brewing/Latte Art control scheme are still being validated on hardware.

---

## Roadmap

### Demo
- [x] Recover and integrate the original demo scenes.
- [x] Establish Windows compatibility and native PSP2 builds.
- [x] Reach the café and gameplay on real Vita hardware.
- [x] Integrate native OGG music streaming and Vita keyboard.
- [x] Implement texture, audio and memory optimizations.
- [ ] Verify the latest brewing, smartphone and Latte Art fixes on hardware.
- [ ] Complete visual, control, save/load and performance regression tests.
- [ ] Finalize the user-supplied game-data preparation workflow.

### Full game
- [x] Create an independent full-game project and application ID.
- [x] Recover full-game scenes, dialogue, music and assets.
- [x] Adapt gameplay scripts and pass legacy C# diagnostics.
- [x] Convert sprite geometry and font assets.
- [ ] Complete scene and serialized-reference validation.
- [ ] Build and validate the first native full-game VPK.
- [ ] Test the complete campaign, branching, saves and memory usage on Vita.

---

## Building and Installation

Development builds use Unity 2017.4.10f1's native PSP2 / IL2CPP backend and an appropriately licensed PlayStation Vita development environment.

The demo can be built locally as a native VPK. The full game is not yet ready for installation. Check the [Releases](https://github.com/WolffsRoom/CoffeeTalkTokyoVita/releases) page for any publicly available releases; local development builds are not automatically published.

Public build and installation instructions will be added when the compatibility workflow, required user-supplied game data and distribution requirements have been finalized. This repository does not distribute proprietary game assets or licensed SDK components.

---

## Credits

- **The Coffee Talk Tokyo development and publishing teams** — creators of the original game.
- **Toge Productions** — the Coffee Talk series.
- **[Unity](https://unity.com/)** — original engine and legacy runtime.
- **[AssetRipper](https://github.com/AssetRipper/AssetRipper)** — Unity asset analysis and recovery.
- **[Spine / Esoteric Software](https://esotericsoftware.com/)** — skeletal animation technology.
- **Wolff's Room** — backport development and compatibility work.
- The PlayStation Vita homebrew development community.

---

## Legal Notice

Coffee Talk Tokyo, its characters, artwork, music, dialogue, animations and original game code belong to their respective rights holders.

This is an unofficial, non-commercial fan backport, not affiliated with or endorsed by the original developers, publishers, Unity or Sony Interactive Entertainment. The repository is intended for port-specific documentation and redistributable compatibility work only. The original game's proprietary content and third-party licensed components remain subject to their respective licenses.

Please support the official release.
