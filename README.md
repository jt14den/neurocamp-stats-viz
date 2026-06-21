# NeuroCamp mini-lecture — Data Viz & t-tests

One-time ~75 min session for NeuroCamp (K-12), Thursday June 25, 2026.
Presenter: Jamie Jamison. Host: Elena Dominguez (NSIDP).

## Files

| File | What it is |
|---|---|
| `lecture-plan.md` | Instructor-facing session plan, timing, talking points, open decisions |
| `neurocamp-stats.qmd` | The runnable teaching doc (Quarto + webr) students/instructor work through |
| `data/reaction-time.csv` | Clean sample dataset (sound vs light). Swap with live class data if collected |
| `data/reaction-time-messy.csv` | Messy version (blanks, bad decimals, mismatched labels) for the cleaning exercise |

## ⚠️ Before the lecture — must do

1. **Confirm the grade band with Elena.** This plan assumes grades ~6-12. See the
   assumptions section at the top of `lecture-plan.md`. If younger, cut the code.

2. **Install the quarto-webr extension** (one time, in this folder):
   ```bash
   cd ~/projects/lessons/instruction/2026-06-25-neurocamp
   quarto add coatless/quarto-webr
   ```

3. **Data is already wired.** The doc loads both CSVs from this repo's raw GitHub URLs
   (`jt14den/neurocamp-stats-viz/main/data/...`), so the webr cells work as-is — no setup.
   To use the class's own data instead, swap the URL, or run locally with
   `read.csv("data/reaction-time.csv")`.

## Render

HTML (default):
```bash
quarto render neurocamp-stats.qmd
```

Slides (revealjs) for lecturing — change the format in the YAML to `revealjs`, or:
```bash
quarto render neurocamp-stats.qmd --to revealjs
```

Live preview while editing:
```bash
quarto preview neurocamp-stats.qmd
```

## Notes

- First webr cell is slow (browser downloads R + packages, several MB), then fast.
- Packages used: `ggplot2`, `dplyr`, `infer` — all available as webr Wasm builds.
- If a room has no devices, the instructor can drive the whole doc on the projector;
  the plan's card-shuffle activity covers the hands-on part without computers.
