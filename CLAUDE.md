# Gemba Walk Tool

Single-page web application for conducting and documenting Gemba Walk inspections on the shop floor.

## Architecture

Everything lives in **`index.html`** — one self-contained file with no build step, no bundler, and no server-side dependencies. It is deployed as a static page (GitHub Pages or any static host).

External CDN dependencies (loaded at runtime):
- **pdf-lib** — PDF generation entirely in the browser
- No other runtime dependencies

## Key Features

- Checklist-based inspection form (6 categories, 24 items)
- Signature capture (canvas)
- Photo attachments with camera / gallery picker
  - Photos are stored as base64 in `localStorage`
  - Each photo shows its sequential number (bottom-right badge) in the UI and in the PDF
- Auto-save to `localStorage` with unsaved-changes guard
- PDF export — A4, embedded photos 2-per-row, footer with page number and timestamp

## Data Flow

All state lives in three module-level variables:
- `photos` — `string[]` of base64 data URLs
- `autosaveTimer` — debounce handle for localStorage writes
- `pdfDownloading` — flag that suppresses the `beforeunload` warning while the PDF file download is in progress

## Development

No build step. Open `index.html` directly in a browser or serve with any static server:

```bash
npx serve .
# or
python3 -m http.server
```

## Deployment

Push to `main` — GitHub Pages picks it up automatically from the repo root.
