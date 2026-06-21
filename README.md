# NeuroCamp: Data Viz & Intro Stats

A short, hands-on lesson that teaches high school students to take real data, clean it,
chart it, and ask a scientist's question: **is the difference between two groups real, or
just luck?** It runs entirely in the browser, with no install.

**▶ Live lesson: https://jt14den.github.io/neurocamp-stats-viz/**

---

## About

Built for **NeuroCamp**, UCLA Brain Research Institute's free summer program for ~30 high
school students (grades 9-12) from schools without university-level science access. This
is a one-time ~60-90 min session on **data visualization and introductory statistics
(t-tests)**, themed around a reaction-time experiment so it mirrors the two-group
comparisons campers already make (e.g. *C. elegans* habituation).

- **Date:** Thursday, June 25, 2026
- **Presenter:** Jamie Jamison (DataSquad / UCLA Data Science Center)
- **Host:** Elena Dominguez, NSIDP

## What students learn

By the end, a student can:

1. Find the rows, columns, and variables in a dataset and run a cell in a coding environment.
2. Spot and fix common data problems (blanks, impossible values, mismatched labels).
3. Calculate a group's average and spread, and choose + build a graph to compare two groups.
4. Decide, in plain language, whether a difference is likely real or due to chance, and find the p-value.

(See `lecture-plan.md` for the full objectives, checks for understanding, and timing.)

## Repository contents

| File | What it is |
|---|---|
| `neurocamp-stats.qmd` | The runnable teaching doc (Quarto + webr). Source for the live site. |
| `lecture-plan.md` | Session plan: arc, timing, learning objectives, talking points, open decisions. |
| `instructor-notes.md` | Plain-language **stats primer for the presenter** — the p-value/t-test story, a shuffle-demo script, student-question answers, and self-study links. Start here if stats are new to you. |
| `cross-validation-review.md` | Critical design review (backward-design / Carpentries lens) with recommended changes. |
| `data/reaction-time.csv` | Clean sample dataset (reaction to sound vs light). |
| `data/reaction-time-messy.csv` | Messy version (blanks, bad decimals, mismatched labels) for the cleaning exercise. |
| `_extensions/` | The `quarto-webr` extension, committed so the doc renders after a fresh clone. |

## Using this lesson

### Students
Just open the **[live lesson](https://jt14den.github.io/neurocamp-stats-viz/)** in any
modern browser. Click **Run Code** under a cell to run it; edit and re-run freely. The
first cell is slow (the browser downloads R), then it's fast. Nothing to install.

### Instructor
1. Read `lecture-plan.md` (what happens when) and `instructor-notes.md` (the stats, in plain words).
2. Decide the open questions (length, devices/wifi, whether to use campers' own data).
3. Teach from the live site, or render locally (below) to project it.

## Running and editing locally

Requires [Quarto](https://quarto.org) and R. The webr extension is already committed, so a
fresh clone renders without extra setup.

```bash
git clone https://github.com/jt14den/neurocamp-stats-viz.git
cd neurocamp-stats-viz

quarto preview neurocamp-stats.qmd   # live preview while editing
quarto render  neurocamp-stats.qmd   # one-time render to index.html
```

Want slides instead of a scrolling page? Change `format: html` to `format: revealjs` in
the `.qmd` front matter, or `quarto render neurocamp-stats.qmd --to revealjs`.

## Adapting it

- **Use the class's own data.** Swap the CSV URL in the data cells (sections 1-2 of the
  `.qmd`), or run locally and read `data/your-file.csv`. Any two-group, one-measurement
  dataset works (the column names `cue` and `reaction_ms` are what the code expects, so
  either match them or update the code).
- **Change the question.** The whole flow generalizes to any "do these two groups differ?"
  comparison — dominant vs non-dominant hand, treated vs control, etc.

## Publishing updates

The live site is GitHub Pages, served from the `gh-pages` branch. To redeploy after editing:

```bash
quarto publish gh-pages neurocamp-stats.qmd
```

Source lives on `main`; `quarto publish` renders and pushes the built site to `gh-pages`.

## How it works (the no-install trick)

The lesson uses **[webr](https://docs.r-wasm.org/webr/latest/)** — R compiled to
WebAssembly — via the **[quarto-webr](https://github.com/coatless/quarto-webr)** extension.
R runs *in the student's browser tab*, not on a server, so there's no install, no account,
and no backend. Packages used (`ggplot2`, `dplyr`, `infer`) are downloaded as pre-compiled
WebAssembly builds on first run and cached.

Trade-off to know: the first cell is a multi-MB download, so on weak classroom wifi with
~30 students at once it can stall. Have students run the first cell early, and keep a
projector-driven fallback ready (see the card-shuffle activity in `lecture-plan.md`).

## Credit

Created by the UCLA Library Data Science Center / DataSquad for NeuroCamp. The
simulation-based approach to inference follows [ModernDive](https://moderndive.com) and the
[infer](https://infer.tidymodels.org) package.
