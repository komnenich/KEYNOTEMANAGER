# LJC Keynote Manager

A browser tool from LJC Design & Engineering for editing Revit keynote files (`.txt`) and checking them against the project specifications and drawing PDFs.

## Features

- **Keynotes:** browse by division, search with `/`, then add, edit, duplicate or delete keynotes. Unpublished changes are listed with per-line revert.
- **Spec check:** choose the spec folder. Section numbers in the file names (`08 7100 - Door Hardware.pdf`, `087100.docx`) are matched to keynote sections. The tool flags sections missing from the specs, specs that have no keynote, and titles that disagree.
- **Drawing check:** choose a folder of drawing PDFs. Keynote tags such as `08 7100.A1` are read from every sheet and checked against the keynote file and the specs.
- **Publish:** in Chrome or Edge, Open file links the shared keynote file. Publish re-reads it, merges other people's edits, asks you to resolve any conflicts, then writes. Other browsers download an updated copy instead.
- The file keeps its original encoding (ANSI, UTF-8 or UTF-16) and line order.

Files are read in the browser and never uploaded. Edits, settings and linked-file permissions are stored only in the browser of the person using the tool.

## Hosting on GitHub Pages

1. Create a repository and add `index.html`, `.nojekyll` and this README to the root.
2. In the repository, open **Settings → Pages**.
3. Under **Build and deployment**, set Source to **Deploy from a branch**, choose `main` and `/ (root)`, then click **Save**.
4. After a minute the site is live at `https://<user-or-org>.github.io/<repo>/`.

GitHub Pages sites are public, even when the repository is private, unless your organization uses GitHub Enterprise Cloud with access control for Pages. The page holds no project data. Each user's keynotes stay on their own computer.

## Requirements

- Chrome or Edge, so Publish can write straight to the linked file. Other modern browsers work in download mode.
- An internet connection. React and the PDF reader (pdf.js) load from cdnjs.cloudflare.com.

## Keyboard

| Key | Action |
| --- | --- |
| `/` | Search |
| `Ctrl S` | Save keynote |
| `Esc` | Close editor |
