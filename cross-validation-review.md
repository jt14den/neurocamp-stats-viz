# Cross-validation review — NeuroCamp lesson

A critical pass over `lecture-plan.md` + `neurocamp-stats.qmd` against backward-design
and Carpentries lesson-design principles. Written to find problems, not to approve.

**Date:** 2026-06-20 · For: Tim, Jamie · Audience: NeuroCamp grades 9-12 (~30 students)

---

## Top-line verdict

The lesson is **well themed and honest about scope, but over-packed and under-assessed.**
Two real risks: (1) it tries to teach too many *new tools* (coding env + cleaning syntax +
ggplot + permutation) to first-timers in one hour, and (2) the learning objectives aren't
written as measurable, checkable outcomes, so there's no way to know if students got it.
Both are fixable before June 25. Recommended changes are prioritized at the bottom.

---

## What's working (keep)

- **Relatable, coherent theme.** Reaction time is collectable, intuitive, and maps onto
  their real two-group experiments (C. elegans habituation). Good backward-design instinct.
- **Zero-install via webr** removes the #1 failure mode of teaching R to novices.
- **Scope honesty already in the plan** — the "you can't do all 7 deeply" note is correct.
- **The p-value-as-shaded-area idea** is genuinely good pedagogy: concept before formula.
- **Two honest p-value warnings** avoid teaching the usual myths.

---

## Problem 1 — the learning objectives aren't measurable

Elena's list (and our table mirroring it) uses **unmeasurable verbs**: "understand,"
"navigate ... with confidence." You can't observe "understand." Carpentries/backward
design wants observable verbs (identify, run, create, choose, interpret, fix) so each
objective has an obvious check.

There are also **seven**, which is 2x too many for a single 60-90 min novice session.
Standard guidance: 3-4 objectives you can actually assess.

### Recommended rewrite — 4 core + 2 stretch

Format: "By the end, students will be able to..."

**Core**
1. **Identify** the rows, columns, and variables in a dataset and **run** a cell in a
   browser-based coding environment. *(covers: navigate environment)*
2. **Spot and fix** three common data problems — blanks, impossible values, mismatched
   labels — in a small dataset. *(covers: organize & clean data)*
3. **Calculate** a group's average and spread and **choose + create** an appropriate
   graph (dot/box) to compare two groups. *(covers: run calculations, choose graph,
   create graph, interpret averages/variability)*
4. **Decide and explain**, in plain language, whether a difference between two groups is
   likely real or due to chance, and **locate** the p-value in the output.
   *(covers: why stats, interpret p-values)*

**Stretch (only if time / devices allow)**
5. **Modify** the code to compare a different pair of groups (or their own camp data).
6. **Enter** new data values by hand and re-run the analysis. *(covers: enter data)*

Note: "enter data" is demoted to stretch on purpose — typing data into a code cell is
slow and error-prone for 30 novices and isn't worth the core time. If Elena specifically
wants data *entry*, do it as the live-collection moment (board → one shared cell), not 30
students typing.

---

## Problem 2 — no assessment / checks for understanding

The plan has activities but no **evidence** that objectives were met. Add one quick
formative check per objective (cheap, 30 sec each):

| Objective | Check for understanding |
|---|---|
| 1 (run a cell) | Show of hands / green check after everyone runs cell 1 |
| 2 (clean data) | "Find the 3 problems" call-out before showing the fix |
| 3 (summarize + graph) | Quick poll: "which chart for comparing two groups?" then everyone produces a box plot that runs |
| 4 (real or luck) | Exit question: "p = 0.01 — real or luck? p = 0.40 — real or luck?" thumbs up/down |

Without these, you're lecturing, not teaching to objectives.

---

## Problem 3 — time is the real enemy (biggest risk)

Eight segments + four brand-new tools in 60-90 min, with ~30 novices, is optimistic.
Carpentries rule of thumb: **everything takes ~2x longer with novices**, and live coding
invites typos, lost students, and "it's not working" hands.

Specific time sinks not yet budgeted:
- **webr cold start at scale.** 30 browsers each downloading R + ggplot/dplyr/infer (several
  MB) over classroom wifi, simultaneously, can stall. This alone can eat 10 minutes.
- **Reading cleaning syntax cold.** §3 currently shows `mutate() |> filter() |> tolower()`.
  First-timers cannot read a 3-function pipe yet. If they must *write* it, it will not fit.
- **Permutation is conceptually hard.** The null distribution trips up undergraduates.
  Expecting 9-12 first-timers to author `infer` code is unrealistic.

### Mitigations
- **Make cleaning and permutation instructor-driven** (Jamie types/runs on the projector;
  students watch + answer questions). Keep students' *hands-on* parts to: run a cell,
  read a table, make a box plot, and modify one number. Active learning where it's cheap;
  watch-along where the syntax is heavy.
- **Front-load the webr cold start:** have students open the page and run cell 1 in the
  first 5 minutes (or before the session) so the download finishes while you talk.
- **Test the room's wifi beforehand.** If it can't handle 30 webr loads, switch to
  instructor-drives-on-projector and hand students the card-shuffle as their active task.
- **The card shuffle is your insurance.** It teaches the p-value idea with zero tech and
  zero wifi. Treat it as the primary delivery of objective 4, with the `infer` cell as a
  watch-along confirmation.

---

## Problem 4 — cognitive load / tool count

Four new mental models in one hour: a coding environment, the tidyverse pipe, ggplot
grammar, and resampling inference. Each is a lesson on its own. The fix isn't to teach
them all — it's to let students *operate* pre-written code and spend their attention on
the **ideas** (messy data, overlap, real-vs-luck), not the syntax. The current doc is
close to this already; just be explicit that students run/modify, not author.

---

## Smaller notes

- **Color-only encoding** in the plots (`color = cue`) is fine for a demo but mention it;
  the box plot already adds position, so it's not color-only there.
- **Define "spread"** the first time in plain words ("how bouncy the numbers are") — `sd`
  is otherwise a black box.
- **revealjs slides**: if Jamie wants to present rather than scroll the HTML, budget time
  to make a slide build; the current single-doc renders to HTML well but slides need a pass.
- **Accessibility / reading level:** keep instructions to short imperative sentences; the
  doc is mostly there.

---

## Prioritized changes before June 25

1. **Swap in the 4 measurable objectives** (above) and add the 4 checks-for-understanding. *(high value, low effort)*
2. **Mark §3 cleaning and §7 permutation as instructor-driven**, students run/modify only. *(de-risks time)*
3. **Add a webr cold-start plan** (run cell 1 first; test room wifi; projector fallback). *(de-risks the whole session)*
4. **Pick a target length and cut to fit:** 60 min → core objectives 1, 3, 4 (cleaning becomes a 2-min demo, permutation is card-shuffle only). 90 min → full arc.
5. Confirm with Elena: is hands-on *data entry* required, or is data literacy + interpretation enough? (decides stretch obj 6).

---

## Still Elena's/Jamie's calls

- Hands-on-first vs. concept-heavy stats (recommended: hands-on-first).
- Confirmed length (60/75/90).
- Devices + wifi reality in the room.
- Use their own camp data instead of the canned CSV (biggest payoff if available).
