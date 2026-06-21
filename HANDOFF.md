# Session Handoff — 2026-06-20

## Accomplished
- Lesson complete and live: https://jt14den.github.io/neurocamp-stats-viz/ (repo jt14den/neurocamp-stats-viz, public). Working tree clean, all pushed.
- Real sheep stem-cell data (openintro), clean -> summarize -> graph -> shuffle/p-value flow, predict-first prompts, Excel/spreadsheet parallels + tabset, §7 "Going further" (5 graded challenges with collapsible solutions), no-install "Your turn" with own-data template.
- Jamie (GitHub: jmjamison) added as write collaborator; instructor-notes.md has stats primer + "teaching what you don't know" + CourseKata notes.
- Reply to Elena drafted in Tim's voice at /tmp/email-draft.txt (NOT sent).

## Pending — pick up here next session
1. **Build the quarto-live prototype** (Tim said go). Convert ONE §7 challenge (effect-size, Challenge 1) into a graded fill-in-the-blank exercise with feedback using the `quarto-live` extension (r-wasm.github.io/quarto-live, gradethis). Keep it a SEPARATE file (e.g. `prototype-quarto-live.qmd`), do NOT migrate the main lesson off quarto-webr before June 25. Goal: let Tim + Jamie see the feedback UX and decide if it's worth adopting.
2. Confirm with Elena/Jamie the open logistics (length 60/75/90, room devices + wifi, time slot on the 25th, whether to use campers' own data). See lecture-plan.md "Still to confirm".
3. Optional: send the Elena reply once Tim approves it.

## Decisions made
- Dataset: openintro::stem_cell (real, p=0.0017, sheep tie-in) over crickets/Guyer/synthetic.
- Stay on quarto-webr for the live lesson; quarto-live only as a prototype/v2.
- CourseKata incorporated as a light touch (predict-first + variation framing), not a full model-comparison rebuild.

## Files modified
- All in ~/projects/lessons/instruction/2026-06-25-neurocamp/ (neurocamp-stats.qmd, lecture-plan.md, instructor-notes.md, README.md, cross-validation-review.md, data/stem-cell*.csv). All committed.

## Blockers / waiting on
- quarto-live install needs network (sandbox blocks `quarto add`; use dangerouslyDisableSandbox or run unsandboxed, as we did for quarto-webr).
