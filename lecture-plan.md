# NeuroCamp mini-lecture: Data Viz & "Easy Stats" (t-tests)

**Date:** Thursday, June 25, 2026
**Length:** 60-90 min (plan below is built for ~75 min, with cut/stretch points marked)
**Presenter:** Jamie Jamison (DataSquad / DSC)
**Audience:** NeuroCamp — **~30 high school students, grades 9-12** (UCLA BRI summer program)
**Host:** Elena Dominguez (NSIDP)

---

## About NeuroCamp (context for the example choices)

UCLA BRI's NeuroCamp is a free 8-day summer program (two weeks; June 25 is the
Thursday of week 2) for ~30 motivated high schoolers. They do real wet-lab work and
lectures across **molecular neurobiology, neurophysiology, and neuroanatomy** —
sheep-brain dissection, cow spinal cords, **C. elegans habituation**, PCR, earthworm
RNA/epigenetics — and they present to their peers.

**Why this matters for us:** these are bright, science-motivated teens who have already
*collected data from experiments*. We can assume they understand "two groups, did the
treatment do something." That lets us run real code (webr) and tie the t-test directly
to comparisons they've already made (e.g. did habituated worms respond differently than
controls?). Pitch to their level, not down to it.

---

## ⚠️ Still to confirm with Elena before finalizing

Grade band is now settled (9-12). Remaining unknowns, confirm at the planning meeting:

1. **Room / devices.** Do students have laptops or Chromebooks (one each? shared?)? Is
   there a projector + wifi? This decides whether they run webr themselves or Jamie
   drives it. With grade 9-12 and devices, **let them run it** — much stronger.
2. **Exact time slot** within the 8 AM-4 PM day, and whether anything precedes/follows.
3. **Their own data.** Do they have data from their C. elegans / earthworm experiments
   we could plug in instead of the canned reaction-time set? That would land hardest.
4. **Prior stats exposure.** Have they seen box plots / averages of groups before?

Default prereq line to send Elena:
> "Students should bring a laptop or Chromebook with a web browser. Comfort with
> averages and reading a simple chart is enough. No software install and no prior
> coding needed — everything runs in the browser."

---

## Learning objectives

Elena's brief asks for two topics (**Statistical Testing** and **Making Graphs & Data
Visualization**) and lists seven candidate objectives. Rewritten here as measurable,
checkable outcomes (4 core + 2 stretch), with what each covers from her list.

**By the end, students will be able to:**

1. **Find** the rows, columns, and variables in a dataset and **run** a cell in a
   browser-based coding environment. *(Elena: navigate a spreadsheet / coding environment)*
2. **Spot and fix** three common data problems (blanks, impossible values, mismatched
   labels) in a small dataset. *(Elena: organize and clean data)*
3. **Calculate** a group's average and spread and **choose + create** an appropriate graph
   (dot / box) to compare two groups. *(Elena: run calculations, interpret averages and
   variability, choose a graph, create a graph)*
4. **Decide and explain**, in plain language, whether a difference between two groups is
   likely real or due to chance, and **locate** the p-value in the output. *(Elena:
   understand why scientists use statistics, interpret p-values)*

**Stretch (only if time and devices allow):**

5. **Modify** the code to compare a different pair of groups, or their own camp data.
6. **Enter** new data values by hand and re-run. *(Elena: enter data. Demoted on purpose:
   30 novices typing into code cells is slow and error-prone. Better done as one shared
   live-collection moment, board to a single cell.)*

### Checks for understanding

One quick formative check per objective, ~30 sec each. Without these you're lecturing, not
teaching to objectives.

| Objective | Check |
|---|---|
| 1 (run a cell) | Show of hands / green check once everyone has run cell 1 |
| 2 (clean data) | "Find the 3 problems" call-out before revealing the fix |
| 3 (summarize + graph) | Quick poll: "which chart compares two groups?", then everyone produces a box plot that runs |
| 4 (real or luck) | Exit question: "p = 0.01, real or luck? p = 0.40, real or luck?" thumbs up/down |

**Predict before every reveal.** Borrowed from CourseKata: before running each cell, have
students commit to a guess (which group is higher, what the plot looks like, real or luck).
The doc has these as "Predict first" callouts. A prediction turns passive watching into
active learning and surfaces misconceptions for free, and it's the non-expert teacher's best
friend (the prediction does the teaching, not you).

### ⚠️ Scope reality

Seven candidate objectives, four of them hands-on data skills, in 60-90 min with students
who may never have opened a spreadsheet or coding tool. You cannot do all of it *deeply*.
Recommendation:

- **Anchor on the hands-on flow** (get into the tool, clean data, summarize, graph). It
  covers most of the objectives and builds the confidence Elena names.
- **Keep statistical testing as the satisfying capstone**, lighter on mechanics. The
  shuffle test carries the p-value intuition; don't belabor t-test math.
- If forced to cut: drop the formal t-test demo (§7) before cutting the hands-on flow. The
  "is it real or luck?" intuition matters more than the `t.test()` output for this age.

The one decision to confirm with Elena/Jamie: **hands-on data literacy first, statistical
testing as the payoff**, vs. a more concept-heavy stats talk. The plan below assumes the
former.

---

## Big idea (the one thing they should leave with)

> You can take real data, put it into a tool, make a picture of it, and ask:
> **is the difference between two groups real, or just luck?**
> Scientists answer that with a p-value, and now you've done it yourself.

---

## Theme: a real sheep stem-cell experiment

The running dataset is a **real, published randomized trial**: 18 sheep were given heart
attacks, then half got embryonic stem cells (`esc`) and half didn't (`ctrl`). Researchers
measured each heart's pumping capacity (a percent) before and after. Source: Menasché et
al., via the `openintro` R package.

Example question: **"Can stem cells help a damaged heart recover?"**

Why this dataset:
- **Real and published**, not made up. Students analyze actual research.
- **Ties to NeuroCamp** (they dissect sheep brains and spinal cords; this is sheep too).
- **Treatment vs control**, the same experimental design they use, so it transfers directly
  to their *C. elegans* habituation and earthworm work.
- The **before/after change score** is a genuine data-handling step (a calculation they
  build), not just a column they're handed.

---

## Cross-tool framing (a transferable-skills thread)

Worth saying out loud as you go: **these operations are the same in every tool.** Every data
project runs load → clean → restructure (new columns, reshape/pivot) → summarize → analyze.
We're in R, but in Excel that's Find & Replace, a calculated column, and a PivotTable. The doc
has "Same idea in a spreadsheet" asides at the clean, new-column, and summarize steps, plus a
"why a coding tool, not Excel?" callout at the shuffle (honest answer: reproducibility + the
simulation). Naming the pipeline helps students carry the skill to whatever tool they use next,
and it reassures the spreadsheet-comfortable kids that they already know most of this.

---

## Session arc (built for ~90 min; 60/75 trims below)

### 1. Hook — feel the variability (10 min) · *why stats*
- Optional warm-up (no data needed): ruler-drop catch in pairs, or a reaction-time site on
  the projector. A couple of volunteers, a couple of tries each.
- Point: "Everyone's different. Even the *same* person differs each try." **Measurements vary.**
- Pivot: "Real scientists deal with this constantly. Here's a real experiment where it matters."

### 2. Get into the environment (10 min) · *navigate a coding environment*
- Open the webr page. "This is a real coding environment, and you can't break it."
- Introduce the sheep study (heart attacks, stem cells vs control, pumping capacity %).
- Show the data as a **table first** (familiar, spreadsheet-like), then the code cell that loaded it.
- Everyone runs the first cell once (it loads R in the browser). Demystify the editor.

### 3. Clean the data (12 min) · *organize, clean*
- Load the **deliberately messy** version (`data/stem-cell-messy.csv`). Three problems:
  a blank value, an **impossible** `after` of 425 (it's a percent, can't exceed 100; a
  decimal slip from 42.5), and mismatched labels (`Ctrl`, `ctrl `, `esc`, `ESC`, `Esc`).
- Spot-and-fix together: lowercase/trim the labels, drop the blank, drop the impossible value.
- **Takeaway:** real data is messy; cleaning is part of the science. (This is Jamie's home turf.)

### 4. Build the measure: the change score (8 min) · *run a calculation*
- The question is about *recovery*, so compute `change = after - before` (positive = improved).
- This is the key munging move: you build the number you actually analyze.

### 5. Summarize it (8 min) · *run functions, interpret averages & variability*
- Grouped summary: average change + spread (sd) per group.
- "The average is the typical change; the spread tells you how much sheep bounce around."
- Both groups have an average AND a spread. Hold the spread for the stats part.

### 6. Graph it (15 min) · *choose the right graph + create graphs*
- Quick "which chart?": bar vs line vs scatter vs box, matched to data type (30-sec rule of thumb).
- Bad chart vs good chart: one cluttered/3D-pie disaster, then a clean one.
- Build it: **dot plot** (every sheep), then **box plot** (middle 50%), with a line at 0.
- Key point: the groups *overlap*. The stem-cell group improved more, but points cross over.

### 7. Is it real, or luck? — statistical testing (15 min) · *interpret p-values*
- The averages differ. "Does that mean stem cells help, or could chance alone explain it?"
  (We weigh evidence; we don't *prove*.)
- Card-shuffle intuition: shuffle the group labels, re-deal, recompute the difference. Chance
  makes differences too. Computer does it 1,000× (**webr + `infer`**), plot the null
  distribution, **shade where the real difference falls.**
- Name it: that's a **t-test** (run one-sided, same direction as the shuffle), and the shaded
  area is the **p-value**. Small p = hard to explain by chance alone. Two honest warnings:
  small p ≠ big/important; a p-value is NOT "the chance I'm wrong" or "the chance it was luck."
  And a simulation p of 0 means "< 1/1000," not zero.

### 8. Bring it home (5 min)
- "For YOUR experiment: get data in, clean it, build your measure, summarize, graph, then
  ask if it's real or luck."
- Tie to their C. elegans / earthworm comparisons. Where to get help: DataSquad / DSC.

---

## Timing flex

| If you have... | Do |
|---|---|
| 60 min | Cut §7 to the card-shuffle intuition only (skip the t-test demo); trim §6 to one chart |
| 75 min | Run as written but keep §7 tight |
| 90 min | Full arc; let students edit a webr cell to compare their own groups |
| Their own data | Use their C. elegans / earthworm data in §3-7 instead of the sheep set, biggest payoff |
| No devices / wifi | Jamie drives the doc on the projector; card-shuffle keeps §7 hands-on |
| Mixed ability / fast finishers | Point advanced students to **§7 "Going further"** (5 graduated challenges with collapsible answers), or the **graded [Practice page](https://jt14den.github.io/neurocamp-stats-viz/practice.html)** for the same challenges as fill-in-the-blanks with instant feedback. Both are **optional, not part of the core 60-75 min**; use for fast finishers or after-session review. They self-pace and self-check while you help others. |

---

## Materials checklist

- [ ] `data/stem-cell.csv` — real sheep stem-cell data (clean)
- [ ] `data/stem-cell-messy.csv` — messy version for the cleaning exercise (§3)
- [ ] `neurocamp-stats.qmd` — the runnable teaching doc (HTML + webr)
- [ ] Slides version (render qmd to revealjs) — optional
- [ ] Index cards + markers for the physical shuffle (§7)
- [ ] Ruler(s) for the optional warm-up game (§1)
- [ ] Projector + the rendered HTML open in a browser
- [ ] Short link to the webr page for students (if they run it themselves)
- [ ] **Run the presenter preflight** (in `instructor-notes.md`) on the room wifi beforehand

---

## Open decisions for Jamie + Tim

- **Scope call:** hands-on data flow first + stats as capstone (recommended) vs. concept-heavy stats talk?
- Confirmed length (60 / 75 / 90)?
- Slides vs. live HTML doc vs. both?
- Do students run webr themselves, or instructor-drives-only? (9-12 + devices → let them)
- Collect live class data, or use the canned CSV?
