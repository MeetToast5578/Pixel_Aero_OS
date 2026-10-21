# Pixel Aero OS — Development Plan

> **Status:** Planning / pre-alpha  
> **Vision:** *The future, imagined in pixels.*  
> **Initial target:** A fully usable, accessible Pixel Aero desktop customization layer on Fedora KDE Plasma 6.  
> **Long-term target:** A reproducible, installable Linux distribution built around this desktop.

## 1. Vision and design principles

Pixel Aero combines **Frutiger Aero's optimistic eco-futurism**, **genuine pixel-art discipline**, and a carefully considered hybrid of **Windows-style productivity** and **classic macOS elegance**.

The project is **not** a Windows Vista/7 clone, macOS clone, or generic blue transparent theme. It must develop its own recognizable visual identity.

Core principles:
- **True Pixel Aero:** pixel-grid-aligned shapes, sprites, borders, highlights, icons and material patterns; do not simply downscale smooth modern UI.
- **Glass Pixels:** pixel-structured frames, icons and stepped silhouettes containing dynamic liquid-glass interiors with real translucency, backdrop-responsive refraction, reflections and gentle motion. **The glass moves; the pixels stay disciplined.**
- **Bright future:** skies, foliage, lakes, bubbles, sunlight, optimistic technology; avoid cyberpunk gloom and visual clutter.
- **Hybrid usability:** a compact top menu/status bar, a useful bottom AeroBar dock/taskbar, a fast app launcher, responsive window management.
- **Readability first:** clear typography, contrast, keyboard navigation, reduced-motion and reduced-transparency modes.
- **Modern Linux underneath:** preserve real application compatibility, security updates, Wayland support and system integrations.
- **Graceful fallback:** visually demanding effects must be optional; disabling the renderer must never make the desktop unusable.

## 2. Initial platform and architecture

| Layer | Proposed technology | Responsibility |
| --- | --- | --- |
| Base OS | Fedora KDE Spin (current supported release) | Linux packages, hardware, updates, installer |
| Desktop | KDE Plasma 6 | Sessions, panels, widgets, application integration |
| Window compositor | KWin / Wayland | Window management and compositor-integrated effects |
| UI | Qt 6 / QML / KDE Frameworks | Custom shell components and settings |
| Shading prototype | Qt Quick shader tooling + GPU shader pipeline | Test pixel glass with permitted local image sampling |
| Final compositor effects | Supported KWin effects APIs; possibly version-specific native integration | Effects requiring access to composited backdrop |
| Graphics | PNG sprites, pixel-grid SVG where appropriate | Icons, corners, borders, highlights |
| Art tools | Aseprite or LibreSprite | Sprites, textures, cursors |
| Versioning/build | Git, CMake, packaging/CI scripts | Reproducible development and releases |

**Architectural boundary:** an ordinary Plasma theme or QML item cannot freely sample the pixels behind arbitrary Wayland windows. The first Glass Pixels prototype should operate on a known image inside its own window. True desktop-wide backdrop pixelation/refraction is a **separate feasibility milestone**, requiring supported KWin effect integration or a documented fallback. Do not promise universal backdrop sampling from a theme.

**Distribution strategy:** start with a non-destructive KDE package; only build a Fedora-based installable image after the shell works reliably. Do not fork the Linux kernel or rewrite a window manager.

## 3. Pixel Aero visual specification (v0.1)

The complete design identity is documented in [docs/design-identity.md](docs/design-identity.md). Frutiger Aero sets the atmosphere, pixel art defines the geometry, and dynamic liquid glass defines the material response. Avoid both static painted-glass-only art and generic smooth blur with a pixelation filter.

### 3.1 Palette

| Token | Hex | Intended use |
| --- | --- | --- |
| Sky | `#BCEEFF` | Airy light surfaces |
| Aqua | `#55C7E8` | Primary glass tint |
| Ocean | `#227FAA` | Active states and window title bars |
| Meadow | `#A5DB78` | Nature accent |
| Cloud | `#FFFFFF` | Highlights |
| Ink | `#28485F` | Legible text and dark outlines |

Define semantic light/dark tokens and contrast-tested foreground/background pairs instead of hardcoding these colors everywhere.

### 3.2 Pixel system

- Use a **logical design grid** and configurable pixel-art scale (initially 2, 3, 4, 6 and 8 physical pixels per art pixel for experiments).
- Render sprites using nearest-neighbor filtering where crisp detail is intended; verify correct results under fractional display scaling.
- Design primary icon masters at 16×16, 32×32 and 64×64; redraw where necessary rather than blindly scaling.
- Keep borders, stepped corners and highlights aligned to the pixel grid.
- Typography can be pixel-inspired, but must remain readable and internationalized; don't force a tiny bitmap font throughout the system.
- Minimize mixed-resolution assets and accidental smooth antialiasing of *pixel artwork*.

### 3.3 Material family

Four related presets, with the same underlying architecture:

1. **Aero (default):** balanced aqua translucency, light pixel dithering, high readability.
2. **Crystal:** clearer glass, stronger stepped edge highlights, minimal diffusion.
3. **Frost:** more obscured backdrop, better text legibility, subtler reflections.
4. **Water:** carefully restrained wave-like refraction, aquatic tint and small highlights.

Material parameters to expose: `pixelSize`, `tintColor`, `tintStrength`, `backgroundVisibility`, `refractionStrength`, `ditherStrength`, `rimStrength`, `reflectionStrength`, and `motionEnabled`.

The settings shown in early concept art are **art direction**, not implemented functionality.

## 4. Glass Pixels Engine

**Material goal:** a crisp pixel-art shell containing a genuinely dynamic liquid-glass interior. Do not force the whole backdrop into visible checkerboard pixels; controlled liquid translucency is as important as pixel-aligned boundaries.

### 4.1 Visual pipeline (target)

1. Obtain a legal/available background texture (prototype: bundled wallpaper image).
2. Apply a configurable pixel grid to interface geometry and selected material details; preserve enough continuous background information for convincing liquid glass.
3. Add motion-responsive refraction to the available background, with pixel-aware stylization and a controlled distortion strength.
4. Sample the background with an intentional filtering policy: crisp artwork where needed, gentle optical continuity within the transparent glass interior.
5. Apply ordered dithering / quantization selectively rather than indiscriminate noise.
6. Tint with aqua/glass material parameters.
7. Apply pixel-grid-aligned highlight masks, edge rims, inset shadow and restrained shine.
8. Composite legible foreground content on top; avoid distorting text and controls.

A checkerboard overlay is **not** a substitute for refraction. Prove that the material remains distinct over sky, foliage, dark, and busy backgrounds.

### 4.2 Performance and safety

- Prototype with one known image first; measure GPU frame time and memory usage.
- Avoid CPU-based live screenshots of arbitrary windows and avoid polling the screen.
- Target fluid interactions on ordinary integrated graphics; dynamic effects should degrade cleanly.
- Honor reduced-motion, reduced-transparency, power-saving and high-contrast settings.
- Never require unsafe Wayland permission bypasses or private compositor hooks as the default path.
- Validate techniques against the exact installed Qt/Plasma/KWin versions before implementation.

### 4.3 Acceptance tests

- Pixel edge structure remains consistent at 100%, 125%, 150% and 200% display scaling (document compromises).
- Four preset materials have visibly distinguishable effects.
- Text retains legibility on complex wallpapers.
- No visible sprite blur or shimmer during normal window motion.
- Renderer can be disabled without compromising functional navigation.
- Transparent surfaces do not reveal sensitive content beyond normal compositor rules.

## 5. UX design: Windows × classic macOS, but original

### AeroBar (bottom)
A single dock/taskbar hybrid with pinned apps, live running-state indicators, window switching, an optional grouped-window overview, drag-and-drop and a system-safe overflow behavior. Avoid duplicating the same status controls in both bars.

### Top bar
Compact application menus where supported, active app identity, and optionally the clock and system status. If a third-party app does not export global menus, its own menu must remain functional.

### Launcher
Original translucent pixel-glass application launcher with instant keyboard search, favorites, recently opened items and clear system actions. Prefer existing KDE app-launch APIs rather than creating a parallel indexing service.

### Window chrome
Distinctive stepped crystal borders, balanced titlebar depth and clear minimize/maximize/close affordances. Support keyboard shortcuts, touch targets, maximized windows and both light and dark modes.

### Desktop widgets
Weather, music, calendar and quick controls, with permission-conscious integrations and graceful offline states. No decorative widgets that incorrectly imply live data.

### File management
Theme Dolphin and its icons first. A new file manager should **not** be an early milestone; compatibility and accessibility take priority.

## 6. Repository structure (proposed)

```text
Pixel_Aero_OS/
├── README.md
├── plan.md
├── LICENSE                     # choose before importing art/code
├── docs/
│   ├── design-system.md
│   ├── glass-spec.md
│   ├── architecture.md
│   └── compatibility.md
├── assets/
│   ├── icons/
│   ├── cursors/
│   ├── wallpapers/
│   ├── textures/
│   └── sounds/
├── glass-engine/
│   ├── demo/
│   ├── shaders/
│   ├── qml/
│   └── tests/
├── plasma-theme/
│   ├── desktoptheme/
│   ├── colors/
│   └── aurorae/
├── shell/
│   ├── aerobar/
│   ├── launcher/
│   ├── quick-settings/
│   └── widgets/
├── applications/
│   └── aero-settings/
├── packaging/
│   └── fedora/
├── scripts/
└── tests/
```

This is a **source layout**, not a claim that every folder maps directly to a Plasma installation path. Each subproject must document its build and deployment paths.

## 7. Roadmap and completion criteria

### Phase 0 — Research, environment, and references
- [ ] Document exact development versions of Fedora, Plasma, Qt and KWin.
- [ ] Confirm current upstream theming and effect-extension APIs.
- [ ] Choose license(s) for code, original artwork and third-party assets.
- [ ] Capture reference art and categorize it by licensing status.
- [ ] Prepare a development VM or secondary Linux install; record recovery steps.
- [ ] Agree on one pixel grid and typography strategy.

**Done when:** versioned environment guide, design reference board and contribution conventions exist.

### Phase 1 — Standalone Glass Pixels Lab (first coded milestone)
- [ ] Build a runnable Qt 6 / QML demo with a bundled local wallpaper.
- [ ] Display multiple draggable glass panels over that wallpaper.
- [ ] Implement Aero, Crystal, Frost and Water material presets.
- [ ] Expose pixel size, tint, dithering, highlights and refraction sliders.
- [ ] Ensure nearest-neighbor fidelity for pixel-art overlays.
- [ ] Add a comparison scene with busy and quiet backgrounds.
- [ ] Add at least one rendering fallback and basic GPU performance notes.
- [ ] Document how to build/run on the selected Fedora environment.

**Done when:** one command launches the demo, settings visibly affect glass, and screenshots can be reproduced. **Do not claim this is real desktop-wide transparency yet.**

### Phase 2 — Installable Pixel Aero Plasma appearance
- [ ] Create Plasma style assets and metadata compatible with selected Plasma version.
- [ ] Implement color schemes, icon theme skeleton, window decorations and cursor prototypes.
- [ ] Use KDE packaging/install conventions rather than overwriting OS files.
- [ ] Offer uninstall and restore-default instructions.
- [ ] Test GTK/Qt interoperability, scaling, accessibility and dark mode.

**Done when:** users can install/remove the theme on a stock KDE installation without breaking their existing setup.

### Phase 3 — Pixel Aero Shell
- [ ] Build the AeroBar dock/taskbar and launcher as Plasma components.
- [ ] Integrate active windows, virtual desktops, notifications and system tray appropriately.
- [ ] Implement keyboard navigation and fallbacks for unsupported global menus.
- [ ] Add a Pixel Aero settings UI for material presets and effects.
- [ ] Explore KWin effect feasibility separately with benchmark and version matrix.

**Done when:** a tester can log in, launch apps, switch windows, manage files and recover from an effect crash.

### Phase 4 — Visual completeness
- [ ] Handcraft production-quality icons, wallpaper set, cursors and sounds.
- [ ] Make Dolphin, Kate, Konsole and settings visually coherent where possible.
- [ ] Add Daylight, Ocean, Forest and Midnight variants.
- [ ] Audit notifications, dialogs, tooltips, context menus and login experience.
- [ ] Improve performance, contrast, translations and HiDPI support.

**Done when:** major everyday workflows feel cohesive and tests cover visual regressions.

### Phase 5 — Distribution and release
- [ ] Produce reproducible Fedora-compatible packages and a test repository.
- [ ] Validate upgrades, user migration, rollback and uninstall.
- [ ] Build a live-image prototype only after packaging stabilizes.
- [ ] Add CI, release artifacts, issue templates and contributor documentation.
- [ ] Document known limitations and support lifetime.

**Done when:** installation, updating and recovery are reliable on supported hardware.

## 8. First Codex development ticket

**Title:** Build standalone Pixel Aero Glass Pixels Lab v0.1

**Scope:**
- Implement a small, buildable Qt 6/QML desktop demo using CMake.
- Use a locally bundled wallpaper and several sample glass cards, not screen capture.
- Provide four material presets: Aero, Crystal, Frost, Water.
- Provide functional pixel size, tint, dithering, edge highlight and refraction controls.
- Put rendering logic in clearly documented shader/QML components; preserve artwork's pixel grid.
- Include a concise README with verified build instructions and the tested version matrix.
- Include at least one fallback if the shader is unsupported.
- Keep the code modular so future Plasma integration does not require a total rewrite.

**Out of scope:** KWin patching, privileged screen capture, distro ISO generation, replacing Dolphin, authentication, and network services.

**Definition of done:** a developer can check out the repository, install documented dependencies, run the demo, and visually verify every control changes the intended material property.

## 9. Suggested quality gates

- **Usability:** mouse + keyboard operation, meaningful focus indication, stable window management.
- **Visual fidelity:** strict nearest-neighbor pixel-art assets; distinguishable materials and original visual vocabulary.
- **Accessibility:** adjustable effects, readable font scaling, reduced motion and contrast checks.
- **Performance:** measure in a repeatable scene, on integrated graphics as well as higher-end GPUs where possible.
- **Security:** no unnecessary elevated privileges, arbitrary screen capture, unsafe installer scripts or silent desktop replacements.
- **Maintainability:** pinned API compatibility, license attribution, modular code and easy rollback.

## 10. Project risks and mitigations

| Risk | Mitigation |
| --- | --- |
| KWin/Wayland backdrop access is unavailable from ordinary themes | Develop a self-contained glass demo first; isolate compositor work behind a feasibility gate |
| KDE APIs change between releases | Pin supported versions and use the upstream SDK/docs; maintain compatibility matrix |
| Pixel shaders conflict with fractional scaling | Use a logical coordinate system and explicit scale tests |
| Glass destroys text readability | Separate foreground plane; provide Frost/high-contrast/reduced transparency |
| Heavy effects impact battery or GPUs | Benchmark and allow static/fallback rendering |
| Existing theme/icon licenses restrict redistribution | Inventory dependencies and draw original assets where necessary |
| A full distribution creates unsustainable maintenance | Release a theme/package first; consider an image only after maturity |

## 11. Immediate next steps

1. Create `docs/design-system.md` and `docs/glass-spec.md` from this plan.
2. Initialize the Qt/QML demo with CMake and a bundled, licensed or original test wallpaper.
3. Implement pixel-grid sampling, controlled tint and a visible stepped edge.
4. Add ordered dithering, then optional refraction, then four presets.
5. Capture screenshots and iterate on the material before developing the full shell.

---

**Visual principle:** The glass moves; the pixels stay disciplined.

**Project rule:** Be ambitious about the appearance and conservative about desktop stability. Every advanced effect must have a safe, readable fallback.
