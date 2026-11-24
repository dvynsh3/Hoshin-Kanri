# Changelog

All notable changes to **Hoshin Kanri Live**, a single-file HTML tool for running a Hoshin Kanri session live. Newest release first. Release dates are taken from the file timestamps of each saved build.

## Version map

The original build numbers (v1 to v18) map to release numbers as follows.

| Original | Release | Date | File |
|---|---|---|---|
| v18 | v1.2.0 | 2026-10-16 | `Hoshin-Kanri-Live-v1.2.0.html` |
| v17 | v1.1.0 | 2026-10-07 | `Hoshin-Kanri-Live-v1.1.0.html` |
| v16 | v1.0.0 | 2026-09-30 | `Hoshin-Kanri-Live-v1.0.0.html` |
| v15 | v0.15.0 | 2026-09-30 | `Hoshin-Kanri-Live-v0.15.0.html` |
| v14 | v0.14.0 | 2026-09-29 | `Hoshin-Kanri-Live-v0.14.0.html` |
| v13 | v0.13.0 | 2026-09-28 | `Hoshin-Kanri-Live-v0.13.0.html` |
| v12 | v0.12.0 | 2026-09-28 | `Hoshin-Kanri-Live-v0.12.0.html` |
| v11 | v0.11.0 | 2026-09-25 | `Hoshin-Kanri-Live-v0.11.0.html` |
| v10 | v0.10.0 | 2026-09-25 | `Hoshin-Kanri-Live-v0.10.0.html` |
| v9 | v0.9.0 | 2026-09-25 | `Hoshin-Kanri-Live-v0.9.0.html` |
| v8 | v0.8.0 | 2026-09-25 | `Hoshin-Kanri-Live-v0.8.0.html` |
| v7 | v0.7.0 | 2026-09-25 | `Hoshin-Kanri-Live-v0.7.0.html` |
| v6 | v0.6.0 | 2026-09-24 | `Hoshin-Kanri-Live-v0.6.0.html` |
| v5 | v0.5.0 | 2026-09-24 | `Hoshin-Kanri-Live-v0.5.0.html` |
| v4 | v0.4.0 | 2026-09-24 | `Hoshin-Kanri-Live-v0.4.0.html` |
| v3 | v0.3.0 | 2026-09-23 | `Hoshin-Kanri-Live-v0.3.0.html` |
| v2 | v0.2.0 | 2026-09-23 | `Hoshin-Kanri-Live-v0.2.0.html` |
| v1 | v0.1.0 | 2026-09-23 | `Hoshin-Kanri-Live-v0.1.0.html` |

## [v1.2.0] - 2026-10-16
Owners can now be edited from the Full Matrix.

### Added
- **Owners in brackets.** Double-click an initiative and the box shows the title with its owners in brackets, e.g. `Marketing (Amit, Kapil)`. The text before the brackets is the initiative name, the bracketed text is saved as the owners.
- Edit the bracketed text to change owners, delete the brackets to remove them, or clear the whole box to delete the initiative.
- The Matrix hint text explains the bracket format.

### Changed
- Owner changes carry through to the Overview blocks, the Initiative-Wise Details pills, Sankey / Bow-tie / Tabulated, and the Excel and PNG exports.

## [v1.1.0] - 2026-10-07
Tabulated PNG export fixed.

### Fixed
- **Tabulated exported incorrectly.** Each row uses CSS Grid, which html2canvas drops almost entirely. Tabulated is now drawn directly on a canvas: purple header with title and owners, Objectives and Metrics sections with coloured left borders, solid "Strong" and dashed "Medium" pills, and the notes box. Every Initiative-Wise Details export (Sankey, Bow-tie, Tabulated) now bypasses html2canvas.
- Checked against the real workbook's data with a Canvas 2D engine, not just by reading the code.

## [v1.0.0] - 2026-09-30
First stable release. Fixes the all-black Sankey and Bow-tie PNGs from Export all.

### Fixed
- **Sankey and Bow-tie PNGs were 100% solid black** (confirmed by inspecting the pixels of an exported zip). html2canvas renders SVGs styled through CSS classes as blank black. These views no longer use it: the SVG is attached to the real page so styles resolve, then rasterised to a canvas.
- **Notes in exports** are drawn directly on a canvas with manual text wrapping and stacked under the diagram, instead of going through html2canvas.

### Known gaps (fixed in the next build)
- Tabulated PNGs still used html2canvas and exported incorrectly.

## [v0.15.0] - 2026-09-30
Open File fix for the hosted page.

### Fixed
- **File upload not being read correctly.** The File System Access API (`showOpenFilePicker`) and its polling code are replaced with a plain hidden `<input type="file">` triggered by the button, which works reliably inside sandboxed pages. Picking the same file again now works (the input is reset after each selection). Reload now opens the file picker.
- The older build that was still live had kept the permissions-gated path from several iterations earlier, which is why uploads stopped behaving as before.

## [v0.14.0] - 2026-09-29
Export all, notes per initiative, and restoring a saved session.

### Added
- **Export all** button at the right of the top ribbon. Produces one .zip containing the .xlsx, `hoshin-state.json`, and every PNG (Goals, Overview, all three Matrix toggles, and every initiative in all three Initiative-Wise Details views), in numbered folders/filenames matching tab order.
- **Notes box** under the diagram in Initiative-Wise Details: an open text box per initiative that stays the same across Sankey, Bow-tie and Tabulated. It saves as you type (one undo step per editing session) and is appended under the diagram in the single Export .png and in Export all.
- **Restore a saved state.** **Open File** (renamed from Open Excel File) now also accepts the Export all .zip or a raw `.json` and restores the exact data, including notes, IDs and colours. Undo history resets on restore.
- Initiatives carry a `notes` field in the saved state.

### Fixed
- **Full Matrix PNG cut off the centre X cell.** The cell was an inline SVG that html2canvas mis-measured and clipped; it is now drawn directly on a canvas.

## [v0.13.0] - 2026-09-28
Export: .xlsx, .png per view, and a single colour for objectives and metrics in Initiative-Wise Details.

### Added
- **Matrix tab: Export .xlsx** (right-aligned in the toggle row). Writes three sheets in the layout of your *FULL Hoshin Kanri* workbook: **Full Matrix** (real text values, not formulas), **Objective, Initiatives, Metrics** and **Goals, Objectives**. Only titled items are written. Includes the template's header colours, rotated titles, the centre block ("CEO Goals", "Objectives", "Metrics", "Initiatives (Owners)"), the colour scales and 5-quarters icon sets, and keeps the centre block centred when the two sides have different counts.
- **Export .png** on the Matrix tab (current toggle only), and on **Goals**, **Overview** and **Initiative-Wise Details** (only the visual, not the surrounding UI): black background, up to 3× resolution. Overview exports whatever is currently highlighted; Initiative-Wise Details exports the selected initiative's current view.
- Excel and PNG libraries (ExcelJS, html2canvas) load from the internet on first use.

### Changed
- **Initiative-Wise Details colours:** every objective is the same green and every metric the same yellow in Sankey, Bow-tie and Tabulated. The per-item colours remain on the other tabs.
- Excel limits sheet names to 31 characters, so the second sheet is named "Objective, Initiatives, Metrics" (as in your original file) rather than "Objectives, Initiatives, Metrics".
- Goals and initiatives are written in the order the app shows them (goals 5 → 1 top to bottom), not the original sheet's 1 → 5.

## [v0.12.0] - 2026-09-28
Layout and look declared final. Input moves from the Excel file to the page itself: the Full Matrix toggle becomes the single editable surface.

### Added
- **Editable data model.** Goals, objectives, initiatives and metrics now live in the browser with stable IDs. Every other tab and toggle (Goals, Overview, the other Matrix toggles, Initiative-Wise Details) reads from it and updates instantly; nothing else accepts input.
- **Rename in place.** Double-click any goal, objective, initiative or metric title to rename it.
- **Delete by blanking.** Renaming to blank deletes the whole row (goal or initiative) or column (objective or metric), and clears every correlation that referred to it.
- **Click-to-cycle correlations.** Clicking a correlation cell cycles None → Medium → Strong → None.
- **Undo / Redo** buttons above the matrix (history up to 60 steps).
- **White circular "+" buttons on all four sides:** left adds an objective column before all others, right adds a metric column after all others, top adds a goal row before all others, bottom adds an initiative row after all others.
- **Static centre cell.** The X cell has no click handlers.
- **Start from scratch.** The app opens empty with no file loaded, so a session can be built purely with the "+" buttons.

### Changed
- **Excel is now a one-time import.** Open Excel File converts the workbook into the editable model. The 2-second background polling is removed, since it would have overwritten on-page edits. Reload now re-imports the file manually.
- Overview and Matrix hint text updated (click any block to highlight; how to edit).

## [v0.11.0] - 2026-09-25
Hotfix for the trapezoid colour.

### Fixed
- **Trapezoid initiative block was fully black.** The purple fill and outline CSS only targeted `rect`; it now also targets `polygon`, so the trapezoid matches the rectangle.

## [v0.10.0] - 2026-09-25
Clickable objectives and metrics, a pill list for choosing initiatives, and a trapezoid initiative block in the Sankey.

### Added
- **Overview: objective and metric blocks are clickable** like initiatives. Clicking one highlights only the initiatives it links to and the specific link lines between them (not every other link those initiatives have). Everything else dims.
- **Initiative-Wise Details: initiative pills.** The dropdown is removed. A list of pills at the left, outside the visual, shows each initiative's name and owner names. Click one to select it, then use Sankey / Bow-tie / Tabulated for that initiative.
- **Sankey: trapezoid initiative block** with a "Trapezoidal initiative block" checkbox (on by default). The block's left edge height equals the combined thickness of incoming objective bands, and its right edge equals the combined thickness of outgoing metric bands. Untick for a plain rectangle.

### Changed
- **Sankey: owner names** now appear inside the initiative block under the title, as in every other view.

### Fixed
- **Sankey gaps next to the initiative block.** Ribbons now extend 6px into the block and are covered by it, so the seam is flush with no hairline gap.

### Known gaps (fixed in the next build)
- The trapezoid rendered solid black instead of the initiative purple.

## [v0.9.0] - 2026-09-25
Descending order in the two remaining Matrix toggles, matching the Full Matrix you called "absolutely perfect".

### Changed
- **Matrix > Objectives, Initiatives, Metrics** and **Goals, Objectives** list objectives 5 → 1.
- **Matrix > Goals, Objectives** lists goals 5 → 1 top to bottom.

## [v0.8.0] - 2026-09-25
One small usability change.

### Changed
- **Tabs stay frozen on screen while scrolling,** in the same sticky bar as the Open Excel File / Reload now row (the top bar and tab row are wrapped in one sticky container).

## [v0.7.0] - 2026-09-25
Goal rows now sit above the X cell, and a short last row of goals is centred.

### Fixed
- **Full Matrix row order.** The header/cross row was being emitted first; it now sits between the goal rows and the initiative rows, so goals appear above the X cell as specified.
- **Goals tab:** a trailing row with only 1 or 2 goals renders in its own centred flex row, sitting centred under the full 3-card rows above it.

## [v0.6.0] - 2026-09-24
Colour fixes and the Full Matrix laid out in the exact row/column order you specified.

### Changed
- **Metric palette widened** to span red → orange → yellow → lime green (hues 0–115). The previous amber range looked identical.
- **Full Matrix order:** columns run Objective 5 … Objective 1, the X cell, Metric 1 … Metric 5; rows run Goal 5 … Goal 1, the X cell, Initiative 1 … Initiative 5. New goals/objectives are added at the outer end of their side, new initiatives/metrics at the far end of theirs.
- **Full Matrix stays centred.** The X cell sits dead centre however many items each side has: the shorter side is padded with borderless spacer rows/columns, and the whole table is centred in the page.
- **Goals tab:** 3 cards per row instead of 2, each card matching a Tabulated instance (purple header, "Objectives" section label, only objectives listed).

### Fixed
- **"Initiatives" / "Goals" header cells now have a real fill (blue / purple).** A more specific CSS rule (`th.rowlabel`) was overriding the background, so only the text colour had changed in [v0.5.0](#v050---2026-09-24).

### Known gaps (fixed in the next build)
- Goal rows still appeared after the X cell instead of above it, and a last row of 1–2 goals stretched across the grid instead of centring.

## [v0.5.0] - 2026-09-24
Metric colours, dashed Medium pills and the Full Matrix rebuilt as a spreadsheet-style table modelled on your reference image.

### Added
- **Colour-coded links on the metric side.** Metrics get their own palette in a warm hue family while objectives stay in cool hues, so every item is distinguishable but the two sides still read as different groups. This powers coloured links in Overview, Bow-tie, Sankey and Tabulated.
- **Matrix > Full Matrix toggle rebuilt** (no button; renders immediately). One spreadsheet-style table: CEO goal rows with magenta cells and "–" in the metric columns, initiative rows with green objective cells, orange metric cells and a blue name/owner label, and rotated (vertical) objective and metric titles flanking a small X-in-a-square legend labelled Goals / Objectives / Metrics / Initiatives. Rows and columns without a title are trimmed from all sides.

### Changed
- **Medium pills (Goals and Tabulated):** now no fill with a dashed outline and text in the item's colour. Strong stays a solid filled pill. One shared function drives both places.
- **Matrix header cells:** "Initiatives" blue and "Goals" purple. Only the text colour changed in this build; the fill is fixed in [v0.6.0](#v060---2026-09-24).

## [v0.4.0] - 2026-09-24
Colour system, click-to-highlight, tab rename and the first X-matrix attempt.

### Added
- **Overview: clickable initiatives.** Click an initiative and its linked objectives, metrics and links stay as they are while everything else dims (about 15% opacity). Click it again or click empty space to reset.
- **Matrix: third toggle "Goals, Objectives"** showing only the goals × objectives matrix, with colour and dots together.
- **Matrix > Full Matrix toggle replaced** by a **Generate X-Matrix** button that renders a static Hoshin X-matrix: Goals across the top, Objectives down the left and Metrics down the right (rotated text), Initiatives along the bottom, a small hub in the middle labelling the four axes, and the three correlation grids filled with colour and dots. Built as a rectangular approximation, since true X-matrices are drawn on diagonals.

### Changed
- **Tab renamed** from "Full Matrix" to **Matrix**.
- **Objective colours:** the shades of green are replaced by a 15-colour blue / green / yellow / orange / purple / teal palette. Each objective number has one fixed colour, identical on every goal, in Overview, Sankey, Bow-tie and Tabulated.
- **No transparency in Goals and Tabulated.** Strong and Medium pills are a solid colour, differing only by solid vs dashed border. Pills are centred in a fixed-width column instead of pinned to the right edge.
- **Matrix > Objectives, Initiatives, Metrics toggle:** the "Initiatives" label added to the header cell, and cells now show **both** the colour fill and the ● / ◐ dot (dark colour + dot for strong, light colour + half-dot for medium).

## [v0.3.0] - 2026-09-23
Large presentation pass on every tab: Goals restyled, Overview widened, counts and headings added, tab renamed, and the Sankey rebuilt to your reference screenshot.

### Added
- **Overview: strong/medium counts.** A small, muted "3S-2M" label under each initiative block, left edge for objective links and right edge for metric links.
- **Overview: in-diagram headings** "Objectives", "Initiatives" and "Metrics" inside the visual, replacing the legend at the top. Only the Strong / Medium legend remains.
- **Bow-tie: counts and headings.** "3 Strong, 2 Medium" under the Objectives and Metrics headings, plus Objectives / Initiative / Metrics headings inside the visual.

### Changed
- **Initiative blocks:** owner text is the same size as the title, in italics.
- **Goals tab** rebuilt in the Tabulated card style: a purple goal header block with the linked objectives listed below and Strong / Medium badges on the right. Objectives keep one colour across all goals.
- **Overview** stretches to the window width, with wider column spacing so links are distinguishable. Objectives and metrics spread across the full height of the initiative list instead of clumping in the middle.
- **Matrix tab** (still named Full Matrix here): the Full Matrix toggle uses the single consolidated "Full Matrix" sheet. Cells are filled dark (strong) or lighter (medium), all text is centred, and full text is shown (rows grow instead of truncating with "..."). The Objectives, Initiatives, Metrics toggle uses the same table style.
- **Tab renamed** from "Initiative Detail" to **Initiative-Wise Details**.
- **"Text detail" renamed to Tabulated.** Strong items sort above medium ones for both objectives and metrics. Bow-tie also sorts strong to the top and medium to the bottom on both sides.
- **Sankey rebuilt to your reference:** three columns, thin rounded bars for objectives and metrics (strong about 72px, medium about 24px), ribbon opacity 0.5 strong / 0.32 medium, labels outside the bars (left side right-aligned, right side left-aligned), and a wide initiative block with white bold centred label. Ribbons are bezier S-curves coloured by source side, with consistent padding so nothing overlaps.

## [v0.2.0] - 2026-09-23
First round of fixes after real use of the template. Mostly correctness and legibility.

### Changed
- **Initiatives show "Owner 1, Owner 2" under the title** in a smaller font in every diagram.
- **Overview** uses solid lines for strong, dashed lines for medium and no line for none, replacing the translucent flow bands. The legend shows line samples.
- **Matrix > Full Matrix toggle** reads the workbook's "Full Matrix" sheet directly and omits goals, objectives, initiatives and metrics that have no title.
- **Matrix > Objectives, Initiatives, Metrics toggle** shows only titled items. The "Obj 1" placeholders and "(empty)" rows are gone.
- **Initiative Detail > Sankey** now builds true proportional stacked bands (segment thickness = correlation weight) instead of collapsing everything to one point.
- **Initiative Detail > Bow-tie** uses solid lines for strong and dashed lines for medium instead of the translucent sankey-style bands.
- **Initiative Detail > Text detail** shows each objective/metric as a card with a coloured Strong / Medium badge (solid or dashed outline). The progress-style bars are removed.

### Fixed
- **Goals tab empty and owners missing.** The parser now reads every cell by its real Excel address (e.g. `S6`, `T6`) instead of by position in a range-relative table. All 5 goals, all initiatives with owners and every correlation now parse correctly (checked against the real workbook).
- **Oversized, clipped text and odd scaling in all visuals.** SVGs now carry explicit width/height matching their content and only shrink, never stretch. Block text is smaller (12px titles, 9.5px owners) and wraps onto multiple lines instead of being truncated.

## [v0.1.0] - 2026-09-23
First working build: a single self-contained HTML file that turns the filled-in *FULL Hoshin Kanri.xlsx* template into live visuals (the file originally published as a hosted page and then handed over as a downloadable file for the office laptop).

### Added
- **Excel input with live refresh.** An **Open Excel File** button opens any workbook regardless of file name. In Chrome/Edge it keeps a handle to the file on disk and re-reads it every 2 seconds (green pulsing dot = live); in Safari/Firefox it falls back to a normal file picker with a **Reload now** button.
- **Template parsing.** Reads the "Objective, Initiatives, Metrics" and "Goals" sheets by their fixed cell layout (15 objectives, 15 metrics, initiatives with owners, up to 5 goals). The Full Matrix tab is derived from that same data rather than from the sheet's formulas, so it cannot go stale on cached values. Correlation 5 = strong, 2 = medium, 0 = none.
- **Show only titled items.** Any goal, objective, initiative or metric without a title (the template placeholders) is not drawn, so items appear as you add them during the discussion.
- **Four tabs:** Goals, Overview, Full Matrix and Initiative Detail.
- **Goals tab.** Up to 5 CEO goals in a 2 / 2 / 1 grid, each with its linked objectives as chips (solid border = strong, dashed = medium).
- **Overview tab.** Objectives (green), Initiatives (purple-blue, owner underneath) and Metrics (yellow) left to right as blocks, joined by curved flow bands following the correlations. Initiatives with a title but no links are greyed out.
- **Full Matrix tab.** Two scrollable toggles mirroring the workbook: "Full Matrix" and "Objectives, Initiatives, Metrics", with ● (strong) and ◐ (medium) icons.
- **Initiative Detail tab.** A dropdown to pick an initiative and three views: **Sankey** (objectives → initiative → metrics), **Bow-tie**, and **Text detail** (objectives and metrics listed with correlation bars). Every objective and metric has a fixed colour per item number, so it stays the same wherever it repeats.

### Known gaps (fixed in the next build)
- Goals tab showed no goals and initiative owners were missing: cells were read by array position, which was one column off on both sheets ([v0.2.0](#v020---2026-09-23)).
- Text inside diagram blocks was too large and cut off, and the diagrams scaled oddly.
- The app opens on the Goals tab, although the brief asked for Overview as the default view. This is unchanged through [v1.2.0](#v120---2026-10-16).

---

## Supporting files (not release builds)

- *Hoshin_Kanri_Example_Alignment_Gaps.xlsx*: example workbook built on the template (goal: achieve XX revenue by FY end) with deliberate alignment gaps for demonstrating revisions to a team: an orphan objective, an objective with no initiative, an initiative with no objective, an initiative with no metric, an initiative with no links at all, and two orphan metrics. Produced between [v1.1.0](#v110---2026-10-07) and [v1.2.0](#v120---2026-10-16).
- *hoshin-state-ready.json*: a verified copy of a saved state file that loads through Open File.
