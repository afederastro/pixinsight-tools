# Tilt Doctor

Sensor tilt from the stars in your subs.
Version 0.1 · Script ▸ FederAstro ▸ Tilt Doctor · Windows, macOS and Linux · Free

## What it does

Tilt Doctor measures every star in your subs and finds where on the sensor the stars are smallest. Without tilt, that
**sharp spot** is the centre of the frame. When the sensor is tilted against the focal plane, the sharp spot moves to
one side and the stars on the opposite side grow. Tilt Doctor reports:

- where the sharp spot sits, how far from the centre (in mm on the sensor) and in which direction, and how many of
  your subs agree;
- the **corner spread**: how much larger the stars are in the worst corner than in the best one;
- a map of star size across the sensor, with the sub itself underneath, an ASTAP-style octagon of the nine region
  medians and a 3 × 3 grid;
- **sessions**: save the results of a set of subs and compare them later, for example before and after adjusting the
  tilt.

It also tells you what it cannot see: a sub focused right where the tilt crosses the centre of the frame shows no clear
sharp spot, which is why a night's worth of subs gives a more dependable answer than a single one.

## Workflow

| Part | What you do |
|---|---|
| **Subs** | **+ Files** or **+ Folder** adds FITS or XISF subs and measures them right away (about a second per sub). **+ Folder** includes subfolders and skips WBPP's `calibrated` and `registered` copies and files named as masters, flats, darks or bias. **Active image** measures the image in the active window. Raw (uncalibrated) subs are fine. The list shows each sub's time, filter, number of stars, median star size, corner spread and sharp spot; click a sub to show it on the map. |
| **Star size across the sensor** | *Image* shows the sub underneath, stretched like PixInsight's automatic STF (the file is read again when you click a sub). *Values* writes each star's size next to it; labels that would overlap are skipped. *Stars* shows every measured star coloured from smaller (teal) to larger (rust), with contours of the fitted surface every 2 %. *Octagon* is drawn as ASTAP draws it: each point sits at a distance from the centre proportional to the median star size of its ninth of the frame, so a corner with 7 % larger stars is 7 % further out; without tilt it is regular. *Both* shows stars and octagon. Point at a star to see its HFD, FWHM and position. |
| **Grid and corners** | The median star size in each ninth of the selected sub, and its difference from the centre. The worst and best corners are named. |
| **Diagnosis** | The median sharp spot of all subs with a clear one, how many subs agree, and the median corner spread with a grade: under 5 % negligible, 5–10 % slight, 10–20 % noticeable, over 20 % strong. When a saved session is ticked, the diagnosis says how much closer to (or further from) the centre the sharp spot is now. |
| **Sharp spot per sub** | The sharp spot of every sub with a clear one, for the current subs and the ticked sessions; rings mark each set's median. |
| **Sessions** | *Save as session* keeps the results of the current subs under a name (not the files). Tick sessions to show them in the chart; the first ticked one is compared in the diagnosis. |
| **Options** | *Star size*: HFD, FWHM or ASTAP (see below). *Measure*: every sub, or every 2nd, 5th or 10th sub of a folder. *Minimum stars per corner* (default 40): a sub counts toward the results only when each corner of the 3 × 3 grid has at least this many measured stars; others (clouds, haze, a sparse field) are listed as *few corner stars* and left out. |
| **Export report** | Saves a one-page PNG report (setup, diagnosis, the map of the selected sub as shown, grid, sharp spots and up to 30 subs) in the current theme, and a CSV file with every sub next to it. |

> Directions (left, right, above, below) are as the image is displayed in PixInsight, always. ASTAP draws FITS images
> bottom-up, so its top and bottom can be swapped compared with Tilt Doctor; the values and the tilt are the same.

## How it is measured

Each sub is read without opening a window. Stars are found with PixInsight's `StarDetector` and fitted with an
elliptical Moffat PSF (`PSF.fitStars`). Saturated and very faint stars and stars within 30 pixels of the edge are not
used. A colour image is measured on its luminance; a raw colour (Bayer) frame is measured at half size so its colour
pattern does not break the stars up.

| Star size | Meaning |
|---|---|
| **HFD** (default) | Half-flux diameter of every detected star, measured from the pixels around the fitted centroid: the diameter of the circle that holds half the star's light. |
| **FWHM** | Full width at half maximum of the fitted PSF, as SubframeSelector reports it. It reacts more strongly to slight defocus, so its percentages run higher than HFD's. |
| **ASTAP** | Reproduces the tilt measurement of ASTAP's *Image inspection*, so the numbers can be compared with ASTAP's directly: ASTAP's star selection (signal-to-noise ratio above 30), its HFD (twice the flux-weighted mean radius over a square aperture), its median of each third of the frame, and tilt = largest minus smallest corner median, in pixels and as a percentage of the median HFD of all stars, with ASTAP's grades (none, almost none, mild, moderate, severe, extreme). Values are shown in pixels. The off-axis aberration (stars beyond 75 % of the half-diagonal minus the centre) is also given. |

For each sub, star size *S* is fitted across the sensor as *S* = *c* + *g*ₓ*X* + *g*ᵧ*Y* + *q*(*X*² + *Y*²), with *X*,
*Y* in millimetres from the sensor centre (from `XPIXSZ`; in pixels when the pixel size is unknown), clipping outliers.
When the stars grow away from one point (*q* > 0) and that point lies on the sensor, it is the sub's sharp spot. The
corner spread is the largest minus the smallest corner median of the 3 × 3 grid, relative to the centre.

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

Tilt Doctor does not use the network and runs no external programs. ASTAP is not needed or used: its measurement method
is reimplemented inside the script.

## Install and remove

PixInsight 1.9.5 or later. Install and update it from the FederAstro repository (see the [README](../README.md#install)).
To remove it, delete the `src/scripts/AfederAstro/TiltDoctor` folder, then use
**Script ▸ Feature Scripts ▸ Regenerate**.

## Credits

By afeder (FederAstro), https://federastro.com/.

The *ASTAP* star size and the octagon follow the method of [ASTAP](https://www.hnsky.org/astap.htm), the astrometric
stacking program by Han Kleijn, reimplemented from a description of how ASTAP measures tilt; no ASTAP code is
included. Tilt Doctor is not affiliated with ASTAP.
