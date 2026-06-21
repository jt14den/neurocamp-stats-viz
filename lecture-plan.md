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

## Elena's brief & learning objectives

Elena's formal request asks for two topics — **Statistical Testing** and **Making Graphs
& Data Visualization** — but the *learning objectives* she listed are broader and lean
hands-on. Mapping each to where this session covers it:

| Elena's objective | Where it's covered | Depth |
|---|---|---|
| Understand *why* scientists use statistics | §1 hook, §6 the chance problem | Core |
| Interpret basic results (p-values, averages, variability) | §5 summarize, §7 stat test | Core |
| Choose the right type of graph for the data | §6 graph it | Core |
| Navigate a spreadsheet / coding environment with confidence | §2 get in the environment | Core |
| Enter, organize, and clean data | §3 enter & clean | Core |
| Run simple calculations/functions to summarize | §5 summarize | Core |
| Create basic graphs/charts from their data | §6 graph it | Core |

### ⚠️ Scope reality (read this first)

Seven objectives, four of them hands-on data skills, in 60-90 min with kids who may have
**never opened a spreadsheet or coding tool** (these are students from schools without
university science access). You cannot do all seven *deeply*. Recommendation:

- **Anchor on the hands-on flow** — *get into the tool → enter/clean data → summarize →
  graph* — because that's 4 of the 7 objectives and builds the confidence Elena names.
- **Keep the statistical-testing piece as the satisfying capstone**, lighter on mechanics.
  The "shuffle test" stays as the intuition for p-values, but don't belabor t-test math.
- If forced to cut: drop the formal t-test demo (§7) before cutting the hands-on flow.
  The "is it real or luck?" intuition matters more than the `t.test()` output for this age.

This is the single decision to confirm with Elena/Jamie: **hands-on data literacy first,
statistical testing as the payoff** — vs. a more concept-heavy stats talk. Plan below
assumes the former.

---

## Big idea (the one thing they should leave with)

> You can take real data, put it into a tool, make a picture of it, and ask:
> **is the difference between two groups real, or just luck?**
> Scientists answer that with a p-value — and now you've done it yourself.

---

## Theme: reaction time

NeuroCamp = brains + experiments, so we use a **reaction-time experiment** as the running
example. It's hands-on, relatable, produces data students can *enter themselves*, and
mirrors the two-group comparisons they've already made at camp (C. elegans habituation,
earthworm treatments).

Example question: **"Do people react faster to a sound than to a flash of light?"**

---

## Session arc (built for ~90 min; 60/75 trims below)

### 1. Hook — play the game (10 min) · *why stats*
- Live reaction-time activity: ruler-drop catch in pairs, or a reaction-time site on the projector.
- Collect numbers from volunteers into two groups. Write them on the board.
- Point: "Everyone's different. Even the *same* person differs each try." **Measurements vary.**

### 2. Get into the environment (10 min) · *navigate a coding environment*
- Open the webr page. "This is a real coding environment — and you can't break it."
- Show the data as a **table first** (familiar, spreadsheet-like), then the code cell that made it.
- Everyone runs the first cell once (it loads R in the browser). Demystify the editor.

### 3. Enter & clean the data (15 min) · *enter, organize, clean*
- Students type the class's collected reaction times into a data cell and run it.
- Then hand them a **deliberately messy** version (`data/reaction-time-messy.csv`): a blank
  cell, a typo (2300 ms from a misplaced decimal), an inconsistent label ("Sound" vs "sound").
- Spot-and-fix together: why a 2300 ms value wrecks the average, why labels must match.
- **Takeaway:** real data is messy; cleaning is part of the science.

### 4. *(moved into §6/§7 — see graph + summarize)*

### 5. Summarize it (10 min) · *run functions, interpret averages & variability*
- Run `mean()`, then a grouped summary: average + spread (sd) per group.
- "The average is the typical value; the spread tells you how much they bounce around."
- Both groups have an average AND a spread — hold the spread for the stats part.

### 6. Graph it (15 min) · *choose the right graph + create graphs*
- Quick "which chart?" — bar vs line vs scatter vs box, matched to data type (30-sec rule of thumb).
- Bad chart vs good chart: one cluttered/3D-pie disaster, then a clean one.
- Build it: **dot plot** (every point), then **box plot** (middle 50%), means marked.
- Key point: the groups *overlap*. Averages differ, but points cross over.

### 7. Is it real, or luck? — statistical testing (15 min) · *interpret p-values*
- The averages differ. "Does that prove sound beats light?"
- Card-shuffle intuition: shuffle the group labels, re-deal, recompute the difference. Luck
  makes differences too. Computer does it 1,000× (**webr + `infer`**), plot the null
  distribution, **shade where the real difference falls.**
- Name it: that's a **t-test**, and the shaded area is the **p-value**. Small p = hard to
  explain by luck. Two honest warnings: small ≠ important; p is not "chance I'm wrong."

### 8. Bring it home (5 min)
- "For YOUR experiment: get data in → clean it → summarize → graph → ask if it's real or luck."
- Tie to their C. elegans / earthworm comparisons. Where to get help: DataSquad / DSC.

---

## Timing flex

| If you have... | Do |
|---|---|
| 60 min | Cut §7 to the card-shuffle intuition only (skip the t-test demo); trim §6 to one chart |
| 75 min | Run as written but keep §7 tight |
| 90 min | Full arc; let students edit a webr cell to compare their own groups |
| Their own data | Use their C. elegans / earthworm data in §3-7 instead of the canned CSV — biggest payoff |
| No devices / wifi | Jamie drives the doc on the projector; card-shuffle keeps §7 hands-on |

---

## Materials checklist

- [ ] `data/reaction-time.csv` — clean dataset (swap with live class data if collected)
- [ ] `data/reaction-time-messy.csv` — messy version for the cleaning exercise (§3)
- [ ] `neurocamp-stats.qmd` — the runnable teaching doc (HTML + webr)
- [ ] Slides version (render qmd to revealjs) — optional
- [ ] Index cards + markers for the physical shuffle (§7)
- [ ] Ruler(s) for the ruler-drop game (§1)
- [ ] Projector + the rendered HTML open in a browser
- [ ] Short link to the webr page for students (if they run it themselves)

---

## Open decisions for Jamie + Tim

- **Scope call:** hands-on data flow first + stats as capstone (recommended) vs. concept-heavy stats talk?
- Confirmed length (60 / 75 / 90)?
- Slides vs. live HTML doc vs. both?
- Do students run webr themselves, or instructor-drives-only? (9-12 + devices → let them)
- Collect live class data, or use the canned CSV?
