# Palette Lab

A narrowband palette explorer for PixInsight.
Version 0.8.0 · Process ▸ FederAstro ▸ Palette Lab · Windows (64-bit) and macOS (Apple silicon) · Free,
[CC BY-NC 4.0](#license-and-credits)

## What it does

Palette Lab takes your Hα, OIII and SII masters (any two or all three, or dual-band one-shot colour masters) and shows
them rendered in many narrowband palettes side by side, so you can compare looks before committing to one. Pick a
palette, fine-tune it, and build it at full resolution as a new image.

Built-in palettes (20): HOO, HOS, HSO, HSS, OHH, OHS, OSH, OSS, SHH, SHO, SOH, SOO, Reef, Forge and Dune (line
colours), Mesa (amber-gold rims and a silvery OIII core, adapted to each target), Foraxx, Dreamsplease, Magma (SHO) and
Magma (HOO), plus any custom palettes you make.

## Now a module (0.8.0)

Since 0.8.0 Palette Lab is a PixInsight module (process `PaletteLab`, category *FederAstro*) instead of a script.

- Open it from **Process ▸ FederAstro ▸ Palette Lab** (it was under Script ▸ FederAstro before).
- Updating removes the old script.
- Custom palettes and presets move over as a `.plab` file: the module reads the script's format. **Before you update,
  open CUSTOM in the script and use EXPORT…** in its Custom Palettes window, then IMPORT… the file in the module
  (importing never overwrites). Favorites, build history, options, theme and the last session don't move over.
- Every full-resolution build is a `PaletteLab` process execution: the instance is in the image's history, so you can
  drag it to a process icon, apply it again, or use it in a process container or a project.
- The module is built for Windows (64-bit) and macOS (Apple silicon) only. On Linux (and Intel Macs) an installed 0.7.6
  script stays where it is but gets no more updates.

## Getting started

1. On **SOURCE**, pick your Hα, OIII and SII masters (or one-shot colour masters, see below), or press
   **AUTO-DETECT**. Tick *Is your data linear?* for linear masters.
2. Press **GENERATE**. The sources are prepared once and every palette is rendered as a thumbnail.
3. Click a tile to build that palette at full resolution: a new image, with the Palette Lab instance in its history.

Thumbnails and full-resolution builds are made from the same prepared sources with the same settings, so what you see
is what you get.

## The sidebar

| Tab | What it holds |
|---|---|
| **SOURCE** | Narrowband and OSC sources, auto-detect, the stretch for linear data (median 0.25, a custom target, or auto STF, with an optional black-point clip), and the preview region: render the thumbnails from a PixInsight preview drawn on a source, at full detail, instead of the whole image. |
| **ADJUST** | Normalization, linear output, channel weights (RESET, AUTO, APPLY), channel statistics and presets (SAVE, DELETE, choose one to apply it). |
| **COLOR** | Neutral background, green removal (SCNR), selective hue, saturation, hue, contrast, glow, protect background and Hα luminance. Changes re-render the thumbnails. |
| **OUTPUT** | Stars, replace previous builds, thumbnail scale, gallery columns, generate scope, save to disk and Narrowband Blend. |

Before rendering, Palette Lab checks the sources: the right kind of image in each picker, the same size, linear and
stretched images not mixed, and that the channels look registered (their stars are compared). Problems are named in the
status line and the Process Console. Palette Lab doesn't register images: run StarAlignment first.

## One-shot colour (OSC) data

Dual-band masters from a colour camera go in the **ONE-SHOT COLOR** pickers on the Source tab, as debayered colour
images:

| Picker | For | Lines it gives |
|---|---|---|
| **OSC HaO3 dual-band** | Hα + OIII filters (L-eXtreme, L-eNhance, NBZ, ALP-T, L-Ultimate and similar; tri- and quad-band filters too) | Hα from red; OIII from the average of green and blue |
| **OSC S2O3 dual-band** | SII + OIII filters | SII from red; OIII from green and blue (averaged with the HaO3 master's OIII when both are set) |

- Use both masters for full SHO palettes from OSC data. With only the HaO3 master it works as with mono Hα and OIII:
  the palettes use Hα where they would use SII, and Magma (SHO) and custom palettes that use `{SII}` are unavailable.
- OSC and mono data mix: a mono image in the Hα, OIII or SII picker always wins over the OSC channel it would replace,
  for example mono Hα with an OSC HaO3 master for OIII.
- Auto-detect finds OSC masters from the `FILTER` keyword or a filter named in the image or file name (HaO3, Ha-OIII,
  L-eXtreme, SiO3, S2O3, SII-OIII and so on).
- With a tri- or quad-band filter, red holds Hα and SII together; Palette Lab uses it as Hα.
- Red comes from a quarter of an OSC camera's pixels (green from half), so Hα and SII from OSC data are usually noisier
  than OIII: noise reduction before Palette Lab helps Hα- and SII-led palettes.

## The gallery

A click on a tile builds it at full resolution; the expand icon opens the preview window; the corner box (or
Ctrl+click) selects it for **BUILD SELECTED**; the star adds a favorite; the cross deletes a custom palette. The wheel
zooms all thumbnails. Filter by favorites, custom palettes or the source channels, page through them and pick 3, 4 or 5
columns. The toolbar also has undo / redo of the settings, **SURPRISE ME**, **CUSTOM**, **EXPORT SHEET** (a PNG or
JPEG contact sheet of the gallery) and **HISTORY**.

## The preview window

Scroll to zoom, drag to pan, double-click to fit, 1:1 for preview pixels at 100%. **HISTOGRAM**, **CLIPPING**
(clipped highlights red, crushed blacks blue), **LOUPE**, a pixel readout, **BEFORE** (or hold B) for the palette
without the COLOR finishing, **A/B COMPARE** with **BLEND**, **4-UP**, **VARIATIONS**, **EVOLVE**, **SAVE .XPSM** (the
palette as a PixelMath process icon), **PIXELMATH** (opens PixelMath with the palette's expressions) and **BUILD FULL
RESOLUTION**. ← / → step through the palettes.

## Making your own palettes

- **Custom palettes**: **CUSTOM** opens the editor: one PixelMath expression per channel, with `{Ha}`, `{OIII}` and
  `{SII}` for the prepared channels (weights and stretch included), and optional symbols. The quick builder writes the
  expressions from percentages of each channel.
- **Blend** two palettes in A/B compare (Mix A); **SAVE AS CUSTOM PALETTE** keeps it.
- **Variations**: a 3 × 3 grid of hue (−20°, 0, +20°) and saturation (0.80, 1.00, 1.30) around a palette. Build one,
  or save it as a custom palette.
- **Surprise me**: six random but sensible looks (weights and mix, hue, saturation, finishing and glow). **SAVE** keeps
  the mix as a custom palette and the finishing as a preset.
- **Evolve**: six small mutations of a palette. Pick the best and evolve again; click an earlier generation to go back.
  **STRENGTH** sets how far children stray; **APPLY** puts the look into the ADJUST and COLOR tabs.
- **Export / import** custom palettes and presets as a `.plab` file to share them or move them to another computer.

## Narrowband Blend

OUTPUT tab, **NARROWBAND BLEND**. Pick a base colour image (for example an HOO palette) and a mono narrowband layer
(for example SII; Palette Lab's prepared channels come first). The layer is coloured (48° gold at 0.90 by default;
GOLD, RED, TEAL and BLUE presets), its background is neutralized, and it is blended in with Screen, Lighten, Add, Soft
light or Overlay at the chosen opacity. Black point, highlights and midtones can be set for both the overlay and the
base. The live preview shows the RESULT, the OVERLAY alone (the sky should be black) or the BASE; **CREATE IMAGE**
blends at full resolution into a new image, with the recipe in its FITS HISTORY. A linear layer gets an automatic STF
stretch.

## Output

- Full-resolution builds open as new image windows (`AFPalette_<palette>`). The settings are recorded in the image:
  FITS HISTORY lines, a `PLRECIPE` recipe and the PaletteLab instance in its history.
- **Save every full-res build** writes each build to a folder as XISF (32-bit float), TIFF or PNG (16-bit), named by a
  pattern with `{target}`, `{palette}`, `{date}` and `{time}`; existing files are never overwritten.
- **HISTORY** lists your builds (and builds found in open images): show a build's window or **REBUILD** it with the
  same palette, weights and finishing.
- Presets keep stretch, normalization, weights, finishing and thumbnail scale. Opened from the process list, Palette
  Lab offers to restore your last session.

## The PaletteLab process

Run globally, an instance makes a new image (`AFPalette_<palette>` unless an output id is set); with *Create new image*
off it replaces the target view (never a source or a preview). Its parameters are the window's settings: the source
view ids, the palette or a custom palette (name, R, G, B, symbols), stretch, normalization, linear output, weights,
every COLOR option, stars and the output id.

## Keyboard

| Key | Where | Does |
|---|---|---|
| ← → ↑ ↓ | Gallery | Move the cursor |
| Enter | Gallery | Build the palette under the cursor |
| Space | Gallery | Open its preview |
| S / X / E | Gallery | Star / select / evolve it |
| Ctrl+Z / Ctrl+Y | Window | Undo / redo settings changes |
| F1 or the **?** button | Window | Help |
| ← →, hold B | Preview | Previous / next palette; before / after |

On macOS, use Cmd wherever Palette Lab says Ctrl. The theme button beside Help switches between the Darkroom (dark) and
Paper (light) themes.

## Files, network and programs

| What | Where |
|---|---|
| Your options, custom palettes, presets, favorites, theme, last session and build history | PixInsight's settings, through the standard PCL interface (module `PaletteLab`) |
| Images, `.xpsm` icons, `.plab` exports and contact sheets | Only where you choose (a save dialog, or the save-to-disk folder) |
| Working images while rendering | In memory only (hidden windows named `AFPL_…`, closed when done) |
| Installed files | `bin/PaletteLab-pxm.dll` (Windows) or `bin/PaletteLab-pxm.dylib` (macOS) with its signature (`.xsgn`), and its page and the PCL license in `doc/tools/PaletteLab/` |

Palette Lab does not use the network and does not run external programs. It only uses PixInsight's own processes
(PixelMath, LinearFit, SCNR, IntegerResample and ChannelExtraction) and PCL's star detector (for the registration
check).

## Install and remove

PixInsight 1.9.5 or later. Install and update it from the FederAstro repository (see the [README](../README.md#install)).
To remove it, uninstall the module (**Process ▸ Modules ▸ Uninstall Modules**).

## Latest changes

- **0.8.0**:
  - Palette Lab is now a native PixInsight module for Windows and macOS (Apple silicon); builds are PaletteLab process
    executions you can reuse; the window opens wide, fitted to your screen; NB Blend is now **Narrowband Blend**.
  - Generate checks the sources first: different sizes, an un-debayered (CFA) image or a colour image in a line picker
    stop with a message; images that don't look registered, or linear and stretched images mixed, give a warning.
  - The line pickers list mono images only and the OSC pickers colour images only; auto-detect also finds dual-band
    OSC masters from the `FILTER` keyword and image or file names.
  - Hα as luminance starts at 0.30 (was 1.0); Mesa's gold rims are adjusted.
- **0.7**: Evolve, Narrowband Blend, Darkroom and Paper themes, Reef, Forge, Dune and Mesa, build history, 4-up
  compare, `.plab` export and import, filter auto-detect from FITS headers.

The full version history is on [federastro.com](https://federastro.com/#/scripts/palette-lab/changelog).

## License and credits

Palette Lab by afeder (FederAstro), https://federastro.com/. It is free and licensed under Creative Commons
Attribution-NonCommercial 4.0 International ([CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)): it may
not be used commercially without permission. The Foraxx, Magma and Dreamsplease formulas are community formulas; credit
belongs to their authors. Narrowband Blend follows Adam Block's technique (see the [README](../README.md#credits)).

Thanks to Franklin Marek ([SetiAstro](https://www.setiastro.com/)), whose **Perfect Palette Picker** inspired Palette
Lab.

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors
(https://pixinsight.com/). It is built with the PixInsight Class Library (PCL), © 2003-2026 Pleiades Astrophoto S.L.,
used under the PixInsight Class Library License 2.0.
