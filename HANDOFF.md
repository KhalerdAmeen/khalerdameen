# HANDOFF — khalerdameen.com

Personal one-page site for Khalid (khalerdameen). Single static HTML file, no
build step, hosted on Vercel, auto-deployed from GitHub. This document is the
handoff for moving the project to a new tool.

_Last updated: 2026-11-13._

---

## 1. What this is

- **Live site:** https://khalerdameen.com (production)
- **Repo:** https://github.com/KhalerdAmeen/khalerdameen (public)
- **Hosting:** Vercel Hobby, auto-deploys on push to `main`
- **Everything is in `index.html`** — all HTML, CSS (`<style>`) and JS (one
  `<script>` at the end of `<body>`). Vanilla only, no frameworks, no libraries,
  no build step.

## 2. Current state — what's built

The live site is the **redesigned** version (benji.org-style: minimal, prose-first,
single centered column, left-aligned body). Features in `index.html`:

- **Palette & type:** black `#000` background, amber `#C8922A` text, self-hosted
  **Ayuthaya** font from `/fonts/Ayuthaya.ttf`. Green `خالد` logo with red layered
  text-shadow — rendered as **text**, not an image.
- **Geo greeting:** on load, fetches `https://ipapi.co/json/` (3s timeout). Types
  out "Good morning/afternoon/evening, [friend] from [City]" where `[friend]` is
  localized by the visitor's language. Logo crossfades to a localized script for
  zh/ko/ru/hi/el. Silently hides if the fetch fails/times out.
- **Owl mascot** (inline SVG, top-right of the logo): head rotates toward the
  cursor (lerped, ±20°), pupils track the cursor, blinks on a timer; on touch
  devices it does periodic idle tilts; static under `prefers-reduced-motion`.
  (Replaced an earlier falcon — see Key decisions.)
- **Intro prose** with 6 inline links (Khad Studio, Routn, Context Labs, Reelhouse,
  Hilal, Nexstop) carrying an **RGB-split glitch effect** (green/red pseudo-element
  copies). Fires on hover + keyboard focus on hover devices; runs once in sequence
  on touch after the intro fades in; disabled under `prefers-reduced-motion`.
- **"Building" accordion:** 6 dropdown rows (Khad Studio, Routn, Context Labs,
  Reelhouse, Hilal, Nexstop). CSS-grid height animation, one-open-at-a-time,
  `aria-expanded`/`aria-controls`, keyboard-operable, reduced-motion aware.
- **Footer:** social/contact/credit links + a live **London time** clock
  (`Intl.DateTimeFormat`, refreshes every 30s).
- **Load animation:** staggered fade-up (greeting → logo → intro → building → footer).
- **Analytics:** Vercel Analytics script tag.

## 3. File / folder structure

```
/
├── index.html          ← the entire site (HTML + CSS + JS)
├── fonts/
│   └── Ayuthaya.ttf     ← self-hosted font (referenced by @font-face)
├── public/
│   └── logo.svg         ← ORIGINAL logo asset — currently UNUSED (logo is text now)
├── favicon.png
├── vercel.json          ← font content-type + long-cache headers (keep this)
├── README.md
├── HANDOFF.md           ← this file
├── DEPLOY.md            ← deploy guide (see §8; partly historical)
├── PROMPT.md            ← original build spec — STALE, pre-redesign
├── content.md           ← original content doc — STALE, pre-redesign
└── public:logo.svg      ← stray mis-named duplicate of public/logo.svg (see Gotchas)
```

## 4. What's left / open items

- **Reelhouse copy:** the Building dropdown currently reads **"Coming soon."**
  (reverted from a cinema-journal description at the owner's request). When the
  product is ready, update that panel's text. All Reelhouse URLs point to
  `https://reelhouse-landing.vercel.app/`.
- **No live visual QA has ever been done.** Every change across these sessions was
  verified with static structure checks + a DOM-stub simulation of the JS — never a
  real browser (the agent had no working browser). **Before trusting the new tool,
  open the live site and check at 375px and 1440px:** owl cursor-tracking, the
  intro-link glitch (hover + touch), the geo greeting, the London clock, and the
  accordion animation.
- **Stale docs:** `PROMPT.md` and `content.md` (and parts of `DEPLOY.md`) describe
  the *original* pre-redesign site (Google Fonts, "22yo founder" tagline, no JS,
  380px column, flat project links). They do **not** match the current site. Update
  or archive them.
- **Unused asset:** `public/logo.svg` is no longer referenced (logo is text). Keep
  or remove.
- **Stray file:** remove `public:logo.svg` (see Gotchas).
- **Meta description** still reads "22yo founder. building & scaling brands." — kept
  deliberately (instructions were to preserve meta tags verbatim) even though the
  visible copy changed. Decide whether to refresh it.

## 5. Key decisions (and why)

- **Logo is text, not `<img>`.** Needed so the geo feature can swap it to localized
  scripts and so the owl can perch on its edge. `public/logo.svg` became unused.
- **Font is self-hosted** (`/fonts/Ayuthaya.ttf` via `@font-face`), not Google Fonts
  as the original `PROMPT.md` specified.
- **Single file, vanilla, no build.** All CSS/JS inline in `index.html`. Keeps Vercel
  config trivial (framework preset "Other", empty build command).
- **`main` is the production branch.** Merges to `main` auto-deploy to the apex
  domain; feature branches get Vercel preview deploys.
- **Mascot history:** falcon (line-art) → detailed falcon → **owl** (current). The
  owl uses `transform-box: fill-box` + explicit `transform-origin` on the SVG groups
  because CSS transforms on SVG elements otherwise pivot from the SVG's `(0,0)`
  origin and look broken/invisible.

## 6. Gotchas

- **Pushing to `main` deploys to production immediately.** Use a branch + PR for
  anything you want to preview first.
- **Repo must stay public** for the Vercel Hobby free tier (per `DEPLOY.md`).
- **`vercel.json`** sets the font MIME type and a 1-year immutable cache on
  `/fonts/*`. Don't drop it or the font can be served with the wrong content-type.
- **ipapi.co** is a free endpoint with rate limits; the greeting is best-effort and
  hides itself on any failure/timeout — don't treat a missing greeting as a bug.
- **`.DS_Store`** was committed in the project's history; it's now in `.gitignore`
  and untracked going forward.
- **`public:logo.svg`** is an accidental file whose name contains a colon (a botched
  `public/logo.svg`). It isn't referenced anywhere; safe to delete.

## 7. Non-code files (designs, emails, docs) and where they are

- **No designs, emails, or external documents were produced outside this repo** in
  the course of these sessions.
- The project's own docs live at the repo root: `README.md`, `DEPLOY.md`,
  `PROMPT.md`, `content.md` (the last two are stale — see §4).
- **Original design source:** the visual spec came from a Figma file referenced in
  `PROMPT.md`; that Figma file is **not** in this repo and its URL was not recorded
  here — ask the owner for it if you need the source of truth for the logo/colors.
- No screenshots exist (the agent never had a working browser).
- Throwaway JS validation scripts were written to `/tmp` during QA and have since
  been cleared; they contained only structural assertions about `index.html` and
  hold no project value. (Hence there is no `/assets` folder — nothing external to
  preserve.)

## 8. Deploy flow

```bash
# edit index.html, then:
git add .
git commit -m "…"
git push               # feature branch → Vercel preview deploy
# open a PR to main and merge → Vercel production deploy to khalerdameen.com
```

Domain/DNS and first-time Vercel setup are documented in `DEPLOY.md` (steps 2–3 are
still accurate; step 1 "git init / create repo" is already done).

## 9. Git state at handoff

- Production branch: **`main`** (contains PRs #1–#4: owl + footer, Context Labs +
  glitch, Reelhouse "coming soon").
- This handoff (HANDOFF.md + `.gitignore` + `.DS_Store` untrack) is committed on the
  branch noted in the final `REPO: … | BRANCH: … | ENV: …` line and pushed to GitHub.
- No `.env` or secret files exist in this project; nothing secret was committed.
