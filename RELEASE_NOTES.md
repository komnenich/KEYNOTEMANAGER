# Keynote Manager: merge Spec check into drawing-based Spec Check

## Commit message

```
Merge Spec check into drawing-based Spec Check tab

- Remove the old file-name-only "Spec check" page; rename "Drawing check" to "Spec Check"
- Add a "Spec folder" panel beside "Drawing folder" (name, file count, scan time, Choose/Rescan)
- Compare keynote tags found on the drawings against spec sections in the chosen folder
- Match keynote keys regardless of spacing (08 71 00.A1 = 087100.A1 = 08 7100.A1)
- Tabs: Not in Spec · Not in keynote file · Matched · All
- Stack cell content vertically (sheets, status chips) so text stays inside its column
- Editor: rename "Spec check" section to "Spec sections"; drop the link to the removed page
```

## Pull request description

### What changed

**Navigation**
- The header has two tabs now: **Keynotes** and **Spec Check**. The old Spec check page, which only compared spec file names with the keynote file, has been removed.

**Spec Check (formerly Drawing check)**
- A **Spec folder** panel sits to the right of **Drawing folder**. It shows the folder name, how many spec files it holds and when it was last scanned, with its own Choose folder and Rescan buttons. The yellow "choose the spec folder" banner was removed, since the panel replaces it.
- The search box moved to its own row under the two panels, and it now also searches spec titles.
- Each keynote tag found on the drawing PDFs is compared with the spec sections in the spec folder:
  - **Not in Spec**: the keynote's section has no spec file.
  - **Not in keynote file**: the tag isn't in the loaded keynote file. This is also shown as an extra label on each row.
  - **Matched**: the section has a spec file.
  - **All**
- Drawing tags are matched to keynote-file keys however the digits are spaced. Before this, a file using `08 71 00.A1` style keys showed every drawing tag as missing.
- Clicking a row opens the matching keynote in the editor.

**Layout**
- Spec Check columns have set widths. Sheet names stack one per line (up to 8, then "+N more"), status labels and the Create keynote button stack vertically, and long keys and text wrap inside their column.

**Editor**
- The "Spec check" section is renamed **Spec sections**, and its "View in Spec check" link (which went to the removed page) is gone.

### Known limitations
- Matching is by section number only. The keynote text isn't compared with the spec title.
- The drawing scan picks up anything shaped like a keynote (`NN NNNN.XX`), so project numbers or section references in notes can show up as tags. Check the Sheets column when a row is both "Not in Spec" and "Not in keynote file".
- `renderSpecPage` and `specData` stay in the code. The editor's Spec sections card still uses `specData`, and `renderSpecPage` is no longer called anywhere.
- The header still reads "Updated Oct 28, 2026".

### Testing
- [ ] Load a keynote file, a drawing folder and a spec folder; check the tab counts look right
- [ ] Check that a keynote file with spaced keys (`08 71 00.A1`) matches tags like `08 7100.A1`
- [ ] Narrow the window below 760px and check the list stays readable
- [ ] Click a matched row and check the editor opens on the right keynote
