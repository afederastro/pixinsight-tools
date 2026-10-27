# Finderscope

A panel for launching PixInsight processes, scripts and your own saved process settings. Formerly *afeder Launcher*.
Version 0.6.3 · Process ▸ FederAstro ▸ Finderscope · Windows (64-bit) · Free

## What it does

Finderscope is a PixInsight module (process `Finderscope`, category *FederAstro*). Open it from
**Process ▸ FederAstro ▸ Finderscope**; it stays open while you work. It shows every installed process and every
script in the Script menu as icon tiles:

- **Processes** and **Scripts** pages are built automatically from what is installed.
- **Your pages**: make your own pages with sections and dividers, color their tabs, and arrange tiles by dragging.
- **Pinned** tiles stay at the top of every page; **Recent** shows what you used last; **Most used** lists what you open most.
- **Saved settings**: tiles that open a process with your own parameters, or apply them to an image (see below).
- **Search** by name or acronym; tile sizes from large to icons only; folding sections; numbered workflow steps;
  export and import of your whole layout.

Clicking a tile opens the process, or runs the script, exactly as the Process and Script menus do. The launcher never
runs anything on its own.

## Saved settings

Set up a process window, drag the triangle at its bottom-left onto the workspace to make a process icon, then use
**More ▸ Save settings from process icons**. Each chosen icon becomes a tile. Clicking the tile opens the process with
those parameters; Shift+click, the tile's play button, or dragging the tile onto an image applies them to that image.

Saved settings are stored as **data**: the process name and its parameter values (numbers, true/false, text and
tables). They are never stored or run as code. The launcher's helper script, `FinderscopeHelper.js` (installed with
the launcher and signed with the same developer identity), reads process icons into this data, and creates a process
and sets its parameters from it. It only sets parameters that the process really has, and only to plain values.
Layout files you import are treated the same way: they can only contain data.

Parameters that hold binary data cannot be saved this way and are left at their defaults.

## Files, network and programs

| What | Where |
|---|---|
| Your pages, pins, recent items, tile size, theme and other preferences | PixInsight's settings, through the standard PCL settings interface (module `Finderscope`) |
| Saved settings (one file per tile, plain JSON data) | Windows: `%APPDATA%\Finderscope\saved-settings\` |
| Temporary files while reading process icons or applying saved settings (`finderscope-icons.txt`, `finderscope-settings.json`) | The system temporary folder (on Windows `%TEMP%`); overwritten each time |
| Layout exports | Only where you choose in the save dialog |

- **Network:** the launcher makes no network connections and collects no data of any kind.
- **External programs:** it launches no external programs.
- **Scripts:** it runs the scripts you click (the same scripts as the Script menu, and any you add with **+ Script**),
  and its own helper script for saved settings. PixInsight's security settings apply to all of them.
- It does not change anything in the PixInsight installation, nor PixInsight's own settings, repositories or updates.

## Install and remove

Install it from the FederAstro repository (see the [README](../README.md#install)). The module is
`bin/Finderscope-pxm.dll`; the helper script is `src/scripts/AfederAstro/FinderscopeHelper.js`. To remove everything
the launcher stored outside PixInsight, delete the `Finderscope` folder listed above.

## Latest changes

- **0.6.2**: new icon; script tiles show icons for scripts that keep theirs in PixInsight's icon folder.
- **0.6.0**: renamed from afeder Launcher to Finderscope, now under Process ▸ FederAstro, documentation page in
  PixInsight's Documentation Browser, saved settings stored as plain data and applied by a signed helper script.
- **0.5.0**: first release in the FederAstro repository.

## Acknowledgments

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors
(https://pixinsight.com/). Finderscope is built with the PixInsight Class Library (PCL), © 2003-2026 Pleiades Astrophoto
S.L., used under the PixInsight Class Library License 2.0; the license file is installed with its documentation.
The process icons shown on tiles are PixInsight's own icons, read from the PixInsight installation.
