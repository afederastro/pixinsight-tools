# Tonight

A quick look at your subs: live while you image, or as an after-action review of subs you already have.
Version 0.1.1 · Process ▸ FederAstro ▸ Tonight · Windows (64-bit) and macOS (Apple silicon) · Free

![Tonight during a live night](https://federastro.com/images/Tonight-live.webp)

## What Tonight is (and isn't)

Tonight is a PixInsight module (process `Tonight`, category *FederAstro*). Open it from
*Process ▸ FederAstro ▸ Tonight*. It has one window that can stay open all night.

It reads your subs, registers each one with PixInsight's own **StarAlignment**, stacks each filter with PixInsight's
own **ImageIntegration** at a reduced size, and shows the stacks, a palette preview, each sub's quality numbers and a
tilt check. You can step through the subs one by one and flag the ones you don't want; Tonight can mark those files so
your preprocessing leaves them out.

> **Note:** Tonight is a **quick look only**. Its stacks are small, uncalibrated and made for viewing. Build your
> masters with your usual preprocessing (for example WeightedBatchPreprocessing), using Tonight's flags to leave out
> the bad subs.

## The start page

![Tonight's start page](https://federastro.com/images/Tonight-start.webp)

Tonight opens on a start page every time you open it, with two choices:

- **Start a live night**: Tonight follows the folder your capture device saves into and adds each sub as it arrives.
- **After-action review**: you choose subs you already have (files, or a whole folder) and Tonight reads them all,
  without watching any folder. Tick **Inspect tilt on every sub** to measure tilt as well (slower); untick it to read
  the subs faster.

**Start page** at the top right of the window shows the start page without ending anything: a night or review still
running is shown there, with **Back to the night** (or **Back to the review**). Starting a new review, or a live night
while a review is open, asks first and then ends the one that is running (see
[what ending removes](#files-network-and-programs)); **Start a live night** during a live night just takes you back to
it. **End the night** / **End the review** end it and return here.

Closing Tonight's window (its close button) ends a night or review that is running, after asking: Tonight does not go
on working behind a closed window. To keep it running out of the way, minimize the window with the button beside the
close button instead (the small bar that is left opens it again). While Tonight is working on a sub (or making its
stacks or the picture), PixInsight neither closes nor opens its window: try again when the step is done.

## A live night

1. After **Start a live night**, a small window asks *Where does your camera save the subs?* Type the folder your
   capture device saves into, or press **...**. It can be a folder on your network, for example the ASIAIR's image
   folder.
2. Choose the stacking size (**1/4**, **1/2** or **Full**): it is fixed for the night. 1/4 is quick and light on disk;
   Full is slow and needs about two sub sizes of disk per sub.
3. Press **Start the night**. The window shrinks into the **Subs from** card at the bottom right, which lights up: that
   is where the night's controls are from then on (the folder, the interval, Add new subs). Tonight adds the subs
   already in the folder, then checks it again at the interval in **Check automatically every** (5 seconds to 60
   minutes, in seconds or minutes). The header shows *Live · checking every minute · next in 0:42*.
4. Untick the automatic check to add subs only when you press **Add new subs** (the header then says
   *Started · add new subs by hand*).

**Start the night** needs a folder that exists (the window says so otherwise). **Not now** closes the small window;
you can choose the folder and press **Start the night** in the Subs from card later.

A file is taken once its size and time have stopped changing (about 20 seconds for the automatic check, 5 for Add new
subs), so a sub still being written or copied is left for the next look. While another process or script runs in
PixInsight, Tonight waits (*Waiting · another process is running*) and goes on when it finishes; a folder check that
falls meanwhile is made a few seconds after it.

For each new sub Tonight reads it, measures its stars and background, checks its tilt, reduces it to the stacking size,
saves a small copy in its work folder, registers it on the night's reference sub and, after a batch of subs, stacks
that filter again. The first sub with enough stars becomes the night's reference (if the first subs are cloudy,
Tonight waits a little for a clearer one); a filter shows its newest sub alone until it has three.

## After-action review

1. On the start page, tick or untick **Inspect tilt on every sub** (remembered).
2. Press **Choose subs...** to pick files (hold Ctrl or Shift for several), or **Choose a folder...** for every sub in
   a folder. A folder's `Flagged` subfolder, if an earlier night or review moved subs there, is read too.
3. Tonight reads the subs one after another, in the order of their file times, with the same steps as a live night.
   The header shows *After-action review · reading 12 of 48*. You can already look around while it reads.
4. When every sub is read, the window switches to the **Subs** view at the first sub, ready to step through with
   ← / → and flag.

- **Add subs...** and **Add a folder...** on the **Subs** card add more subs to the same review.
- Subs flagged before come back flagged: from a name ending in `_FLAG-clouds-trail`, from Tonight's `FLAGGED` keyword
  in the header, or (with **Choose a folder...**) from being in its `Flagged` subfolder (reason *Other* when it has no
  other mark). Loading a review changes no file, except that a sub left half-marked by an interrupted marking is put
  back first (see [Marking the flagged files](#marking-the-flagged-files)).
- A sub that can't be used yet (for example a cloudy one read before the reference sub) is read again after the others,
  twice at most, then listed as left out.
- Without the tilt check, the Tilt card says so and offers **Check tilt now**: once every sub is read, each one is read
  again from its file and measured, in order, about a second each (the header shows
  *checking tilt: 12 of 48 measured*). Subs added later are measured too.

## The window

| Part | What it holds |
|---|---|
| Header | The mode light (Not started, Live, Started, Waiting, After-action review), alerts, and **Start page**. |
| Preview | **Stack** \| **Subs**, the palette or filter shown, the size, zoom, Stretch, Less green and the view's turn; in the Subs view the filter tabs, the Flagged tab and the step row. |
| The night | One mark per sub on a time line, in its filter's color: outlined = flagged, red = left out. Click a mark to review that sub. |
| Filters | One card per stack: a thumbnail, subs × exposure, hours, and what another hour would add. |
| Tilt | The newest sub's tilt (HFD, FWHM or Corner HFD), and every sub's corner spread. **Expand** opens the tilt details. |
| Last sub \| Flagged | The newest sub's stars, star size and background against the night's usual values; or the list of flagged subs with **Mark the files...**. |
| Subs from / Subs | Live: the folder, the automatic check, Start the night, Add new subs. Review: how many subs and from where, Add subs..., Add a folder.... Both: the work folder and its size. |
| Footer | The status line, **Save stacks...**, **Open stacks**, **End the night** / **End the review**. |

## The preview

- The palette menu lists RGB and LRGB (for broadband data), then Palette Lab's palettes: its favorites, its 20
  built-in palettes and your custom ones. **Hα**, **OIII** and **SII** show one stack. A palette waits until the
  filters it needs have stacks; the badge says what is missing.
- **Soft** / **Normal** / **Strong** set the automatic stretch; **Less green** pulls green toward red and blue in a
  palette. These change the picture only, never the stacks.
- **Fit**, **1:1**, − and +, the mouse wheel, and dragging to pan (the hand cursor shows when the picture can move).
  Double-click switches between Fit and 1:1.
- **↻** turns the view by quarter turns. It turns the preview and the tilt map only; files, registration, stacks and
  tilt numbers don't change.

Tonight's palettes use its own copy of Palette Lab's palette formulas, without Palette Lab's finishing steps: they are
a quick look. Palette Lab itself is not needed, and is not changed.

## Filters and cameras

- The filter comes from the `FILTER` keyword, else from the file name: Hα, OIII, SII, L, R, G, B.
- **Color cameras**: a raw color sub (with `BAYERPAT`) is split into color by 2×2 cells (red, the average of the two
  greens, blue), so its full size is half the sensor's. Without a narrowband filter it feeds R, G and B stacks.
- **Duo-band filters** (for example L-eXtreme, L-Ultimate, L-eNhance, ALP-T, NBZ, Askar C1/C2, SV220): Hα (or SII) is
  taken from red and OIII from the average of green and blue, so the narrowband palettes work. SII+OIII filters give
  SII and OIII stacks.
- Subs of different camera angles are registered to the reference sub, so the stacks line up.

## Filters, Last sub and alerts

Each **filter card** estimates what another hour would add to that stack's signal-to-noise (it grows with the square
root of the time), and names the faintest channel, where more time helps most. The **Last sub** card compares the
newest sub's star count, star size and background with the night's usual values for its filter, and draws the star
count of every sub of that filter.

In a live night the header warns when two or more subs in a row are left out; once a filter has at least four subs in
its stack, when a sub has less than half the usual stars (*Clouds?*), or when the last two subs have stars more than
30 % bigger than usual while still having most of the usual stars (*Focus?*).

## The tilt check

![Tonight's tilt details](https://federastro.com/images/Tonight-tilt.webp)

Every sub is measured as it is read, before it is reduced (a raw color sub is measured at half size for HFD and
FWHM), with three methods, as in Tilt Doctor: **HFD** (half-flux diameter), **FWHM** (from a Moffat fit of each star)
and **Corner HFD** (its own detection of the stars with a signal-to-noise ratio above 30, their half-flux diameter and
the median of each ninth of the frame; the tilt is the corner spread relative to the median of all stars, and the
off-axis aberration comes from the outer stars). Switch between them on the Tilt card at any time. The card shows the
newest sub's octagon, its corner spread (green under 10 %, amber under 20 %, red above), where the sharpest spot is,
and a line of every sub's corner spread, so you can see the effect of an adjustment as the next subs come in.

**Expand** opens the tilt details in place of the preview: a list of every measured sub, the star map over the sub
(stars, octagon or both, with contours around the sharp spot), a diagnosis, the sharp spot of every sub, a 3×3 grid
and the corners. Pick a sub in the list to see it; *Show each new sub as it comes in* follows the newest.

Subs are turned to match the sky of the reference sub, but tilt words (left, top, ...) stay in the camera's own frame,
so they don't flip between subs taken at different angles. The tilt check is a diagnosis aid, not a replacement for
Tilt Doctor or AberrationInspector.

## Reviewing subs one by one

![Reviewing subs in Tonight](https://federastro.com/images/Tonight-subs.webp)

Press **Subs** above the preview (or click a mark in the night strip). Each sub is shown aligned on the stack, with a
badge of its numbers against the night's usual values and its flags.

- The tabs choose which subs you step through: **All**, one filter, or **Flagged** (only the flagged subs). The Flagged
  tab also shows in the Stack view once a sub is flagged.
- ← / → or the arrow buttons step; hold Space for a moment, or press **Show the stack** to keep it, to compare the sub
  with its own filter's stack (Flag and the reason keys wait until the sub is shown again).

## Flagging subs

Press **Flag...** (or `F`) for the flag window, or toggle a reason directly with `1`–`9`:

| Key | Reason | Key word |
|---|---|---|
| `1` | Clouds | `clouds` |
| `2` | Tracking / guiding | `tracking` |
| `3` | Satellite / plane trail | `trail` |
| `4` | Excessive tilt | `tilt` |
| `5` | Focus / soft stars | `focus` |
| `6` | Wind / vibration | `wind` |
| `7` | Dew / frost | `dew` |
| `8` | Moon / stray light | `light` |
| `9` | Other | `other` |

**Leave flagged subs out of tonight's stacks** (on by default) takes them out of Tonight's stacks; **Clear flags** puts
a sub back. The Flagged list on the Last sub card shows every flagged sub; click one to review it.

## Marking the flagged files

Tonight can mark a flagged sub's file itself, so you can leave the subs out later in your preprocessing
(WeightedBatchPreprocessing can exclude files by a keyword in the file name or in the header). The bottom of the flag
window, **Mark the sub's file**, sets how and when; the choices are remembered. **By default** (*Now, as I flag*, with
the file name and the keyword ticked) a flagged sub's file is renamed and gets a `FLAGGED` keyword about 1.5 s after
you flag it. Choose *Later* to keep the flags inside Tonight until you press **Mark the files...**. Unticking every way
stops new marks; in *Now* mode it also puts back the files Tonight has already marked (also marks found by a review),
so choose *Later* first if you want those left as they are.

| Way | What changes |
|---|---|
| Reasons in the file name | `..._0014.fit` is renamed `..._0014_FLAG-clouds-trail.fit`. On by default. |
| FLAGGED keyword in the header | A `FLAGGED = 'clouds, trail'` keyword is added to the file's header (FITS: a header card; XISF: a FITSKeyword element). On by default. Only the header changes: the rest of the file is copied byte for byte. |
| Move into a Flagged folder | The file is moved into a folder named `Flagged` next to the subs. |
| Add to the night's list (CSV) | `Tonight-flags-<date and time>.csv` in the subs folder lists every flagged sub: its date and time (`DATE-OBS`, else the sub's time in UTC), filter, file name, folder and reasons. It is written again each time files are marked; after you clear the last flag in *Later* mode, **Mark the files...** writes it again without that sub. |

- **When**: *Now, as I flag* marks the file a moment (1.5 s) after your last change to its flags; *Later* marks nothing
  until you press **Mark the files...** on the Flagged list, which shows the files and the same choices before it
  applies them.
- Clearing a sub's flags (or unticking a way) puts its file back: the original name, no keyword, out of the Flagged
  folder.
- The header is written to a temporary copy (`<name>.tonight-new<ext>`), which is read back and checked byte for byte.
  Just before the swap, again right after the original is renamed out of the way, and once more before the old copy is
  deleted, Tonight checks that the original hasn't changed meanwhile (its header bytes, size and modified time): if
  another program wrote to it, its version is what stays (put back if needed) and the marked copy is deleted. What
  these checks can't see: a change after the header that keeps the size and whose modified time still reads the same
  (file times are compared to the second; a network share may report a changed time late), and a write in the moment
  between the last check and the old copy's deletion. Don't let another program write to a sub while Tonight marks it.
  Then the original is renamed `<name>.tonight-old<ext>`, the copy takes the original's name (with the original's
  modified time, to the second, so the order of the subs by file time stays the same) and the old file is deleted.
- If this is interrupted, the next Start the night or review looks at what was left: with the original gone, the
  `.tonight-old` copy is put back under its name (and an unfinished copy deleted); with the original there, an
  unfinished `.tonight-new` copy is deleted, and a `.tonight-old` copy is kept beside it and reported, for you to check
  and delete.
- Tonight refuses to write a header (and says why) for a read-only file, a FITS file with a `CHECKSUM` or without an
  `END`, a signed XISF file, an XISF file holding more than one image or whose header has no room, a `FLAGGED` keyword
  written by another program, more than one `FLAGGED` keyword, or when a `.tonight-` file of an earlier marking is
  still in the way. The other ways still work.
- Marking waits while another process runs in PixInsight: files flagged meanwhile, and those you apply in
  **Mark the files...**, are marked as soon as it has finished, with the marking choices as they are then (ending the
  night or review is refused until then; an out-of-date list alone: press **Mark the files...** again then).

## Saving and opening the stacks

**Save stacks...** writes each filter's stack, linear and cropped to the area every sub covers, as
`Tonight_<filter>.xisf` (`_2`, `_3`, ... when that name is taken: nothing is overwritten) in a folder you choose (not
the subs folder or the work folder), with `FILTER` and `NCOMBINE` keywords. **Open stacks** opens them as image windows
`Tonight_<filter>`. Remember they are quick-look stacks at the night's stacking size.

## Keys and mouse

| Key or gesture | Does |
|---|---|
| ← / → | Previous / next sub (opens the Subs view) |
| `F` | Flag window |
| `1`–`9` | Toggle a reason on the sub shown |
| Hold Space | The sub's own filter stack instead of the sub |
| Wheel, drag | Zoom at the cursor, pan |
| Double-click | Fit / 1:1 |
| Click the night strip | Review that sub |

The keys work anywhere in Tonight's window, except while you type in a box or move through a list. `F`, `1`–`9` and
Space work in the Subs view; in the Stack view an arrow key opens the Subs view.

## Files, network and programs

| What | Where |
|---|---|
| Your subs | **Read** from the folder or files you choose. They are changed only when flagged subs are marked, in the ways you chose (by default as you flag: renamed, with a `FLAGGED` keyword; optionally moved into a `Flagged` folder next to the subs, which Tonight creates and leaves in place), and put back when you clear the flags. |
| The flag list | `Tonight-flags-<date and time>.csv` in the subs folder (a review: the folder of the first chosen sub, or the one above it if that is a `Flagged` folder), only if you tick *Add to the night's list*. Tonight writes it again at each marking and never deletes it. |
| While a header is written | `<name>.tonight-new<ext>` and `<name>.tonight-old<ext>` next to the sub for a moment (see above). Start the night and choosing review subs look for such files left by an interrupted marking in those folders (and their `Flagged` folders): with the original gone, the `.tonight-old` copy is renamed back (and an unfinished copy deleted); with the original there, an unfinished copy is deleted and an old copy is kept and reported. |
| The work folder | `<system temporary folder>/Tonight/<subs folder name, or "review">-<yyyymmdd-hhmmss>` (with `-2`, `-3`, ... if that name is taken): the night's reference sub and a registered copy of every sub (one per channel for a color sub), 32-bit, about 6.5 MB per sub at 1/4 size for a 26-megapixel camera. Its path and size are shown on the window. **End the night** or **End the review**, closing Tonight's window during one, starting a new review or a live night over it on the start page, and changing the subs folder during a night delete Tonight's files there and the folder, after asking. Quitting PixInsight while a night or review is open removes it too. If PixInsight stops without quitting normally, the folder stays: delete it yourself (the `Tonight` folder in your system's temporary folder). |
| Saved stacks | `Tonight_<filter>.xisf` in the folder you choose, when you press Save stacks. |
| Settings | PixInsight's settings, through the standard PCL settings interface (module `Tonight`): the subs folder, the automatic check (on or off, interval), the stacking size, the palette and view (Palette, Hα, OIII, SII, stretch, Less green, view turn), the tilt method and tilt-details view, Leave flagged subs out, the marking ways and when, and the review choices (Inspect tilt, the last review folder). |
| Palette Lab's settings | **Read only**, for its favorites and custom palettes. |

- **Processes:** Tonight runs PixInsight's own StarAlignment (registration) and ImageIntegration (stacking, its cache
  off) on the copies in its work folder, and PixInsight's PixelMath for some palette previews. It waits while another
  process runs: new subs, stacks made again after a flag, a palette picture whenever it is made (any Palette Lab
  palette, built-in or custom, whatever its name; made once the process has finished) and marking. Tonight's own RGB
  and LRGB pictures, one filter's stack and a sub never run a process, so they don't wait. A process counts as running
  until about 1.5 seconds after PixInsight last showed one, so Tonight does not start its own work at the very end of a
  process or in the short gaps between a script's steps (WBPP's, for example). It opens hidden working image windows
  for a moment and closes them itself.
- **Network:** Tonight makes no network connections of its own and collects no data of any kind. A subs folder on a
  network share is read through the operating system like any other folder.
- **External programs and scripts:** it runs none.
- It does not change the PixInsight installation, nor PixInsight's own settings, repositories or updates.

## Installing and removing

Install it through PixInsight's update system from the FederAstro signed update repository
(https://federastro.com/pixinsight/), or manually with *Process ▸ Modules ▸ Install Modules*. The module is
`bin/Tonight-pxm.dll` (Windows 64-bit) or `bin/Tonight-pxm.dylib` (macOS, Apple silicon); its documentation is in
`doc/tools/Tonight/`.

To remove everything Tonight made: end the night or review (its work folder is deleted), delete the `Tonight` folder in
your system's temporary folder if one is left, delete any `Tonight-flags-*.csv`, empty `Flagged` folders and saved
stacks you no longer want, and clear the flags of any marked subs to put their files back.

Tonight is free for any use.

## Acknowledgments

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors
(https://pixinsight.com/).

Tonight is built with the PixInsight Class Library (PCL), © 2003-2026 Pleiades Astrophoto S.L., used under the
PixInsight Class Library License 2.0. The license's copyright notice, conditions, restriction and disclaimer are
reproduced in `PCL-LICENSE.txt`, distributed with the module's documentation.

The palettes are Palette Lab's, by afeder.
