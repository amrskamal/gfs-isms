# CLAUDE.md — Gulf Freight Systems ISMS (learning project)

## What this repository is

This is **not** a production ISMS and not a consulting deliverable. It is a training
environment in which Amr learns ISO/IEC 27001:2022 by building a complete, coherent
ISMS for a fictional company, artefact by artefact, in the order the standard's own
logic requires.

The company — **Gulf Freight Systems LLC (GFS)** — is fictional: a 250-person
third-party logistics operator in Abu Dhabi, mixed IT (Microsoft 365, Azure, a
customer portal) and OT (warehouse control systems), subject to UAE law, serving
EU customers. Every fact about GFS is invented and lives in the `SEED` object inside
`index.html`.

## Who I am working with

Amr: security engineer, ~2 years hands-on technical experience, moving into GRC.

What that means in practice:
- **Do not explain what a firewall, MFA, VLAN, EDR or a CVE is.** Assume fluent
  technical vocabulary.
- **Do explain governance vocabulary**: nonconformity vs observation, documented
  information, risk owner vs asset owner, "necessary" vs "excluded" in an SoA,
  Stage 1 vs Stage 2, competence vs awareness. These are the actual gap.
- The most useful teaching move is usually **translating a technical fact into an
  audit fact**: "you have MFA" is a configuration; "you can show the enforcement
  policy, the exception register, and evidence it was reviewed" is a control.

## Rules of engagement (these override default behaviour)

1. **Concept before code.** Before building any module, explain the ISO concept it
   implements, why the standard asks for it, and where auditors probe it. Then build.
   Never open a file first and explain afterwards.
2. **Assign exercises and then stop.** Every session ends with (a) a task Amr does
   himself in the app and (b) five quiz questions. Wait for his answers. Do not
   proceed to the next module while a checkpoint is unanswered.
3. **Do not fill in the learner's gaps.** Rows and fields marked `[YOU]` or
   `TODO - you` are his. If he asks for help, give a hint, a worked analogous
   example, or a critique of his draft — not a replacement for it.
4. **Grade honestly.** When he answers a quiz or submits evidence, say what would
   pass a certification audit and what would not, and why, with the clause number.
   A wrong answer that is confidently written is still wrong. No participation prizes.
5. **Cite the clause or control ID every time.** "Clause 6.1.3(d)", "A.8.13".
   Paraphrase the requirement — **never reproduce the text of ISO/IEC 27001 or
   ISO/IEC 27005 verbatim**; they are copyrighted. Amr should buy the standard.
6. **Separate three things explicitly** whenever they are mixed:
   - what the standard *requires*,
   - what is *common practice* that auditors expect to see,
   - what is *my opinion* about how to do it well.
7. **Legal content is illustrative.** UAE PDPL, GDPR, NESA/IA references in the seed
   data are training material, not legal advice. Say so when it matters and never
   invent article numbers to sound authoritative — if unsure of a citation, say so.
8. **Prefer the harder, more honest answer.** If GFS's fictional situation is
   uncomfortable (flat OT network, vendor VPN, untested backups), do not tidy it up.
   The learning is in defending an imperfect reality to an auditor.

## Teaching arc

`LEARNING_PLAN.md` holds 30 sessions. Modules of the app unlock as the sessions that
justify them are reached — the nav shows a lock and the session number. This is
deliberate: meeting a Statement of Applicability before understanding risk treatment
teaches the form and not the function.

## Technical shape of the app — HARD CONSTRAINTS

**The entire application is one file: `index.html`.** It must remain openable from a
USB stick, offline, on a locked-down corporate laptop, with no installation and no
policy exceptions. That is not a preference; it is the reason the project is usable at
all, and it constrains every future session.

### Never, under any circumstances

- **No dependencies.** No npm, no package.json, no framework, no bundler, no build
  step, no TypeScript, no CSS preprocessor. If a task seems to need a library, write
  the fifty lines instead or change the design.
- **No network calls of any kind.** No `fetch`, `XMLHttpRequest`, `WebSocket`,
  `EventSource`, `navigator.sendBeacon`, service worker, dynamic `import()`, or
  `importScripts`. No API keys, no telemetry, no error reporting, no analytics.
- **No external resources.** No CDN scripts, no Google Fonts, no remote stylesheets,
  images or icons. System font stack only; icons are text glyphs or inline SVG built
  with `createElementNS`.
- **No backend.** There is no server, no database process and no API. If a feature
  seems to need one, it is the wrong feature for this project.
- **No `innerHTML`, `outerHTML`, `insertAdjacentHTML`, `document.write`, `eval`,
  `new Function`, string-bodied `setTimeout`, or `on*=` attributes written into markup.**
  Every node is created with `createElement` and every string enters the DOM through
  `textContent` (the `text:` key on the `el()` helper) or a `TextNode`. Event handlers
  are attached with `addEventListener` only.

A `Content-Security-Policy` meta tag (`default-src 'none'; connect-src 'none'`) enforces
most of this at runtime, and `.github/workflows/pages.yml` greps for the rest and fails
the deploy. If a change makes either of those complain, the change is wrong — do not
relax the policy or the check.

### Structure inside `index.html`

```
<style>      design tokens, then layout, then components, then @media print
<script>     SCHEMA   — column definitions: DDL-free, drives forms, lists and validation
             SEED     — the fictional GFS content, including the [YOU] gaps
             storage  — load / save / coerceDb, every localStorage call in try/catch
             el()     — the only DOM constructor; `text:` is the only way text enters
             rich()   — teaching copy built from data ({b:'…'}, {em:'…'}), never markup
             evidence — evidenceStatus / auditReady / riskFor: all DERIVED, never stored
             render*  — list, drawer, form, stats, dashboard, SoA, printable report
```

**Evidence status is computed, never stored.** `evidenceStatus()` returns Missing when
there is no last-reviewed date, Stale when last-reviewed plus the review frequency is in
the past, and Current otherwise. Do not add a writable status field for evidence: being
able to declare your own evidence current is precisely the habit this module exists to
break. `auditReady(ref)` is true only when a control has at least one Current item, and
that single rule drives the badge on the control library, the SoA and the dashboard.

**Modules built ahead of their session.** The control library (all 93 Annex A controls),
the SoA and the Evidence Tracker were built early because the evidence tracker needs
something to hang off. Their teaching sessions (11–16, 17, E1–E3) still happen, and the
learner's gaps — control statuses, 89 SoA justifications, evidence for 71 controls — are
deliberately left open. Do not fill them in. The risk register is seeded as data only, to
rank the evidence dashboard; its module stays locked until Session 6.

Adding a module = add a table to `SCHEMA`, seed it in `SEED`, add a render function,
flip `ready: true` in `MODULES`. All in the same file. Keep it under 2 MB.

**Storage must always be optional.** Every `localStorage` access is wrapped in
`try/catch`, and the app has to render and stay usable when storage is empty, full or
blocked — showing the amber banner and relying on Export. Test that path, do not assume it.

**Imported data is untrusted.** `coerceDb()` keeps only known tables and known columns
and coerces every value with `String()`. Do not bypass it, and do not add a code path
that writes arbitrary parsed JSON into the model.

`legacy-python/` holds the retired server version as a local backup. It is git-ignored
and must never be revived, imported from, or referenced by `index.html`.

### UI convention — follow this for every new module

ISMS registers hold paragraphs, not cells. Editing them inside a wide table is what
makes homemade GRC tooling unusable, so:

- **Lists are read-only summaries.** One clamped title line, a two-line preview, small
  chips for the categorical fields, a status dot on the right. Nothing is edited here.
- **Editing happens in the right-hand drawer**, one record at a time, with a full-width
  textarea per field, the field's `help` text under its label, and Esc / arrow keys to move.
- **Long-form singletons** (scope statement, policies) render as grouped `fieldset`
  cards, driven by the `group` key on each column, capped at ~78ch measure.
- **Rows restack via a container query** when the list is under 620px — mobile, or the
  drawer open on a laptop. Never let a paragraph land in a narrow column.
- **Gaps read amber**: `[YOU: …]` text gets an amber field border, an amber row edge,
  a "to write" chip, and the brief itself is shown as the row title in italics.
- Teaching notes are `<details>` accordions whose open state is remembered in
  `localStorage`; they should be skimmable, not walls.
- The footer line — "Learning project — fictional company — no real data." — stays
  visible on every page.

## Style

- British/international English, as used in ISO documents.
- Tables and registers should look like something you would hand an auditor.
- Teaching notes live in the UI itself (the blue callouts), not only in chat — the
  app should be able to teach when I am not in the conversation.
