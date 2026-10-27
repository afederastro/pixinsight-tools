# Mask Lab

Paint, select and refine masks at full resolution, then apply them to your image.
Version 0.1.1 · Process ▸ FederAstro ▸ Mask Lab · Windows (64-bit) · Free

![Mask Lab's window](https://federastro.com/images/MaskLab1.webp)

## Getting started

Mask Lab is a PixInsight module (process `MaskLab`, category *FederAstro*). It has its own window with the image inside
it, and stays open while you work.

1. Choose the image in **Image** at the top left. Mask Lab starts from the image's current mask (if it has one of the
   same size), or from a black mask.
2. Paint, draw shapes, select by brightness or color, and refine. Everything happens on a working copy: nothing changes
   in PixInsight until you apply.
3. Press **Apply mask** at the bottom right. Mask Lab stays open, so you can keep editing and apply again.

A mask is white where a process should act and black where the image is protected. Mask Lab shows it as a colored
overlay on the image by default.

## Seeing the mask

- **Overlay** (with **Protected** to color the black parts instead, as PixInsight's own overlay does), **Edge** (only
  the 50% outline), **Mask only** and **Image only**. `\` switches between Overlay and Image only.
- The image is shown with its screen stretch (STF). Brightness and color tools use the image *as displayed*, so what
  you see is what they select.
- Zoom with the mouse wheel, `+` `-` `0` (fit) `1` (1:1) or the Zoom tool; pan with Space+drag, the middle button,
  the Pan tool or the Navigator.
- **Preview size** (full, 1/2, 1/4) sets the size slower previews are shown at while you adjust them. Applying always
  works at full size.

## Tools

| Tool | Key | What it does |
|---|---|---|
| Brush / Eraser | B / E | Paint toward white or black: size, hardness, opacity, flow, smoothing. X swaps them. |
| Soften | R | Blurs the mask under the brush. |
| History Brush | Y | Paints an earlier state of the mask back. |
| Refine Edge Brush | D | Paint over an edge; on release the mask inside the stroke is refitted to the image's own edges. |
| Rectangle, Ellipse, Lasso, Points | M, O, L, P | Shapes; the Ellipse and Points stay editable until you apply them. |
| Magnetic Lasso | N | Click on an edge and move along it: the outline snaps to the strongest edge nearby. |
| Gradient | G | Linear or radial ramps. |
| Range, Fill, Color Range | Q, W, C | Select by brightness, by connected area, or by color (color images), with live previews. |
| Pan, Zoom | H, Z | Navigation. |

Brush size: `[` and `]`, or right-drag up and down. Shift+click draws a straight stroke from the last one.

Shapes, gradients and selections **Add** to or **Subtract** from the mask, painted in one of five styles (Solid,
Feathered, Centre gradient, Luminance-protected, Brightness). **Lines** sets the color of outlines and the cursor.

## Refine whole mask

- **Feather**, **Grow**, **Shrink** (previewed live), **Invert**, **Clear**, **From image**.
- **Levels…** and **Curves…** over the mask's histogram.
- **Refine edge…**: makes the mask's edge follow the image (radius, smart radius, smooth, feather, contrast, shift).
- **Stars…**: add a star mask (PixInsight's StarMask) or take the stars out.
- **Combine with image…**: add, subtract, intersect, lighter or darker with any open image of the same size, optionally
  inverted, blended by amount, with a plain-language description of the result.
- **New mask from…** (top bar): black, white, the image's brightness, its own mask as it is now, or a copy of another
  open image. One undoable step.

Every action is a row in **History** (undo, redo, click a row to go back to it).

## Applying the mask

**Apply to**: *The image's mask* (written into its current mask when that is a 32-bit grayscale image of the same
size, otherwise a new mask image is made and attached) or *A new image*. **Cancel** throws away the changes since the
last apply.

## Tip

If Mask Lab's window (or any process window) looks see-through, turn off PixInsight's
*Edit ▸ Global Preferences ▸ Special GUI Effects ▸ Translucent workspace top-level windows*.

## Files, network and programs

- Settings are kept in PixInsight's settings through the standard PCL interface (module `MaskLab`).
- Mask Lab writes no files. Star masks are made with PixInsight's StarMask process in temporary image windows that are
  closed straight away.
- No network connections, no external programs, no scripts. Images change only when you apply.
- The module is `bin/MaskLab-pxm.dll`; its documentation is in `doc/tools/MaskLab/`. Uninstalling the module removes it
  completely.

## Acknowledgments

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors
(https://pixinsight.com/). It is built with the PixInsight Class Library (PCL), © 2003-2026 Pleiades Astrophoto S.L.,
used under the PixInsight Class Library License 2.0.

Refine edge, the Refine Edge Brush, Color Range and the Magnetic Lasso are C++ ports of algorithms from
[PhotoCraft](https://github.com/storytold/photocraft), used under its MIT license (© 2026 ArtCraft Team and the
PhotoCraft contributors); the full notice is in Mask Lab's built-in documentation. The methods behind them: K. He,
J. Sun and X. Tang, *Guided Image Filtering* (ECCV 2010); E. N. Mortensen and W. A. Barrett, *Intelligent Scissors for
Image Composition* (SIGGRAPH 1995). The shape styles follow the mask types of the GAME script for PixInsight.
