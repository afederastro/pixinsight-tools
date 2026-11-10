# FederAstro PixInsight tools

Scripts and modules for [PixInsight](https://pixinsight.com/) by afeder ([FederAstro](https://federastro.com/)),
a Certified PixInsight Developer (identifier **afederastro**).

This repository holds the **documentation** and the **issue tracker**. The tools themselves are installed and
updated through PixInsight's own update system from the signed FederAstro repository, so there are no downloads here.

| Tool | Type | Version | Platforms | Find it in PixInsight | Docs |
|---|---|---|---|---|---|
| **Palette Lab** | Module | 0.8.0 | Windows (64-bit), macOS (Apple silicon) | Process ▸ FederAstro ▸ Palette Lab | [docs](docs/PaletteLab.md) |
| **Mask Lab** | Module | 0.1.3 | Windows (64-bit), macOS (Apple silicon) | Process ▸ FederAstro ▸ Mask Lab | [docs](docs/MaskLab.md) |
| **Touch Stretch** | Module | 0.1.1 | Windows (64-bit), macOS (Apple silicon) | Process ▸ FederAstro ▸ Touch Stretch | [docs](docs/TouchStretch.md) |
| **Finderscope** | Module | 0.6.5 | Windows (64-bit), macOS (Apple silicon) | Process ▸ FederAstro ▸ Finderscope | [docs](docs/Finderscope.md) |
| **Acquisition Card** | Script | 0.2.0 | Windows, macOS, Linux | Script ▸ FederAstro ▸ Acquisition Card | [docs](docs/AcquisitionCard.md) |
| **Tilt Doctor** | Script | 0.1.3 | Windows, macOS, Linux | Script ▸ FederAstro ▸ Tilt Doctor | [docs](docs/TiltDoctor.md) |

- **Palette Lab**: 20 built-in narrowband palettes side by side from your Hα, OIII and SII masters (or dual-band
  one-shot colour masters), plus palettes you design yourself; finishes the color and builds the one you like at full
  resolution. A module since 0.8.0 (it was a script before; updating replaces it, see its [docs](docs/PaletteLab.md#now-a-module-080)).
- **Mask Lab**: paint, select and refine masks at full resolution in a window of their own, then apply them to your image.
- **Touch Stretch**: stretch an image by touching it: click a brightness and drag up to bring it out or down to hold
  it back, in a window of its own with a live full-resolution preview.
- **Finderscope**: a dockable panel of icon tiles for every process and script you use, arranged on your own pages,
  plus saved process settings you can apply with one click.
- **Acquisition Card**: builds AstroBin's acquisition CSV and a session summary from the headers of your subs and
  calibration masters, and a card: a picture of the capture to post next to your image.
- **Tilt Doctor**: finds sensor tilt from the size of the stars across your subs: where the sharpest spot sits, how
  much the corners differ, and how that changes between sessions (for example before and after adjusting the tilt).

More about each, with screenshots: [federastro.com/scripts](https://federastro.com/scripts/).

## Install

Add the FederAstro repository to PixInsight once; PixInsight then installs every tool and offers each update automatically.

1. In PixInsight, open **Resources ▸ Updates ▸ Manage Repositories**.
2. Click **Add** and enter `https://federastro.com/pixinsight/`
3. Click **OK**, then **Resources ▸ Updates ▸ Check for Updates**.
4. Apply the update and restart PixInsight when it asks.

Everything in the repository is code-signed with the afederastro developer identity, so PixInsight verifies it before
installing. Each tool's documentation is also built in: select it under FederAstro in the Process Explorer to open its
page in PixInsight's Documentation Browser.

PixInsight 1.9.5 or later is required.

## Report a problem or suggest an idea

[Open an issue](../../issues/new/choose) and pick **Bug report** or **Feature request**. For a bug, the version of the
tool and of PixInsight, your operating system and the text from the Process Console help a lot.

For a security problem, please don't open a public issue: see [SECURITY.md](SECURITY.md).

## Licenses

- **Palette Lab** is free and licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/): not for
  commercial use. Thanks to Franklin Marek ([SetiAstro](https://www.setiastro.com/)), whose Perfect Palette Picker
  inspired it.
- **Acquisition Card** and **Tilt Doctor** are freeware: free for any use, including commercial imaging work. Unchanged
  copies may be shared free of charge, but they may not be sold, and changed copies may not be distributed (full text
  in each tool's doc).
- **Mask Lab**, **Touch Stretch** and **Finderscope** are free to use. Palette Lab, Mask Lab,
  Touch Stretch and Finderscope are based on software
  from the PixInsight project, developed by Pleiades Astrophoto and its contributors (https://pixinsight.com/); Mask Lab
  also contains code ported from [PhotoCraft](https://github.com/storytold/photocraft) under its MIT license (the
  notice is in its documentation).

## Credits

- **Palette Lab**'s Narrowband Blend follows Adam Block's technique for adding a narrowband channel to a color
  image: the stretched channel is colored with one hue, its background is neutralized, and it is screen-blended in.

The documentation in this repository is © afeder (FederAstro).
