# Acquisition Card

AstroBin acquisition details from your headers.
Version 0.1 · Script ▸ FederAstro ▸ Acquisition Card · Windows, macOS and Linux · Free

## What it does

Acquisition Card reads the FITS and XISF headers of your light frames and calibration files (never their pixels) and builds:

- the **acquisition CSV** that AstroBin imports: one row per night, filter, exposure, binning and gain, with the number
  of subs, sensor temperature, dark, flat, flat-dark and bias counts, Bortle, SQM and mean FWHM;
- a **summary** of total integration per filter, equipment and calibration for your image description, as plain text
  or in AstroBin's BBCode.

## Workflow

| Step | What you do |
|---|---|
| **Sources** | **+ Folder** reads a folder of subs and its subfolders. WBPP's `calibrated` and `registered` copies are skipped, and the same frame saved twice (for example a `.fit` and a converted `.xisf`) is counted once. Master darks, flats, flat-darks and bias found there are counted from the frame list PixInsight stores in them, from `StackNN` in ASIAIR file names, or from `NCOMBINE`. **+ Files** adds single files, including a **master light**: its frame list gives the subs that were actually integrated, even if they were deleted. Select a calibration item to correct its type or frame count. |
| **Filters** | AstroBin identifies filters by number. Open your filter in AstroBin's equipment database, copy the page address, select the filter here and paste it (or just the number). It is remembered. |
| **Site & nights** | Bortle and mean SQM are added to every row when given. *Local night* puts a sub taken after midnight on the evening the night began (from the site longitude in the headers); *UTC date* uses `DATE-OBS` as it is. Sensor temperature is the measured `CCD-TEMP` or the cooler set point. |
| **Sessions** | Untick a row to leave it out. Calibration is matched to each session by exposure (darks), filter (flats) and the nearest date. A dark that matches only your flats' exposure is treated as a flat-dark. *Measure FWHM* runs SubframeSelector on a sample of each session's subs (3, 5, 10 or all, spread across the night) and reports the mean in arcseconds; frames with too few stars are left out. |
| **Output** | *Copy* puts the text on the clipboard; paste it into AstroBin (edit the image's acquisition details, then import CSV) or into your description. *Save* writes it to a file you choose. |

> PixInsight scripts have no clipboard function of their own, so *Copy* hands the text to your system's clipboard tool
> (see below). If that tool is missing, the text is selected instead and Ctrl+C copies it.

## Header keywords used

`IMAGETYP`, `DATE-OBS`, `FILTER`, `EXPOSURE`/`EXPTIME`, `XBINNING`, `GAIN`, `OFFSET`, `ISOSPEED`, `CCD-TEMP`,
`SET-TEMP`, `AMBTEMP`, `SITELAT`/`SITELONG`, `OBJECT`, `INSTRUME`, `TELESCOP`, `FOCALLEN`, `XPIXSZ`, `GUIDECAM` and
`CREATOR`/`SWCREATE`, plus the equivalent XISF properties and the processing history of masters. Site coordinates
appear in the summary only if you tick *Include site coordinates*.

## Files, network and programs

| What | Where |
|---|---|
| Your options (filter IDs, Bortle, SQM, date and temperature modes, FWHM sample, theme, last folder, unticked sessions) | PixInsight's settings, through the standard PJSR `Settings` interface (key `AFederAcquisitionCard`) |
| Your image files | Read only; nothing is written to them |
| Saved CSV or summary | Only where you choose in a save dialog |
| FWHM measurement | PixInsight's SubframeSelector process, with its own file cache |
| Copy | A temporary text file in your system's temporary folder, deleted right after copying |
| Installed files | `src/scripts/AfederAstro/AcquisitionCard/` (the script, its signature and its icon) and its page in `doc/scripts/` |

Acquisition Card does not use the network. The only external program it runs is your system's clipboard tool, and only
when you click *Copy*: `clip.exe` on Windows, `pbcopy` on macOS, or the first of `wl-copy`, `xclip` and `xsel` found on
Linux. It also uses PixInsight's own SubframeSelector process.

## Install and remove

PixInsight 1.9.5 or later. Install and update it from the FederAstro repository (see the [README](../README.md#install)).
To remove it, delete the `src/scripts/AfederAstro/AcquisitionCard` folder, then use
**Script ▸ Feature Scripts ▸ Regenerate**.

## Credits

By afeder (FederAstro), https://federastro.com/. AstroBin is a service of its respective owner; this script only
produces text in the format AstroBin's CSV import accepts and is not affiliated with AstroBin.
