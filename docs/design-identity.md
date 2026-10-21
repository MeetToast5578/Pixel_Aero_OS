# Pixel Aero — Design Identity v0.1

> **Tagline:** The future, imagined in pixels.  
> **Status:** Design direction, not an implemented feature specification.

## Definition

**Pixel Aero** is a visual design language that fuses **Frutiger Aero's optimistic eco-futurism**, **intentional hand-crafted pixel art**, and **dynamic liquid-glass material effects**.

It imagines a future of computing that remains colorful, tactile, natural, welcoming, and expressive. This design language applies both to **Pixel Aero OS** and potentially to other projects, including game UI.

Pixel Aero is **not** a normal glass UI run through a pixelation filter, nor a static pixel-art illustration of glass.

## Three foundations

1. **Frutiger Aero — Atmosphere:** crystal water, lush green hills, bright skies, white clouds, bubbles, glossy depth, sunlight, friendly futuristic cities and nature woven into technology.
2. **Pixel Art — Structure:** deliberately placed pixels, crisp silhouettes, consistent grid, stepped curves, sprite icons, controlled clusters and highlights. Pixelation is an artistic choice, not a low-resolution defect.
3. **Dynamic Liquid Glass — Material:** real translucency, backdrop-dependent distortion/refraction, responsive highlights, restrained blur and fluid light transitions, bounded by pixel-art silhouettes.

## Defining material: Glass Pixels

**Glass Pixels** is the design term for pixel-structured UI surfaces that retain crisp pixel-art geometry while their interior behaves like dynamic liquid glass.

**Rule: _The glass moves; the pixels stay disciplined._**

- The *frame, corners, interactive structure, icon silhouettes and edge highlights* are deliberately pixel-aligned.
- The *interior glass response* may dynamically transmit, refract and softly blur the changing backdrop.
- Reflections may respond to motion and surrounding light, with pixel-aware styling.
- Motion must remain subtle, responsive and optional; text and controls sit on readable foreground layers.
- Avoid a chunky mosaic of individually embossed cubes, static painted-only glass, and generic smooth glass with a pixel filter pasted over it.
- Do not require every color sample within the glass to become an opaque tile: preserve the feeling of genuinely translucent, fluid material.

This is the **target visual behavior**, not a claim that KWin or a Plasma theme already implements it. The first prototype uses an explicitly provided backdrop; system-wide live backdrop effects require separate compositor integration research.

### Material variations

| Preset | Visual role |
| --- | --- |
| **Aero (default)** | Balanced aqua tint, translucency and legible highlights |
| **Crystal** | Clearer surface, stronger pixel-step rim highlights and sharper reflections |
| **Frost** | More diffused backdrop, calmer motion and maximum readability |
| **Water** | Gently animated aquatic refraction and light ripples |

## Geometry, color and rendering

### Pixel grammar

- Pixel-rounded stepped corners and intentional block silhouettes.
- Pixel-grid-aligned borders, gloss strips, icon art and highlights.
- Design multiple optical sizes instead of automatically stretching tiny icons.
- Avoid blurry pixel sprites; use appropriate nearest-neighbor filtering when raster sprites are scaled.
- The *liquid interior* may interpolate smoothly when needed, but its visual treatment must remain coherent with the surrounding pixel art.
- Prioritize legible typography and accessibility over strict bitmap-font purity.

### Initial color tokens

| Token | Color | Purpose |
| --- | --- | --- |
| Sky | `#BCEEFF` | Light airy surfaces |
| Aqua | `#55C7E8` | Signature glass tint |
| Ocean | `#227FAA` | Focus and saturated elements |
| Meadow | `#A5DB78` | Nature accent |
| Cloud | `#FFFFFF` | Rim highlights and shine |
| Ink | `#28485F` | Text and outlines |

Colors are starting values, not a finalized contrast system. Create tested foreground/background tokens and high-contrast variants.

### Image language

Wallpaper motifs: pixel-art clouds, coastal lakes, waterfalls, futuristic eco-cities, floating glass-and-greenery architecture, sunlight, bubbles and gentle sky reflections.

Use original artwork, with compatible licensing and attribution for any externally sourced assets.

## Interface personality and UX

**Windows practicality + classic macOS refinement, translated into one original visual language.** Avoid shipping direct replicas of proprietary interfaces.

| Component | Direction |
| --- | --- |
| Desktop | Bright pixel-art landscapes and optional subtle ambient motion |
| Top bar | Compact active-app/menu/status surface; graceful menu integration fallback |
| **AeroBar** | Glossy dock/taskbar hybrid with pinned/running apps and window switching |
| Launcher | Fast searchable floating Glass Pixels dashboard |
| Windows | Crisp stepped frame plus live translucent interior, usable window controls |
| File manager | Theme Dolphin first, with clean navigation and pixel-art iconography |
| Widgets | Pixel-glass weather, music, calendar and quick settings |
| Icons | Handcrafted pixel-art sprites with selective glassy highlights |
| Animations | Calm, fluid, purposeful movement; reduced-motion alternative |
| Typography | Pixel-inspired but modern, readable, accessible and internationalized |

Do not let translucent visuals reduce text contrast, obscure controls or interfere with keyboard use.

## Emotional direction

**Feel:** optimistic, nostalgic, refreshing, playful, futuristic, natural, comfortable, lively and approachable.

**Avoid:** sterile flat UI, muddy glass, harsh cyberpunk neon, fake data widgets, excessive skeuomorphism, constant distracting animation, poor contrast, and indiscriminate blur.

The reference fantasy is an **alternate late-2000s future where interfaces continued to become beautiful, expressive and tactile rather than purely flat**.

## OS implementation boundary

Pixel Aero OS is planned as a customization layer and shell for **Fedora KDE Plasma 6** using **Qt 6/QML**, KDE components, original art and—where feasible—**KWin/Wayland effects**.

- Begin with **Glass Pixels Lab**, a runnable prototype using a supplied background image, genuine dynamic effects and pixel-art frames.
- Next produce an installable Plasma theme and modular UI components.
- Evaluate compositor-level backdrop sampling separately; ordinary themes do not freely read arbitrary Wayland surfaces.
- Keep fallbacks for reduced transparency, reduced motion and weaker GPUs.
- Only package a full Linux distribution when the desktop is stable, maintainable and reversible.

## Condensed official definition

> **Pixel Aero is a digital aesthetic and interface design philosophy combining Frutiger Aero, true pixel art, and dynamic liquid-glass materials. It preserves the handcrafted geometry of pixel art while introducing live transparency, refraction, reflection and fluidity through a material language called Glass Pixels. Inspired by the optimistic futures imagined in the 2000s, Pixel Aero celebrates glossy depth, vibrant aquatic color, natural scenery and friendly technology. It is an imagined continuation of a future where digital interfaces stayed colorful, tactile, playful and alive.**
