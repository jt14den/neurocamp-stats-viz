# Instructor notes — the stats side, in plain language

**For:** Jamie · **Why this exists:** you've got the data-management half of this lesson
cold (loading, cleaning, munging, summarizing — sections 1-4 are your wheelhouse). This
primer covers the *stats* half (section 5) so you can teach it confidently and answer the
questions students will ask, without needing a stats background.

The good news baked into this lesson: **the simulation (shuffle) approach means you don't
need formulas.** You need the *story*, and the story is below. If you can explain "shuffle
the labels and see if chance can fake it," you can teach this.

---

## Presenter preflight (run through this before class)

Five minutes the morning of, on the actual room wifi if you can:

- [ ] Open the **Lesson** page; run the **first cell** and wait for webR/R to finish loading.
- [ ] Scroll the lesson; run the **shuffle** cell and the **t-test** cell, confirm a plot and
      output appear.
- [ ] Open the **Practice** page (navbar link). Run one exercise **with the blanks still in**
      and confirm it gives a nudge, not a crash.
- [ ] Fill the blanks correctly and confirm it shows **pass/correct** feedback.
- [ ] Confirm the **Hint** and **Solution** buttons appear and work.
- [ ] Confirm the **navbar** moves between Lesson and Practice.
- [ ] If wifi is weak or webR is slow for 30 machines at once: switch to **projector-driven
      mode** (you drive the doc) and run the **card-shuffle** demo by hand. See `lecture-plan.md`.

---

## Teaching what you don't know (this is an advantage)

Borrowed from Therese Huston's book *Teaching What You Don't Know*. Neither of us is a
statistician, and that is genuinely useful here, not a liability. Lean into it.

- **You only need to be a week ahead, not an expert.** Mastery is not the bar. A clear
  mental model one layer deeper than what you teach is plenty. Prepare the *next* question,
  not the whole field.
- **You don't have the expert's blind spot.** People who've known stats for 20 years have
  forgotten what's confusing about a p-value. You haven't. Your fresh confusion is a map of
  where students will get stuck. When something tripped *you* up this week, slow down there,
  that's the spot that trips them up too.
- **Model being a learner, out loud.** "I had to look this up myself" and "here's how I made
  sense of it" are powerful. You're showing them how a smart adult learns something new,
  which is half of what NeuroCamp is really about.
- **"I don't know, let's find out" is a strong move, not a weakness.** When a question lands
  outside your depth: say so, then either reason through it together, run it as a quick
  experiment in the code, or write it down and follow up. Confident bluffing is the only
  real failure mode. (The FAQ below pre-loads the common ones so this happens less.)
- **Let the students and the data do the work.** Your job is to run a good activity, not to
  perform expertise. The shuffle demo, the "find the 3 problems" hunt, the live plots, these
  carry the learning. You narrate and ask questions. This is exactly why active learning is
  the non-expert teacher's best friend.
- **Lower the stakes, for you and them.** You're the lead learner in the room, not the
  oracle. That framing takes the pressure off and makes it safe for students to be confused
  too.

Net: teach from curiosity, not authority. Being one week ahead with a still-forming mental
model is a feature of this lesson, not a bug.

### Two moves baked into the doc (from CourseKata, UCLA-rooted)

CourseKata is a respected intro stats curriculum (co-created by Jim Stigler at UCLA). Two of
its ideas are built into this lesson, so just lean on them:

- **It's all about explaining variation.** The framing question is "why aren't all the
  values the same?" The average is our **best guess** for a group; the spread is the
  **leftover** that guess misses. The stats question is just: does knowing the group shrink
  that leftover by more than luck would? You don't need to say it that formally, but that's
  the thread.
- **Predict before every reveal.** The doc has "Predict first" callouts before the summary,
  the plot, and the shuffle. Always make students commit to a guess before you run the cell.
  This is the single highest-value teaching move in the lesson, and it works *because* you're
  not lecturing, the prediction is.

---

## The one idea everything hangs on

> Two groups almost always have different averages. The real question is whether the
> difference is **bigger than what random luck would produce.**

Everything in section 5 is a way to answer that one question. Hold it in your head and the
rest follows.

---

## Concepts, teacher depth

### Average and spread
- **Average (mean):** the typical value. Students know this.
- **Spread (standard deviation, `sd`):** "how bouncy the numbers are around the average."
  Two groups can have the same average but very different spread. Spread is *why* we can't
  just compare averages and call it a day — a difference in averages might be drowned out
  by how much individuals bounce around.
- Plain words for `sd`: roughly, the typical distance of a data point from its group's average.

### Sampling variability (why random groups still differ)
- If you split the room by coin flip into two groups and measure anything, the two
  averages will **not** be exactly equal. Random groups differ a little, by luck alone.
- So when our real groups (stem cells vs control) differ, the honest question is: is this
  more than that everyday random wiggle?

### The shuffle / permutation test — THE key move
This is the heart of the lesson. Logic, step by step:

1. **Suppose the treatment doesn't matter at all** (stem cells vs control makes no
   difference). Then the labels `esc` and `ctrl` are meaningless tags, and we could swap
   them around and nothing real would change.
2. So **shuffle the labels** randomly onto the data and recompute the difference in averages.
   That difference is **pure luck**, because we just destroyed any real connection.
3. Do that **1000 times.** You get a whole pile of "differences luck can produce." That
   pile is the **null distribution** — literally, "what the world looks like if the cue
   does nothing."
4. Now drop in **our real difference.** If it lands way out past the pile, chance almost never
   makes a gap that big → that's **evidence the treatment may matter**. If it lands inside the
   pile, chance makes gaps like this all the time → **not strong evidence** either way.

That's it. No formula. The picture *is* the argument.

### The p-value
- **Plain definition:** the fraction of those shuffles that produced a difference as big as
  (or bigger than) our real one. "Out of 1000 luck-runs, how many matched or beat reality?"
- If 10 of 1000 shuffles beat reality, p = 0.01 → chance rarely does this → strong evidence
  against a chance-only explanation.
- If 400 of 1000 do, p = 0.40 → chance does this constantly → not much evidence either way.
- **The shaded area in the plot is the p-value.** That visual is your best teaching tool.
- **A simulation p-value can't be literally 0.** With 1000 shuffles, if none beat the real
  result, report it as "less than 1 in 1000," not "p = 0." (Same point applies if a student's
  Challenge 3 code returns `0`.)

### The t-test (and why it's one-sided here)
- Scientists don't shuffle cards every time. The **t-test** is a formula-based version of the
  same comparison. It's a shortcut, not a different question.
- For our purposes: run it, point at the p-value. You do **not** need to explain the formula,
  t-statistic, or degrees of freedom. If a sharp student asks, "it's a math shortcut for the
  shuffle we just did" is honest and sufficient.
- **Design choice (Option A): the shuffle and the t-test are both run one-sided, in the same
  direction** ("did stem-cell sheep improve *more* than control?"). In the code the groups are
  ordered stem-cell-first (`factor(levels = c("esc","ctrl"))`) and the t-test uses
  `alternative = "greater"`, so its p-value lines up with the shuffle's. Student-facing line:
  "because our question is whether stem-cell sheep improved *more*, we look in that direction."
  Don't over-teach one- vs two-sided. (If you'd rather skip it, treat the t-test as optional
  and lean on the shuffle, which is the main idea.)

---

## The two honest warnings (know these cold — students and adults get them wrong)

1. **A small p-value does not mean the effect is big or important.** It's evidence against a
   chance-only explanation, nothing more. With enough data (or duplicated rows, see Challenge
   4) a tiny difference can have a small p-value. Importance is about the *size* of the
   difference (e.g. a few percentage points), not the p-value.
2. **A p-value is not "the chance I'm wrong," and not "the chance the result was due to
   luck."** It's "if there were truly no effect, how often would chance alone fake a result
   this extreme?" The everyday wrong version ("p = 0.05 means 5% chance the result is wrong")
   is false; don't say it.

You don't need to lecture these. Just don't teach the myths, and if they come up, you have
the correct version here.

---

## The "Going further" challenges (§7) — for advanced students

The doc ends with 5 graduated challenges, each with a **collapsible solution** so students
try first and self-check. Point fast finishers there and keep teaching the rest of the room;
you don't have to work these live. What each one teaches, so you can nudge or discuss:

| Challenge | The deeper idea |
|---|---|
| 1. How big is the effect? | Significance ≠ size. Effect size vs p-value. |
| 2. Did groups start the same? | Why randomization / baseline checks matter. |
| 3. Compute the p-value yourself | Demystifies the p-value: it's just counting the tail. |
| 4. Does more data change it? | p-values depend on sample size (the big "aha"). |
| 5. Skeptic's check (median) | Robustness: does the result survive a different choice? |

Two things to flag if they come up: **Challenge 4 is a toy demo** (copying rows is not real
new evidence; only more *independent* observations count), and a simulation p-value of `0`
means "less than 1 in 1000," not zero.

If a strong student finishes everything, the natural open-ended extension is "bring your own
camp data and run the whole pipeline on it." That's the real win.

There's also a **graded [Practice page](https://jt14den.github.io/neurocamp-stats-viz/practice.html)**:
the same five challenges as fill-in-the-blank exercises that auto-check the answer and give
feedback, with Hint and Solution buttons. It's **optional**, for fast finishers, after-session
review, or your own preflight, not something every student must finish. (Built with
quarto-live; the main lesson stays on quarto-webr.)

## Speaking to the spreadsheet crowd

Many students will be more comfortable in Excel/Sheets, and that's an opening, not a problem.
The doc maps each R step to its spreadsheet equivalent ("Same idea in a spreadsheet" asides):
cleaning = Find & Replace + filter/delete; `mutate()` = a calculated column; `group_by()` +
`summarise()` = a PivotTable. This is your data-management home turf, so narrate it from
experience. The honest "why code, not Excel?" answer (at the shuffle in section 5): you *can*
do the early steps in a spreadsheet, but code **remembers every step** (reproducible) and
makes **simulations** like the shuffle easy. Excel is genuinely fine for a quick look at small
data. Don't oversell code; sell the *transferable pipeline* (load, clean, restructure,
summarize, analyze) that's the same everywhere.

## Narration script for the shuffle demo (say this)

Use index cards (one sheep's change score + its label per card) on the projector, then the
webr cell.

1. "Here's our real result: the stem-cell sheep improved by about 8 points more than the
   control sheep, on average."
2. "Maybe stem cells really help. Or maybe we just got a lucky split. How do we tell?"
3. "Let's pretend the treatment did nothing. If that's true, these labels are meaningless."
   *(shuffle the cards, re-deal into two piles)*
4. "New difference. That's a difference luck made. Let's do it again." *(repeat 2-3 times,
   jot the numbers)* "Already they're bouncing around zero."
5. "The computer does this 1000 times instantly." *(run the `infer` cell)*
6. "This pile is every difference luck can make. Now here's our real result." *(point at the
   red line)* "Is it out in the tail, or buried in the pile?"
7. "That shaded bit has a name: the p-value. Small p, way out in the tail, hard to explain
   by chance. That's all a p-value is."

---

## Likely student questions + confident answers

- **"What counts as a good p-value?"** "By convention people use 0.05 as a rough line, but
  it's a convention, not a law. Smaller means stronger evidence against 'it's just luck.'"
- **"Why 0.05?"** "History and habit, honestly. It's a common cutoff, not a magic number.
  A p of 0.049 and 0.051 are basically the same evidence."
- **"What if p is just above 0.05?"** "Then we don't have strong evidence — but it's not
  'nothing happened.' It means this experiment couldn't tell. Maybe more data would."
- **"Does a small p mean the difference is big?"** "No — separate questions. p says 'hard to
  explain by chance.' The size of the gap (a few points) says 'how much it matters.' Always
  look at both."
- **"Can a p-value be zero?"** "No. A simulation p-value of 0 just means none of our 1000
  shuffles beat the real result, so it's smaller than we can measure. Report it as < 1/1000."
- **"What's the difference between the shuffle and the t-test?"** "Same question, two methods.
  The shuffle simulates chance directly; the t-test is a formula that estimates the same
  answer. We run them in the same direction here, so they agree closely."
- **"What's standard deviation again?"** "Roughly how far a typical data point sits from its
  group's average — how spread out the numbers are."
- **"Can we prove stem cells work?"** "We never 'prove' in stats. We say the difference is
  hard to explain by chance alone, which is evidence the treatment may matter. Science deals
  in evidence, not proof."

---

## If you want to go deeper before the 25th (optional, all beginner-friendly)

- **StatQuest with Josh Starmer** (youtube, statquest.org) — short, friendly videos on
  "p-values" and "the t-test." Best single resource for exactly this gap. Start there.
- **Seeing Theory** (seeing-theory.brown.edu) — animated, interactive hypothesis testing
  and sampling distributions. Great for seeing the null distribution move.
- **ModernDive** (moderndive.com) — the free book this lesson's approach comes from;
  the "Hypothesis Testing" chapter walks the exact shuffle → p-value logic in R.
- **infer package site** (infer.tidymodels.org) — the package the lesson uses; the
  "Getting started" vignette mirrors our code.

You won't need any of this to teach the lesson. It's here if you want to feel even more solid.

---

## Division of labor suggestion

Given your strengths, a natural split if you want to lean in gradually:
- **Lead with confidence:** sections 1-4 (get data in, clean it, summarize, graph) — your
  data-management home turf. Narrate the cleaning from experience; students benefit from
  hearing a real practitioner talk about messy data.
- **Teach from the story:** section 5 — use the card shuffle + the script above. The
  simulation does the heavy lifting; you're the narrator, not the mathematician.
- This is the teach-to-learn part. After running it once, the p-value will feel like yours.
