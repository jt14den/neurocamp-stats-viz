# NeuroCamp: Data Viz & Intro Stats

A short, hands-on lesson that teaches high school students to take real data, clean it,
chart it, and ask a scientist's question: **is the difference between two groups real, or
just luck?** It runs entirely in the browser, with no install.

**▶ Live lesson: https://jt14den.github.io/neurocamp-stats-viz/**
**▶ Practice (graded, self-checking): https://jt14den.github.io/neurocamp-stats-viz/practice.html**

---

## About

Built for **NeuroCamp**, UCLA Brain Research Institute's free summer program for ~30 high
school students (grades 9-12) from schools without university-level science access. This
is a one-time ~60-90 min session on **data visualization and introductory statistics
(t-tests)**, built around a **real published experiment** (a randomized stem-cell trial in
sheep) so it mirrors the treatment-vs-control comparisons campers already make (e.g.
*C. elegans* habituation).

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
| `neurocamp-stats.qmd` | The main runnable teaching doc (Quarto + quarto-webr). Source for the live lesson. |
| `practice.qmd` | Companion **graded** challenges (Quarto + quarto-live + gradethis): fill-in-the-blank with instant feedback. The §7 challenges, self-checking. |
| `_quarto.yml` | Website project config so the lesson and practice pages deploy together. |
| `lecture-plan.md` | Session plan: arc, timing, learning objectives, talking points, open decisions. |
| `instructor-notes.md` | Plain-language **stats primer for the presenter** — the p-value/t-test story, a shuffle-demo script, student-question answers, and self-study links. Start here if stats are new to you. |
| `cross-validation-review.md` | Critical design review (backward-design / Carpentries lens) with recommended changes. |
| `data/stem-cell.csv` | Real data: sheep stem-cell heart-attack trial (treatment, before, after). From the `openintro` package (Menasché et al.). |
| `data/stem-cell-messy.csv` | Messy version (a blank, an impossible value, mismatched labels) for the cleaning exercise. |
| `_extensions/` | The `quarto-webr` and `quarto-live` extensions, committed so both pages render after a fresh clone. |

## Using this lesson

### Students
Just open the **[live lesson](https://jt14den.github.io/neurocamp-stats-viz/)** in any
modern browser. Click **Run Code** under a cell to run it; edit and re-run freely. The
first cell is slow (the browser downloads R), then it's fast. **Nothing to install, no
account, no cloud** — R runs inside your browser tab (webr). Bookmark the link to return
later; note the page **resets if you refresh**, so copy out anything you want to keep. To
analyze your own data, type it into the template in section 6.

Want harder, self-checking problems? The
**[Practice page](https://jt14den.github.io/neurocamp-stats-viz/practice.html)** has graded
fill-in-the-blank challenges with hints and instant feedback.

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

quarto preview                       # preview the whole site (lesson + practice)
quarto preview practice.qmd          # just the graded practice page
quarto render                        # build both pages into _site/
```

Want slides instead of a scrolling page? Change `format: html` to `format: revealjs` in
the `.qmd` front matter, or `quarto render neurocamp-stats.qmd --to revealjs`.

## Adapting it

- **Use the class's own data.** Swap the CSV URL in the data cells (sections 1-2 of the
  `.qmd`), or run locally and read `data/your-file.csv`. Any two-group dataset works; update
  the column names in the code (`trmt`, `before`, `after`) to match your file.
- **Change the question.** The whole flow generalizes to any "do these two groups differ?"
  comparison, e.g. treated vs control worms, habituated vs naive, etc.

## Publishing updates

The live site is GitHub Pages, served from the `gh-pages` branch. It's a Quarto **website
project** (both pages), so redeploy the whole site after editing:

```bash
quarto publish gh-pages
```

Source lives on `main`; `quarto publish` renders both pages and pushes the built site to
`gh-pages`.

## How it works (the no-install trick)

The lesson uses **[webr](https://docs.r-wasm.org/webr/latest/)** — R compiled to
WebAssembly — via the **[quarto-webr](https://github.com/coatless/quarto-webr)** extension.
R runs *in the student's browser tab*, not on a server, so there's no install, no account,
and no backend. Packages used (`ggplot2`, `dplyr`, `infer`) are downloaded as pre-compiled
WebAssembly builds on first run and cached.

Trade-off to know: the first cell is a multi-MB download, so on weak classroom wifi with
~30 students at once it can stall. Have students run the first cell early, and keep a
projector-driven fallback ready (see the card-shuffle activity in `lecture-plan.md`).

The **Practice page** uses a sibling extension,
**[quarto-live](https://r-wasm.github.io/quarto-live/)**, which adds graded fill-in-the-blank
exercises (via `gradethis`) on top of the same in-browser webR. The main lesson stays on
quarto-webr; the two run as separate pages.

## Credit

Created by the UCLA Library Data Science Center / DataSquad for NeuroCamp. The
simulation-based approach to inference follows [ModernDive](https://moderndive.com) and the
[infer](https://infer.tidymodels.org) package.
