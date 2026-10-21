# 🌊 Pixel Aero OS

**The future, imagined in pixels.**

Pixel Aero OS is an open-source project exploring a new Linux desktop aesthetic: **Frutiger Aero meets true pixel art**. Imagine bright skies, sparkling water, optimistic eco-futurism, glossy interfaces, and **Glass Pixels: pixel-structured, dynamic liquid-glass surfaces**—paired with a functional desktop that combines the practical window management of Windows with the elegance of classic macOS.

> **Project status: Planning / pre-alpha.** Pixel Aero OS is not yet an installable operating system. The first goal is a standalone glass-rendering prototype, followed by an installable KDE Plasma theme and desktop shell. A full Linux distribution is a long-term goal.

## ✨ The vision

Pixel Aero is intended to feel like an alternate, brighter future of desktop computing—not a Windows 7 skin, a macOS copy, or just a pixelated wallpaper.

- **True pixel art:** hand-crafted icons, crisp pixel edges, stepped corners, and deliberate highlights.
- **Glass Pixels:** dynamic liquid-glass interiors with true transparency, backdrop-responsive refraction and reflections, bounded by crisp pixel-art silhouettes.
- **Nature meets technology:** clouds, water, sunlight, plants, and friendly futuristic details.
- **A hybrid desktop:** a top menu/status bar, a bottom **AeroBar** dock/taskbar, intuitive application launcher, and excellent window management.
- **Modern computing:** Linux application compatibility, Wayland support, keyboard accessibility, and sensible performance fallbacks.
- **Customization:** planned Aero, Crystal, Frost, and Water glass styles; eventually multiple day/night color themes.

## 🖥️ Planned technology

| Layer | Starting point |
| --- | --- |
| Linux base | Fedora KDE |
| Desktop environment | KDE Plasma 6 |
| UI framework | Qt 6 / QML |
| Compositor | KWin / Wayland |
| Glass experiments | Qt Quick shaders; compositor work investigated separately |
| Artwork | Original pixel-art icons, wallpapers, cursors, and textures |

We will **build on existing Linux technology** rather than create a kernel or window manager from scratch.

### What makes Glass Pixels different?

Pixel Aero combines **pixel-art structure with living glass material**. Frames, silhouettes, icons and stylized highlights remain crisp and deliberate, while interior surfaces respond dynamically to the background through translucency, subtle refraction and reflections. It is neither static painted glass nor a pixelation filter applied to ordinary blur. **The glass moves; the pixels stay disciplined.**

The first implementation will use a local background image in a self-contained demo. Applying true pixelated refraction behind arbitrary application windows on Wayland requires additional compositor-level research and is **not yet implemented**.

## 🛠️ Roadmap

- [ ] **Phase 0 — Foundations:** development environment, design system, licenses, and compatibility decisions.
- [ ] **Phase 1 — Glass Pixels Lab:** runnable Qt/QML demo showcasing Aero, Crystal, Frost, and Water presets.
- [ ] **Phase 2 — Plasma theme:** icons, colors, window decorations, controls, and safe installation/uninstallation.
- [ ] **Phase 3 — Pixel Aero Shell:** AeroBar, launcher, quick settings, widgets, and tested compositor effects where feasible.
- [ ] **Phase 4 — Polish:** cohesive applications, wallpapers, accessibility, scaling, and performance.
- [ ] **Phase 5 — Pixel Aero Linux:** reproducible packages and, eventually, a bootable Fedora-based image.

🎨 **[Read the Pixel Aero design identity](docs/design-identity.md)** for the complete aesthetic, Glass Pixels principles, palette, UX and emotional direction.

📋 **[Read the full development plan](plan.md)** for architecture, milestones, constraints, and the first Codex development ticket.

## 🚀 Getting started

**There is no stable release or installation package yet.** For development, the intended target is a recent supported Fedora KDE installation (preferably on a test machine, separate partition, or virtual machine).

When the first prototype lands, this section will include exact dependencies, build commands, screenshots, and instructions to run it without replacing your existing desktop.

For now, explore [plan.md](plan.md) and follow development in this repository.

## 🎨 Design guidelines

1. Preserve pixel-art geometry; don't merely downscale smooth UI screenshots.
2. Favor aqua blues, ocean colors, bright whites, and natural green accents.
3. Keep text, focus states, and essential controls readable over any glass surface.
4. Make expensive effects adjustable and optional.
5. Favor original visuals over copying proprietary operating-system assets.
6. Keep ordinary Linux desktop use dependable even when visual effects are disabled.

## 🤝 Contributing

The project is in its earliest stage. Design concepts, original pixel-art assets, Qt/QML knowledge, KDE Plasma integration ideas, accessibility feedback, and performance testing are all welcome.

Open an issue to propose an idea or discuss a technical approach. Before submitting third-party graphics or code, confirm that their licenses permit redistribution.

## 📄 License

**To be determined.** A license for source code and appropriate licenses for artwork/assets will be selected before incorporating external contributions or publishing distributable releases. Until then, do not assume that repository contents are licensed for redistribution.

---

**Pixel Aero OS** — *The future, imagined in pixels.* 🌤️
