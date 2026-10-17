# Google AI Studio — Universal App Builder Guide

An interactive, multilingual, accessible single-page tutorial that teaches students, seniors, entrepreneurs and non-coders how to **build any non-AI app in Google AI Studio's Build mode** — from first idea to a published app.

The whole app ships as **one self-contained HTML file** (React, Tailwind CSS, all content and images inlined). No build step, no server, no backend.

---

## Table of contents

- [Features](#features)
- [Tutorial content](#tutorial-content)
- [Quick start](#quick-start)
- [Usage](#usage)
- [Download the printable guide](#download-the-printable-guide)
- [Printing and PDF export](#printing-and-pdf-export)
- [Accessibility](#accessibility)
- [Tech stack](#tech-stack)
- [Project structure](#project-structure)
- [Customization notes](#customization-notes)
- [Deployment](#deployment)
- [Browser support](#browser-support)
- [Known limitations](#known-limitations)
- [Contributing](#contributing)
- [Disclaimer](#disclaimer)
- [License](#license)

---

## Features

- **12 hands-on modules** (Module 0–11) covering the full journey from introduction to deployment.
- **Three languages:** English (EN), Chinese (ZH) and Malay (BM), switchable instantly from the header.
- **Interactive progress tracking:** a checklist in every module, with a live progress ring and percentage in the sidebar.
- **Live search** across all modules (press `/` to focus the search box, `Esc` to leave it).
- **Copy-to-clipboard** buttons for prompts, templates, code examples and copyable snippets.
- **Prompt library:** ready-made non-AI app prompt templates built on the universal formula.
- **Tables, callouts, FAQs, tips and screenshots** (each image is labelled *real* or *illustrative*), with a click-to-expand image viewer.
- **Accessibility controls:** font size (A− / A / A+), high-contrast mode and dyslexia-friendly mode.
- **One-click printable guide:** the **Download** button exports the entire guide in the current language as one plain, accessible HTML page.
- **Back-to-top button** at the end of every chapter in the downloaded guide (works in the browser and in the saved PDF).
- **Print-optimized layout** for Letter and A4 portrait with no large blank areas.

## Tutorial content

| # | Module |
|---|--------|
| 0 | Introduction — What is Google AI Studio Build? |
| 1 | Prerequisites & Model Selection — What You Actually Need |
| 2 | Accessing Google AI Studio — First Open |
| 3 | Anatomy of the Build Interface — 4 Panels |
| 4 | Prompt Engineering Formula for ANY Non-AI App |
| 5 | Building Your First App — Inventory Manager Hands-On |
| 6 | Iterating & Refining — Talk to Your App |
| 7 | Understanding Generated Code — React + TypeScript |
| 8 | Testing & Debugging — When Preview Fails |
| 9 | Export & Local Development + Android Build |
| 10 | Deployment & Sharing — Go Live in One Click |
| 11 | Accessibility, Best Practices, FAQ & Next Steps |

The core teaching device is the **universal prompt formula**:

```
APP TYPE + CORE FEATURES + UI STYLE + DATA MODEL + RULES
```

Tip: end prompts with *"no AI, localStorage only, validation"* to keep generated apps simple and offline-friendly.

## Quick start

No installation is required.

```bash
# 1. Clone the repository
git clone https://github.com/hockchiyeer/ai-studio-build-guide.git
cd <your-repo>

# 2. Open the app
#    Option A: double-click the HTML file, or
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows

#    Option B: serve it locally
python3 -m http.server 8000
# then visit http://localhost:8000/index.html
```

> Tip: rename the file to `index.html` if you plan to host it on GitHub Pages or another static host.

An internet connection is only needed for Google Fonts (Inter, Noto Sans, Noto Sans SC). If the fonts cannot load, the app falls back to system fonts.

## Usage

| Action | How |
|--------|-----|
| Switch language | EN / ZH / BM toggle in the header |
| Jump to a module | Click it in the left sidebar |
| Search | Type in the sidebar search box, or press `/` |
| Clear / leave search | `Esc` |
| Track progress | Tick items in each module's checklist |
| Copy a prompt or code | Use the **Copy** button on the block |
| Enlarge a screenshot | Click the image |
| Change text size | **A−**, **A**, **A+** in the header |
| High contrast / dyslexia-friendly | Toggle buttons in the header |
| Export the guide | **Download** button in the header |

Progress and checklist state are held in memory for the current session only (see [Known limitations](#known-limitations)).

## Download the printable guide

Click **Download** in the header to save `AI-Studio-Guide-<LANG>.html` (for example `AI-Studio-Guide-EN.html`). It contains:

- All modules, tables, prompts, checklists, tips, FAQs and images in the **currently selected language**.
- A clickable table of contents.
- A **Print / Save as PDF** button.
- A **↑ Back to top** button at the end of every chapter that returns to the title and contents.

The file is plain semantic HTML with no JavaScript dependency, so it works offline and is friendly to screen readers.

## Printing and PDF export

Open the downloaded guide and press **Print / Save as PDF** (or `Ctrl/Cmd + P`).

The print stylesheet is tuned for **portrait Letter and A4**:

- `@page` portrait with 14 mm / 12 mm margins; paper size follows the browser's choice.
- Chapters flow continuously instead of forcing a new page each time.
- Long code blocks, tables and callouts may split across pages, avoiding large gaps.
- Table rows stay intact and table headers repeat on each page.
- Screenshots are centred, scaled to the page width and capped in height.
- Back-to-top links stay clickable in the saved PDF.

Recommended print settings (Chrome or Edge): **Margins: Default**, **Scale: 100%**, **Headers and footers: Off**, **Background graphics: On**.

## Accessibility

The project aims for **WCAG 2.2 AA**:

- Skip-to-content link and semantic landmarks (`header`, `nav`, `main`, `aside`, `footer`).
- Keyboard-operable controls with visible focus styles.
- `aria-live` announcements for copy, language and download actions.
- `aria-pressed`, `aria-expanded`, `aria-label` and progress-bar roles where appropriate.
- Adjustable font size, high-contrast mode and dyslexia-friendly mode.
- Automatic `lang` attribute updates (`en`, `zh`, `ms`) when the language changes.
- Light/dark colour-scheme awareness.

## Tech stack

- **React** (UI, state via hooks)
- **Tailwind CSS** (utility classes, compiled and inlined)
- **Google Fonts:** Inter, Noto Sans, Noto Sans SC
- **Vanilla browser APIs:** Clipboard API, Blob / `URL.createObjectURL` (download), `window.print()`
- Bundled by a Vite-style bundler into a single file; content (text, tables, images as data URIs) is embedded in the bundle.

## Project structure

```
.
├── index.html   # the entire SPA (bundled, self-contained)
└── README.md
```

Because the HTML file is a bundled build artifact, the source modules are not included. If you maintain the original source project, add it to the repository and document the build commands here.

Inside the bundle:

- **Content data** — module text, tables, prompts, checklists, FAQs and image data in EN / ZH / BM.
- **`eh()`** — the main React component (UI, search, progress, accessibility toggles).
- **`ah()`** — the generator behind the **Download** button. It builds the standalone printable HTML page, including its embedded CSS (screen and `@media print`) and the back-to-top buttons.

## Customization notes

Since this is a minified bundle, edits are best made with care:

- **Printable guide layout / print CSS:** search for `@page{size:portrait` and the preceding `<style>` block inside `ah()`.
- **Back-to-top button label or behavior:** search for `class="totop"` inside `ah()`; the target is `id="top"` on the generated `<header>`.
- **Theme colours:** CSS variables such as `--accent`, `--bg`, `--surface`, `--text` and `--border` near the top of the stylesheet.
- **Languages:** UI strings and module content are keyed by `EN`, `ZH` and `BM`; the language helper `E(en, zh, bm)` is used for inline strings.

Always re-test the live page, the **Download** button and a **Print to PDF** after any change.

## Deployment

Any static host works:

- **GitHub Pages:** rename the file to `index.html`, push, then enable Pages (Settings → Pages → Deploy from branch).
- **Netlify / Vercel / Cloudflare Pages:** drag-and-drop the file or connect the repo; no build command and publish directory is the repo root.
- **Local or intranet:** copy the single file anywhere and open it.

## Browser support

Current versions of Chrome, Edge, Firefox and Safari (desktop and mobile). The Clipboard API requires a secure context (`https://` or `localhost`); opening the file directly via `file://` may block copy buttons in some browsers.

## Known limitations

- **No persistence:** checklist progress is not saved between page reloads.
- **Clipboard** may be unavailable on insecure origins.
- **Fonts** require internet access; otherwise system fonts are used.
- **PDF link behavior** depends on the browser's PDF engine; Chromium-based browsers preserve internal links best.
- **Page breaks** vary slightly between browsers and paper sizes. Very tall images are kept whole and may leave a small gap.
- Google AI Studio's interface changes often; screenshots marked *illustrative* may differ from what you see.

## Contributing

Contributions are welcome.

1. Fork the repository.
2. Create a branch: `git checkout -b feature/your-change`.
3. Make focused changes and test in the browser, including the **Download** and print flows in all three languages.
4. Commit with a clear message and open a pull request describing what changed and why.

Good first contributions: translation fixes, accessibility improvements, updated screenshots, and new prompt templates.

## Disclaimer

This is an independent educational resource. It is **not affiliated with, endorsed by, or sponsored by Google**. *Google*, *Google AI Studio* and *Gemini* are trademarks of Google LLC. Features, names and interfaces of Google AI Studio may change; always verify against the official product.

## License

Please refer to [LICENSE.txt](./LICENSE.txt)