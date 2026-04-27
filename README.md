# AI Readiness Assessment

A self-contained, printable diagnostic that scores an organisation's readiness to put AI into operations. Answer 15 questions across six dimensions, get a total out of 75, and land in one of three interpretation bands with concrete next steps.

Single HTML file. No build, no dependencies, no backend.

## Running it

Open [index.html](index.html) in any modern browser, or host it as a static asset:

```bash
# quick local preview
python -m http.server 8000
# -> http://localhost:8000/
```

Answers save to `localStorage` (key `nordglade_ai_readiness_v1`) and persist across reloads. The **Reset** button clears them. **Save as PDF** uses the browser print dialog (choose "Save as PDF" as the destination).

## Scoring

| Dimension | Questions | Max |
| --- | --- | --- |
| 01 Problem Clarity | 3 | 15 |
| 02 Process Readiness | 3 | 15 |
| 03 Data & Systems Fit | 2 | 10 |
| 04 Team & Change Capacity | 3 | 15 |
| 05 Governance & Control | 2 | 10 |
| 06 Automation Maturity | 2 | 10 |
| **Total** | **15** | **75** |

Bands:

- **0–25** — Start with one bounded use case.
- **26–51** — Ready for targeted pilots.
- **52–75** — Ready for systematic adoption.

The band on the results page only activates once at least 80% of questions (12 of 15) are answered, so partial fills don't misattribute a band.

## Customising

All content lives in [index.html](index.html). The notable hooks:

- **Dimensions and questions** — the `DIMENSIONS` array in the `<script>` block. Each entry has a title, a max score, an epigraph, and an array of questions with `[label, points]` tuples. Adding or removing questions automatically updates the radar, score table, totals, and band threshold.
- **Bands** — the three `<div class="band">` blocks on the interpretation page. Update thresholds in `renderBandActive()` if you change totals.
- **Table of contents** — the `pages` array in `renderTOC()`. Page numbers are hand-coded; update them if you reorder sections.
- **EU AI Act note** — any dimension can carry a `regnote` property which renders as a boxed callout at the bottom of its page.
- **Branding** — `--accent`, `--paper`, `--ink*` CSS variables in `:root`. The wordmark ("Nordglade") appears in the cover, running footer, and sign-off.

## Privacy and third-party resources

- **Fonts** are loaded from [Bunny Fonts](https://fonts.bunny.net), a GDPR-compliant mirror of Google Fonts that does not log IP addresses. To self-host fully, download the four families (Inter Tight, IBM Plex Mono, IBM Plex Serif) as `woff2` and rewrite the `@font-face` declarations.
- **No analytics, no trackers, no remote scripts.** A `Content-Security-Policy` meta tag blocks everything except inline JS/CSS and the Bunny Fonts origin.
- **Answers stay in the browser.** Nothing is transmitted. Reset wipes local storage for this origin.

## Print layout

Designed for A4 portrait. Each `<section class="page">` fills one page at print time. The three-band interpretation page highlights the reader's current band with a tinted background — print colour adjustment is forced on via `print-color-adjust: exact`.

## Files

- [index.html](index.html) — the entire assessment
- [.gitignore](.gitignore)
- [README.md](README.md)

## Author

Imre Bartis — [imre@nordglade.com](mailto:imre@nordglade.com)
