# Touch Stretch

Stretch an image by touching it: click a brightness and drag.
Version 0.1.1 · Process ▸ FederAstro ▸ Touch Stretch · Windows (64-bit) and macOS (Apple silicon) · Free

![Touch Stretch's split view](https://federastro.com/images/TouchStretch1.webp)

## Getting started

Touch Stretch is a PixInsight module (process `TouchStretch`, category *FederAstro*). It has its own window with the
image inside it, and stays open while you work.

1. Open it with the image you want to stretch in front: it loads the active image. You can pick another one in
   **Image** at the top.
2. Click a part of the image (a faint nebula, say) and drag up. Every pixel of that brightness, anywhere in the image,
   brightens and gains contrast. Drag down to hold a brightness back. Each gesture adds a *stage*.
3. Press **Apply**. The stages run on the image as one step in its history. Touch Stretch stays open, so you can add
   more stages and apply again.

Linear images are shown first with an automatic preview stretch, so you can see where to click; as soon as a stage does
something, the window shows the real result. Nothing changes in PixInsight until you apply.

## Stretching by touch

With the **Stretch** tool (`S`), press on the image: Touch Stretch reads the median brightness of a small area around
the click (25 × 25 pixels of the full-size image). That brightness becomes the stage's *symmetry point*: the stretch is
strongest there and weaker for brightness further away. It is not a local adjustment: every pixel of that brightness
changes together, wherever it is.

- **Drag up** to stretch, **drag down** to unstretch (the inverse curve, for example to hold back a bright core).
  Strength follows the drag; hold Shift for five times finer control.
- **Drag sideways** while dragging to set the stage's *localized intensity*: right concentrates the stretch on the
  clicked brightness, left spreads it out.
- **Grab a stage's square** on the image to change it again.

A stage is centred on a brightness of the *original* image, so it stays anchored when you change the stages before it.

## Stages and fine-tuning

Stages run top to bottom, each on the result of the ones before. Select one in the list (or click its square) to
fine-tune it: **Strength** (the stretch factor ln(D+1)), **Localized intensity** (b), **Symmetry point**, and
**Protect shadows / highlights** (the curve becomes a straight line below or above those levels). **Hide**, **Remove**
(or Delete / Backspace), the arrows and **Clear all** manage the list; **+ Stretch** and **+ Linear** add a stage to set by hand.
Arrow keys nudge the selected stage (Up / Down strength, Left / Right symmetry point; Shift for finer steps).

- **Linear** (`L`): black and white points by touch. Click the sky and drag down to raise the black point; click a
  bright part and drag up to lower the white point. Its **BP** and **WP** handles show on the curve, with how much the
  stage clips.
- **Protect** (`P`, or Alt+click with the Stretch or Linear tool): pins a brightness so every stretch stage keeps the contrast on the far side of it.
  Right-click a marker (or select it and press Delete) to remove it.
- **Magic**: Soft, Medium or Deep make a first stretch from the image's statistics (a black point a few robust sigmas
  below the median, then a stretch that brings the median to a target). The options button sets the target, the black
  point sigma, No black clip, and Linked / Unlinked for colour images.

## The curve

The image's histogram, the histogram after the stages, the overall curve and markers for the stages. Pointing at the
image draws that brightness on the curve with what it becomes. Drag the selected stage's **SP**, **LP**, **HP** (or
**BP**, **WP**) handles along the histogram. **Log** / **Linear** axis, zoom with the wheel or − / +, pan by dragging an
empty spot, **All** for the whole range, **Auto** (or a double-click) to fit the data.

## Colour, masks and viewing

- **Preserve colour** stretches the average of R, G and B and scales the channels alike (with a colour blend);
  **Per channel** stretches each channel with the same curve.
- When the image has an active mask, the preview shows the result through it, as PixInsight will apply it. **Mask**
  tints the protected parts red.
- **Before** / **After** / **Split** (`B`; drag the divider in Split view), **Loupe** (`Z`), Fit (`0`), 1:1 (`1`),
  − / + or the wheel (a double-click on the image fits it); pan with `H`, the middle button or Space. Only the pixels on screen are computed, at full
  resolution.
- **Reset** (the window's bottom bar) clears the stages and puts every setting except the theme back; Undo brings the
  stages back.

## Applying

**Apply** runs the stages on the image as one `TouchStretch` step in its history (Ctrl+Z on the image undoes it),
honouring the image's mask. Drag the triangle at the bottom left of the window to make a process icon of the stages.
Closing the window with unapplied stages asks first.

The process's parameters: a `stages` table (`type`, `channel`, `strength`, `focus`, `level`, `protectShadows`,
`protectHighlights`, `blackPoint`, `whitePoint`, `enabled`), `colourMode` (PreserveColour or PerChannel) and
`colourBlend`.

If Touch Stretch's window (or any process window) looks see-through, turn off PixInsight's
*Edit ▸ Global Preferences ▸ Special GUI Effects ▸ Translucent workspace top-level windows*.

## Files, network and programs

- Settings (theme, colour settings, Magic options, the curve's Auto zoom) are kept in PixInsight's settings through
  the standard PCL interface (module `TouchStretch`).
- Touch Stretch writes no files. No network connections, no external programs, no scripts. Images change only when
  you apply.
- The module is `bin/TouchStretch-pxm.dll` (Windows) or `bin/TouchStretch-pxm.dylib` (macOS, Apple silicon); its
  documentation is in `doc/tools/TouchStretch/`.
- On macOS, use the Cmd key wherever Touch Stretch says Ctrl (Cmd+Z, Cmd+Y), and Option for Alt.

## Acknowledgments

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors
(https://pixinsight.com/). It is built with the PixInsight Class Library (PCL), © 2003-2026 Pleiades Astrophoto S.L.,
used under the PixInsight Class Library License 2.0.

The hyperbolic stretch equations are by David Payne and Mike Cranfield.
