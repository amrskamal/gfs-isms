# Gulf Freight Systems — ISMS Workbench

A training ISMS for a fictional Abu Dhabi logistics company, built clause by clause.
See `CLAUDE.md` for what this is, and `LEARNING_PLAN.md` for the 30 sessions.

**The whole application is one file: `index.html`.** No installer, no server, no
accounts, no build step, no dependencies.

---

## Opening it

**Any of these work, on any machine:**

- Double-click `index.html`.
- Drag `index.html` onto an open Chrome or Edge window.
- Copy it to a USB stick, plug the stick into another laptop, open it from there.
- Or, if you publish it, open the GitHub Pages URL.

Nothing is installed and nothing is downloaded. If the browser asks for permission to
do anything, that is not this page.

**Requirements:** Chrome or Edge (or any current browser). No extensions needed, no
developer mode, no policy exceptions. It works with JavaScript enabled and nothing else.

## Where your work is kept

Everything you type is written to that browser's `localStorage`, on that machine only.
It is not sent anywhere and it is not readable by any other site.

Two consequences worth understanding before you rely on it:

- **Storage is per-browser and per-origin.** Work done in the file opened from your USB
  stick does not appear in the GitHub Pages version, or in a different browser, or in a
  private window. Move work between them with Export/Import.
- **Some locked-down machines block storage entirely.** The app detects this, shows an
  amber banner, and keeps working — but your changes then last only until you close the
  tab. Export before you close.

Clearing your browser's site data will delete your work. Export regularly.

## Export / Import / Reset

The three buttons are in the sidebar under **Your data**.

| Button | What it does |
|---|---|
| **Export** | Downloads everything as one plain JSON file, `gfs-isms-YYYY-MM-DD.json`. Nothing but data — no scripts, no formatting, no macros. Safe to email, archive, or read in any text editor. |
| **Import** | Opens a file picker, then asks you to confirm before replacing what is currently in the app. Unknown fields are discarded and every value is treated as plain text, so a malformed or hostile file cannot do anything except fail to import. |
| **Reset** | Puts everything back to the original Gulf Freight Systems seed data. Asks first. Export before you use it. |

Typical workflow across machines: **Export** on the laptop where you did the work,
carry the JSON file, **Import** on the other machine.

## It makes no network calls

This is a deliberate design constraint, not a side effect:

- No `fetch`, no `XMLHttpRequest`, no WebSocket, no `sendBeacon`, no service worker.
- No external scripts, stylesheets, fonts, images, analytics or CDN references. All CSS
  and JavaScript are inline in `index.html`.
- No cookies, no telemetry, no error reporting, no API keys — there is no server to talk to.
- A `Content-Security-Policy` meta tag in the file sets `default-src 'none'` and
  `connect-src 'none'`, so even if a network call were added by mistake, the browser
  would block it.

Verify it yourself: open DevTools → Network, reload, and count the requests. You should
see exactly one — the page itself — and zero when opened from a local file.

`.github/workflows/pages.yml` re-runs the same checks on every push and fails the
deployment if an external reference, a network API, or an unsafe HTML sink appears.

## Files

| Path | What it is |
|---|---|
| `index.html` | **The entire application.** CSS, JavaScript and seed data inline. ~69 KB. |
| `CLAUDE.md` | The teaching contract and the rules future sessions must follow. |
| `LEARNING_PLAN.md` | 30 sessions, each with a task and five questions. |
| `auditor/AUDITOR_MODE.md` | The mock PECB Stage 2 auditor persona. |
| `.claude/commands/auditor.md` | `/auditor A.8.13` when running Claude Code from this directory. |
| `.github/workflows/pages.yml` | Publishes `index.html` (and nothing else) to GitHub Pages. |
| `legacy-python/` | The retired Python + SQLite version and its database, kept as a local backup. Git-ignored, never deployed. Delete it whenever you like. |

## Publishing to GitHub Pages (optional)

```bash
git init && git add . && git commit -m "ISMS workbench"
git branch -M main
git remote add origin git@github.com:<you>/<repo>.git
git push -u origin main
```

Then in the repository: **Settings → Pages → Source → GitHub Actions**. The workflow
publishes `index.html` alone — the learning notes and the auditor prompt stay private
to the repository.

Note that a published page is public. The seed data is fictional, and `.gitignore`
excludes `*.json` so your exports are never committed by accident, but do not put real
company information into a copy you intend to publish.

## Status

- [x] Session 1 — Scope & Context (clause 4)
- [ ] Asset register (S4) · Risk register (S6) · Control library (S11) · SoA (S17)
- [ ] Policy library (S19) · Internal audit (S27) · Management review (S29)

Gulf Freight Systems is fictional. Legal references are illustrative training material
and are not legal advice.
