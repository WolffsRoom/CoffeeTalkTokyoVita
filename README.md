<div align="center">
  <h1>Coffee Talk Tokyo Vita</h1>
  <p>An unofficial native backport of <strong>Coffee Talk Tokyo</strong> for the PlayStation Vita.</p>
  <p>
    <img src="https://img.shields.io/badge/STATUS-WORK_IN_PROGRESS-orange?style=for-the-badge" alt="Work in progress">
    <img src="https://img.shields.io/badge/PLATFORM-PS_VITA-003791?style=for-the-badge&logo=playstation&logoColor=white" alt="PS Vita">
    <img src="https://img.shields.io/badge/UNITY-2017.4.10f1-222222?style=for-the-badge&logo=unity&logoColor=white" alt="Unity 2017.4.10f1">
    <img src="https://img.shields.io/badge/SCOPE-DEMO-yellow?style=for-the-badge" alt="Demo only">
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
> The current scope is exclusively the **Coffee Talk Tokyo PC demo**. Work on the full game is planned as a future development phase, once the demo backport is stable. The full game is not currently supported.
>
> This is an experimental, unofficial fan project, not a finished release. No proprietary game data, decompiled game code, or licensed Unity/PlayStation SDK binaries are distributed by this repository. Obtain the original game from its official source.

---

## Project Status

The backport is currently undergoing compatibility testing on Windows using Unity 2017 before full validation on PlayStation Vita hardware. A smaller proof of concept has already been tested on real hardware; the complete demo project is a separate, more ambitious development effort.

| Component | Status |
| :--- | :--- |
| Unity 6 → Unity 2017 project migration | Implemented; ongoing compatibility work |
| Original demo scenes and gameplay scripts | Recovered and integrated |
| Windows compatibility build | Compiles and launches |
| Language selection, opening logos and main menu | Tested on Windows |
| Opening sequence, dialogue, inventory and brewing | Reached during Windows gameplay tests |
| 960 × 544 display | Validated through the Windows menu transition |
| Sprite UVs, character transparency and text wrapping | Latest fixes implemented; awaiting visual regression tests |
| Custom shader effects | Partial; fidelity improvements ongoing |
| Offline initialization and local save system | Implemented; save/load regression testing pending |
| Native Vita inputs and touch | Initial integration; full validation pending |
| Complete demo VPK | In development |
| Full game | Planned |

The goal is a faithful **1:1 port**, keeping the original gameplay and presentation wherever possible while adapting the implementation to the Vita's hardware and legacy engine.

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

- Repaired malformed recovered audio files and configured streaming for OGG music.
- Adapted splash video audio routing for the legacy player.
- Preserved the original sound and video assets in the local development project.
- Began adapting gamepad input, dialogue advancement and touch support for the Vita.

Audio playback, video decoding, physical controls and touch interaction still require end-to-end testing on the handheld.

---

## How It Works

```text
Original PC demo (Unity 6)
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

The target input scheme combines the original game's pointer-based interactions with physical PlayStation Vita controls and the touchscreen. Dialogue advancement through the Cross button is being integrated.

The final button mapping will be documented after the demo's menus, inventory and brewing interactions have been validated on real hardware.

---

## Roadmap

- [x] Recover and integrate the original demo scenes.
- [x] Establish a working Unity 2017 Windows compatibility build.
- [x] Restore the original startup, language selection and main menu.
- [x] Preserve the Vita's 960 × 544 display resolution.
- [x] Reach dialogue and coffee-brewing gameplay in desktop tests.
- [ ] Complete visual regression tests for sprites, character animations and typography.
- [ ] Restore remaining shader effects and original visual fidelity.
- [ ] Validate all demo dialogue branches, inventory interactions and drink preparation.
- [ ] Verify audio, video, controls and save/load behavior on real hardware.
- [ ] Optimize RAM, VRAM, loading times and frame pacing for the Vita.
- [ ] Complete and test the full demo VPK.
- [ ] Document the installation and user-supplied game-data preparation workflow.
- [ ] Begin adapting the full game.

---

## Building and Installation

The full demo backport is not ready for public installation yet. The intended build target is Unity 2017.4.10f1's PSP2/IL2CPP backend, using an appropriately licensed PlayStation Vita development environment.

Public build and installation instructions will be added when the compatibility workflow, required game data and distribution requirements have been finalized. A complete standalone VPK is not currently available from this repository.

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
