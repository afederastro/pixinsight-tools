# Tilt Doctor

Sensor tilt from the stars in your subs.
Version 0.1.5 · Script ▸ FederAstro ▸ Tilt Doctor · Windows, macOS and Linux · Free

## What it does

Tilt Doctor measures every star in your subs and finds where on the sensor the stars are smallest. Without tilt, that
**sharp spot** is the center of the frame. When the sensor is tilted against the focal plane, the sharp spot moves to
one side and the stars on the opposite side grow. Tilt Doctor reports:

- where the sharp spot sits, how far from the center (in mm on the sensor) and in which direction, and how many of
  your subs agree;
- the **corner spread**: how much larger the stars are in the worst corner than in the best one;
- a map of star size across the sensor, with the sub itself underneath, an octagon of the nine region
  medians and a 3 × 3 grid;
- **sessions**: save the results of a set of subs and compare them later, for example before and after adjusting the
  tilt.

It also tells you what it cannot see: a sub focused right where the tilt crosses the center of the frame shows no clear
sharp spot, which is why a night's worth of subs gives a more dependable answer than a single one.

## Workflow

| Part | What you do |
|---|---|
| **Subs** | **+ Files** or **+ Folder** adds FITS or XISF subs and measures them right away (about a second per sub). **+ Folder** includes subfolders and skips WBPP's `calibrated` and `registered` copies and files named as masters, flats, darks or bias. **Active image** measures the image in the active window. Raw (uncalibrated) subs are fine. The list shows each sub's time, filter, number of stars, median star size, corner spread and sharp spot; click a sub to show it on the map. |
| **Star size across the sensor** | *Image* shows the sub underneath, stretched like PixInsight's automatic STF (the file is read again when you click a sub). *Values* writes each star's size next to it; labels that would overlap are skipped. *Stars* shows every measured star colored from smaller (teal) to larger (rust), with contours of the fitted surface every 2 %. *Octagon*: each point sits at a distance from the center proportional to the median star size of its ninth of the frame, so a corner with 7 % larger stars is 7 % further out; without tilt it is regular. *Both* shows stars and octagon. Point at a star to see its HFD, FWHM and position. |
| **Grid and corners** | The median star size in each ninth of the selected sub, and its difference from the center. The worst and best corners are named. |
| **Diagnosis** | The median sharp spot of all subs with a clear one, how many subs agree, and the median corner spread with a grade: under 5 % negligible, 5–10 % slight, 10–20 % noticeable, over 20 % strong. When a saved session is ticked, the diagnosis says how much closer to (or further from) the center the sharp spot is now. |
| **Sharp spot per sub** | The sharp spot of every sub with a clear one, for the current subs and the ticked sessions; rings mark each set's median. |
| **Sessions** | *Save as session* keeps the results of the current subs under a name (not the files). Tick sessions to show them in the chart; the first ticked one is compared in the diagnosis. |
| **Options** | *Star size*: HFD, FWHM or Corner HFD (see below). *Measure*: every sub, or every 2nd, 5th or 10th sub of a folder. *Minimum stars per corner* (default 40): a sub counts toward the results only when each corner of the 3 × 3 grid has at least this many measured stars; others (clouds, haze, a sparse field) are listed as *few corner stars* and left out. |
| **Export report** | Saves a one-page PNG report (setup, diagnosis, the map of the selected sub as shown, grid, sharp spots and up to 30 subs) in the current theme, and a CSV file with every sub next to it. |

> Directions (left, right, above, below) are as the image is displayed in PixInsight, always.

## How it is measured

Each sub is read without opening a window. Stars are found with PixInsight's `StarDetector` and fitted with an
elliptical Moffat PSF (`PSF.fitStars`). Saturated and very faint stars and stars within 30 pixels of the edge are not
used. A color image is measured on its luminance; a raw color (Bayer) frame is measured at half size so its color
pattern does not break the stars up.

| Star size | Meaning |
|---|---|
| **HFD** (default) | Half-flux diameter of every detected star, measured from the pixels around the fitted centroid: the diameter of the circle that holds half the star's light. |
| **FWHM** | Full width at half maximum of the fitted PSF, as SubframeSelector reports it. It reacts more strongly to slight defocus, so its percentages run higher than HFD's. |
| **Corner HFD** | Its own star detection (stars with a signal-to-noise ratio above 30), their half-flux diameter (twice the flux-weighted mean radius over a square aperture), the median of each third of the frame, and tilt = largest minus smallest corner median, in pixels and as a percentage of the median HFD of all stars, with its own grades (none, almost none, mild, moderate, severe, extreme). Values are shown in pixels. The off-axis aberration (stars beyond 75 % of the half-diagonal minus the center) is also given. |

For each sub, star size *S* is fitted across the sensor as *S* = *c* + *g*ₓ*X* + *g*ᵧ*Y* + *q*(*X*² + *Y*²), with *X*,
*Y* in millimeters from the sensor center (from `XPIXSZ`; in pixels when the pixel size is unknown), clipping outliers.
When the stars grow away from one point (*q* > 0) and that point lies on the sensor, it is the sub's sharp spot. The
corner spread is the largest minus the smallest corner median of the 3 × 3 grid, relative to the center.

## Header keywords used

`DATE-OBS`, `FILTER`, `EXPOSURE`/`EXPTIME`, `FOCUSPOS`/`FOCPOS`, `XPIXSZ`/`PIXSIZE1`, `FOCALLEN`, `INSTRUME` and
`BAYERPAT`/`COLORTYP`. Arcseconds are shown when the pixel size and focal length are known.

## Files, network and programs

| What | Where |
|---|---|
| Your options (theme, star size, map view, image and values toggles, minimum stars per corner, folder sampling, last folder) and saved sessions (their results only) | PixInsight's settings, through the standard PJSR `Settings` interface (key `AFederTiltDoctor`) |
| Your image files | Read only; nothing is written to them. Measurements and display images are kept in memory while the window is open |
| Exported report | Only where you choose in a save dialog: a PNG image and a CSV file with the same name |
| Installed files | `src/scripts/AfederAstro/TiltDoctor/` (the script, its signature and its icon) and its page in `doc/scripts/` |

Tilt Doctor does not use the network and runs no external programs.

## Install and remove

PixInsight 1.9.5 or later. Install and update it from the FederAstro repository (see the [README](../README.md#install)).
To remove it, delete the `src/scripts/AfederAstro/TiltDoctor` folder, then use
**Script ▸ Feature Scripts ▸ Regenerate**.

## License

Copyright © 2026 afeder (FederAstro). Tilt Doctor is freeware: you may use it free of charge for any purpose,
including commercial imaging work, change it for your own use, and share unchanged copies free of charge. You may
not sell it, include it in anything sold, or distribute changed copies. It is provided as is, without warranty of
any kind, and the author is not liable for any damage arising from its use. The official copy is in the FederAstro
repository, https://federastro.com/pixinsight/.

## Credits

By afeder (FederAstro), https://federastro.com/.
