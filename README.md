# darshanram008.github.io

Personal portfolio — RTL-to-GDS digital design, physical design and timing signoff.
Static site, no build step, no dependencies. `index.html` is the whole thing.

Live at <https://darshanram008.github.io/>

## Layout

```
index.html                     the site — all CSS and JS inline
404.html                       styled not-found page
.nojekyll                      skip Jekyll processing on Pages
.github/workflows/deploy.yml   Pages deploy via GitHub Actions
```

Fonts load from Google Fonts; everything else ships with the page.

## Putting it live

The repository **must** be named `darshanram008.github.io` exactly — that is what makes
GitHub serve it as a user site at the apex path rather than under a subdirectory.

```bash
git init
git add .
git commit -m "Portfolio site"
git branch -M main
git remote add origin git@github.com:darshanram008/darshanram008.github.io.git
git push -u origin main
```

Then in **Settings → Pages**, set **Source**. Two options, pick one:

- **GitHub Actions** — uses `.github/workflows/deploy.yml`, already in the repo.
- **Deploy from a branch** — `main` / `/ (root)`. Equally fine for a site with no build
  step; delete `.github/` if you go this way.

First publish takes a couple of minutes. Pushes to `main` redeploy.

## Editing

Content lives in plain HTML in `index.html`, in reading order: hero, signoff strip,
`#work`, `#experience`, `#publication`, `#skills`, `#education`.

**Adding a project.** Copy an existing `<article class="entry">` block. Two things
matter:

- `data-tags` drives the discipline filter. Space-separated, drawn from
  `pd` · `rtl` · `dv` · `emb`. A project with no tags is unreachable by any filter
  except *All*.
- The `<table class="res">` rows are the measured results. Add `class="hi"` to the
  value cell to pull a number into the copper accent — use it for the one figure that
  earns the reader's attention, not for every row.

**Colors and type** are CSS custom properties at the top of the `<style>` block. Every
token is declared in the bare `:root`, then redefined twice for dark — once under
`prefers-color-scheme`, once under `[data-theme="dark"]` so the toggle wins in both
directions. If you add a color, declare it in all three places or it will be undefined
in one of the theme states.

## Unverified claims, deliberately omitted

The page carries only figures traceable to a report. These were left off and should
stay off until sourced:

| Claim | Status |
|---|---|
| NAL percentage improvements (stability, jitter, integration bugs, CPU load, debug speed) | Unsourced estimates |
| "90% relative flux error reduction" (MPLab) | Unsourced; the report shows fidelity improving with sampling density, no figure |
| "Timing closure at 800 MHz" (8-bit µP) | Contradicted — the measured numbers are 350 ps and ≈1.4 GHz |
| "Pipelined MAC" (FIR) | Contradicted — one multiplier and one adder, stepped sequentially |
| ESP-Chiplets interconnect latency / routing overhead | Proposal projections, not measurements |
| Chipathon setup and hold slack | Two prior resumes disagree; no report on hand |
| BERT-Tiny "< 0.6 resource variation" | Metric undefined, not in any report |
| Analog Electronic Circuits project | Report is image-only; contents unknown |

Resolve one and it goes on the page.
