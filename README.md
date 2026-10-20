# FederAstro PixInsight tools

Scripts and modules for [PixInsight](https://pixinsight.com/) by afeder ([FederAstro](https://federastro.com/)),
a PixInsight Certified Developer (identifier **afederastro**).

This repository holds the **documentation** and the **issue tracker**. The tools themselves are installed and
updated through PixInsight's own update system from the signed FederAstro repository, so there are no downloads here.

| Tool | Type | Version | Platforms | Find it in PixInsight | Docs |
|---|---|---|---|---|---|
| **Palette Lab** | Script | 0.7 | Windows, macOS, Linux | Script ▸ FederAstro ▸ Palette Lab | [docs](docs/PaletteLab.md) |
| **Mask Lab** | Module | 0.1.0 | Windows (64-bit) | Process ▸ FederAstro ▸ Mask Lab | [docs](docs/MaskLab.md) |
| **Finderscope** | Module | 0.6.2 | Windows (64-bit) | Process ▸ FederAstro ▸ Finderscope | [docs](docs/Finderscope.md) |
| **Acquisition Card** | Script | 0.1 | Windows, macOS, Linux | Script ▸ FederAstro ▸ Acquisition Card | [docs](docs/AcquisitionCard.md) |

- **Palette Lab**: 19 built-in narrowband palettes side by side from your Hα, OIII and SII masters, plus palettes you
  design yourself; finishes the color and builds the one you like at full resolution.
- **Mask Lab**: paint, select and refine masks at full resolution in a window of their own, then apply them to your image.
- **Finderscope**: a dockable panel of icon tiles for every process and script you use, arranged on your own pages,
  plus saved process settings you can apply with one click.
- **Acquisition Card**: builds AstroBin's acquisition CSV and a session summary from the headers of your subs and
  calibration masters.

More about each, with screenshots: [federastro.com/#/scripts](https://federastro.com/#/scripts).

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

- **Palette Lab** is derived in part from Perfect Palette Picker 1.3 by Franklin Marek
  ([SetiAstro](https://www.setiastro.com/)) and is distributed under the same license,
  [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/): free, not for commercial use.
- **Mask Lab**, **Finderscope** and **Acquisition Card** are free to use. Mask Lab and Finderscope are based on software
  from the PixInsight project, developed by Pleiades Astrophoto and its contributors (https://pixinsight.com/); Mask Lab
  also contains code ported from [PhotoCraft](https://github.com/storytold/photocraft) under its MIT license (the
  notice is in its documentation).

The documentation in this repository is © afeder (FederAstro).
