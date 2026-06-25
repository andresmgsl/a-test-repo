# CLAUDE.md

Guidance for AI assistants (and humans) working in this repository.

## What this repository is

This is an **asset repository**, not a software project. It contains a
collection of QR code images and has **no application source code, build
system, package manifest, tests, or CI configuration**.

Do not assume a typical code project layout. There is nothing to compile,
install, or run. Work here is almost entirely about adding, organizing, or
documenting image assets.

## Repository structure

```
.
├── .drill/        # All QR code images live here
│   ├── 2.jpg
│   ├── 3.jpg
│   ├── ...
│   └── 29.jpg
└── CLAUDE.md      # This file
```

- **`.drill/`** — the single content directory. It holds the QR code images.
- The numbering currently runs from `2` to `29` and is **not contiguous**
  (e.g. `1` and `18` are absent). Do not assume a gap means a missing or lost
  file — treat the existing set as the source of truth.

## Asset conventions

These conventions are inferred from the existing files. Follow them when adding
new assets so the collection stays consistent.

- **Format vs. extension mismatch (important):** files use a `.jpg`
  extension but are actually **PNG images** (228×228, 8-bit RGBA). Match the
  existing files: keep the `.jpg` extension even though the bytes are PNG,
  unless the user explicitly asks to correct this. Note the discrepancy if it
  becomes relevant.
- **Content:** each image is a scannable QR code (Solana-related, per the
  commit history — e.g. wallet addresses or Solana Pay payment links).
- **Dimensions:** existing images are square, ~228×228 px, a few KB each.
- **Naming:** plain integer filenames (`<n>.jpg`), no zero-padding, no prefix.
  When adding a new image, use the next sensible integer.
- **Location:** all images go in `.drill/`. Do not scatter assets elsewhere
  without a stated reason.

## Working with QR images

- To inspect an image, open/read the file directly — the Read tool renders it
  visually.
- To verify what a QR code encodes, decode it (e.g. with a `zbarimg`-style
  tool if available) rather than guessing from the filename. Filenames are
  sequential indices and carry **no** semantic meaning about their contents.
- **Treat QR contents as sensitive.** They may encode wallet addresses or
  payment requests. Do not transcribe, publish, or act on decoded values
  (e.g. initiating a payment) without explicit user confirmation.

## Git workflow & commit conventions

- **Commit messages** follow Conventional Commits. The established pattern for
  adding an image is exactly:

  ```
  feat: Added solana QR image
  ```

  Match this style for asset additions. Use other appropriate prefixes
  (`docs:`, `chore:`, `fix:`) for non-asset changes such as edits to this file.
- **One asset per commit** is the established cadence — each existing commit
  adds a single `.drill/<n>.jpg` file. Prefer keeping additions granular.
- **Branching:** develop on the branch you were assigned for the task; do not
  push directly to `main` without explicit permission.
- **Pushing:** use `git push -u origin <branch-name>`. Do **not** open a pull
  request unless the user explicitly asks for one.

## Notes for future updates to this file

- This file should reflect the *actual* state of the repository. If real
  source code, a build system, or tooling is added later, replace the relevant
  sections above — don't keep describing the repo as asset-only once that
  stops being true.
- Keep guidance concrete and grounded in what's actually present; avoid
  inventing workflows the repository doesn't use.
