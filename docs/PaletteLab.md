# Palette Lab

A narrowband palette explorer for PixInsight.
Version 0.7.1 · Script ▸ FederAstro ▸ Palette Lab · Windows, macOS and Linux · [CC BY-NC 4.0](#license-and-credits)

## What it does

Palette Lab takes your Hα, OIII and SII images (any two or all three) and shows them rendered in many narrowband
palettes side by side, so you can compare looks before committing to one. Pick a palette, fine-tune it, and build it
at full resolution as a new image.

Built-in palettes: HOO, HOS, HSO, HSS, OHH, OHS, OSH, OSS, SHH, SHO, SOH, SOO, Realistic 1 and 2, Foraxx,
Dynamic Inverse, Dreamsplease, Magma (SHO) and Magma (HOO), plus any custom palettes you make.

## Workflow

The sidebar has four tabs:

| Tab | What you do there |
|---|---|
| **Source** | Choose the Hα, OIII and SII images (auto-detect reads the FITS `FILTER` keyword, then image names), say whether the data is linear, and optionally render thumbnails from a PixInsight preview region. |
| **Adjust** | Channel weights (or AUTO), channel normalization, stretch (median target or Auto STF) and the black-point clip. |
| **Color** | Green removal, saturation, hue shift, selective hue, neutral background, background protection, contrast curve, Hα as luminance and glow. |
| **Output** | Build options, star recombination, NB Blend (blending a colored narrowband channel into a palette image), saving builds to disk, and replace-or-duplicate for rebuilds. |

Click **Generate** to render the gallery. Click a tile for the expanded preview (zoom, 1:1, histogram, pixel readout,
clipping overlay, loupe, before/after, A/B and 4-up compare). Build the palette from there or from the tile.

## Making your own palettes

- **Custom palettes**: write expressions with `{Ha}`, `{OIII}` and `{SII}`, or use the quick mapping builder.
- **Blend** two palettes from the A/B compare view, or make a **variations** grid of hue and saturation.
- **Evolve** breeds six mutations of a palette; pick the best and repeat.
- **Surprise me** makes six random looks.
- **Favorites** (star) and gallery filters help you narrow things down.
- **Export / import** custom palettes and presets as a `.plab` file to share them or move them to another computer.

## Output

- Full-resolution builds open as new image windows. The settings are recorded in the image (FITS HISTORY and a recipe
  that the Build history window can rebuild from).
- Optionally save builds to disk as XISF, TIFF or PNG with a file name pattern.
- Open any palette in PixelMath with its expressions loaded, or save it as a PixelMath process icon file (`.xpsm`).
- Export a contact sheet of the gallery as PNG or JPEG.

## Keyboard

| Key | Action |
|---|---|
| F1 or the **?** button | Help window |
| Ctrl+Z / Ctrl+Y | Undo / redo settings changes |
| Arrow keys | Move through the gallery; previous / next palette in the expanded preview |
| Hold B | Before / after in the expanded preview |

The theme button beside Help switches between the Darkroom (dark) and Paper (light) themes.

## Files, network and programs

| What | Where |
|---|---|
| Your options, custom palettes, presets, favorites, theme, last session and build history | PixInsight's settings, through the standard PJSR `Settings` interface (key `AFederPaletteLab`) |
| Images, `.xpsm` icons, `.plab` exports and contact sheets | Only where you choose in a save dialog |
| Working images while rendering | In memory only (hidden windows named `AFPL_…`, closed when done) |
| Installed files | `src/scripts/AfederAstro/PaletteLab/` (the script, its signature and its icon) and its page in `doc/scripts/` |

Palette Lab does not use the network and does not run external programs. It only uses PixInsight's own processes
(PixelMath, LinearFit, SCNR, IntegerResample, Crop and ChannelExtraction).

## Install and remove

PixInsight 1.9.5 or later. Install and update it from the FederAstro repository (see the [README](../README.md#install)).
To remove it, delete the `src/scripts/AfederAstro/PaletteLab` folder, then use **Script ▸ Feature Scripts ▸ Regenerate**.

## Latest changes (0.7)

- Now installed and updated from the signed FederAstro repository, with its own icon and a page in PixInsight's
  Documentation Browser.
- **Evolve**: breed six variations of any palette, pick the best and evolve again.
- **NB Blend** (the Adam Block method): color a narrowband channel and screen it into a palette image, with live preview.
- Darkroom and Paper themes; clip black point option; neutral background measures only the sky.
- SCNR runs PixInsight's own SCNR process; Cancel stops a render right away.
- Build history window, 4-up compare, `.plab` export and import, filter auto-detect from FITS headers.

The full version history is on [federastro.com](https://federastro.com/#/scripts/palette-lab/changelog).

## License and credits

Palette Lab is derived in part from **Perfect Palette Picker** v1.3 by Franklin Marek
([SetiAstro](https://www.setiastro.com/)), licensed under Creative Commons Attribution-NonCommercial 4.0 International
([CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)). The original code and adapted palette algorithms
remain attributed to their author. Palette Lab is distributed under the same license: it is free, and may not be used
commercially without the rights holder's permission. The Magma and Dreamsplease formulas are community formulas;
credit belongs to their authors.

Interface, workflow and additional features by afeder (FederAstro), https://federastro.com/.
