# AGENTS.md

## Cursor Cloud specific instructions

### What this repo is
This repository is a single, self-contained static web app: `index.html` (HTML + CSS + vanilla JS, no framework). It is the **Planning Apply Queue** dashboard — a read-only job-hunt queue. The job data is baked directly into `index.html` inside `<script id="payload" type="application/json">` and is regenerated externally by a bot (`hunt-bot`); do not expect a scraper/backend in this repo. "Applied" state is stored only in browser `localStorage` (`jobhunt.applied.v1`), not on any server.

### Dependencies / build
- There are **no dependencies, package manager, lockfiles, or build step**. Nothing to install.
- There is **no lint, test, or build tooling** in this repo. Do not fabricate `npm`/`make` commands — none exist.

### Running it (the only "service")
Serve the static file with any HTTP server and open it in a browser. Serving over HTTP (not `file://`) matters because the "Copy done IDs" button uses the clipboard API:

```
python3 -m http.server 8080 --directory /workspace
```

Then open `http://localhost:8080/`. `python3` and `node` are both available in the environment.

### Verifying changes
This is a UI-only app, so verify visually in the browser. Core flow to smoke-test: load the page, click "Mark applied" on a job card — the funnel "actioned" count should increment, "still open" should decrement, the button should read "Applied", and the card should dim. Toggle the "Hide done" chip to show/hide completed jobs.
