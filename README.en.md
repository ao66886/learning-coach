# learning-coach · a universal study coach prompt

> A copy-paste prompt / agent skill that turns any LLM into a **study coach that runs a process** instead of an answer machine. Works for any subject: computational, memorization-heavy, skill-based, or mixed.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Prompt](https://img.shields.io/badge/prompt-v2.1-success.svg)](prompt/learning-coach-zh.md)

> 中文版见 [README.md](README.md)。主提示词目前是中文（[`prompt/learning-coach-zh.md`](prompt/learning-coach-zh.md)），本文件是英文精简说明。

---

## The problem

Most "AI tutor" sessions fail because of **process**, not model quality. Five failure modes this repo is built to prevent:

| Failure | Symptom | Fix in this repo |
|---|---|---|
| **No target** | Binge a lecture series from episode 1, find out in week 3 that 40% of it is out of scope | **Exam blueprint** first, curriculum second |
| **Input without output** | "It clicked!" — blank a week later | **Three deliverable artifacts** per session |
| **Resource hoarding** | Three courses, 158 hours total, none finished | **Role-based resourcing**: theory / practice / problem bank / diagnostics |
| **Platform lock-in** | Switch from GPT to Claude, lose all progress | **Learning record card** — state lives outside the chat |
| **Coach decay** | The AI drifts back into Q&A bot mode | 7-point self-check + a correction script |

---

## How it runs

```
① Classify subject type (A computational / B memorization / C skill / D mixed)
        ↓
② Collect 5 inputs (exam date · question sources · textbook · current progress · hours/day)
        ↓
③ Fill the Learning Record Card      ← the only portable state
        ↓
④ Build the exam blueprint (chapter × question no. × marks × phrasing × frequency)
        ↓
⑤ Diagnose: 5 questions, one per layer of the dependency chain
        ↓
⑥ Plan: 4–5 stages in dependency order, each with a verifiable exit criterion
        ↓
⑦ Daily brief (6 items) → grade → variants → update card → back to ⑦
```

Step ④ is the hinge. **Recommendations about "which course is best" should be decided by the exam paper, not by reviews.**

---

## Quick start

```text
1. Open prompt/learning-coach-zh.md and copy the whole ```text block.
2. Paste it into your AI's system prompt / custom instructions
   (not into every message — it needs system-level authority).
3. Replace {{subject}} with your course, then say: 开始  ("start").
```

For agent runtimes (WorkBuddy / Claude Skills):

```bash
git clone https://github.com/ao66886/learning-coach.git
cp -r learning-coach/skill/learning-coach ~/.workbuddy/skills/
```

---

## Six principles (authority order)

1. **Target before study** — the exam paper outranks any course recommendation.
2. **Judgment before calculation** — most marks sit in "decide which case this is"; get the judgment wrong and perfect algebra scores zero.
3. **Output before input** — retention comes from hand-drawing and immediate problem solving, not from "understanding" a video.
4. **Resources play roles, not rankings** — there is no "best course", only a division of labour.
5. **Record card before memory** — no LLM has cross-session memory; portability means externalized state.
6. **Exam-relevant before important** — "important" is not a reason to spend time. "Will be tested" is.

---

## Subject types

| Type | Examples | Blueprint | Core action | #1 killer |
|---|---|---|---|---|
| **A** computational | math, circuits, physics | exam blueprint | derivation from scratch + variants | reading without deriving |
| **B** memorization | medicine, law, history | frequency table | active recall + spaced repetition | familiarity illusion from re-reading |
| **C** skill | programming, speaking, writing | capability + portfolio list | smallest executable task + feedback | watching tutorials only |
| **D** mixed | grad-school subjects, certifications | hybrid | A for skeleton, B for detail | spreading effort evenly |

---

## Feature: Cornell cue card

For people who take Cornell notes. Every session the coach also emits a **screenshot-ready narrow card** for the cue column:

- **Questions only, never answers** — an answer in the cue column defeats the purpose.
- Max **5–7 lines**, ≤10–12 characters each.
- Every line must be tagged with **where it gets tested**; untagged lines get deleted.
- Fixed groups: `①②③ causal chain` / `★ must-answer` / `? stuck  ⊘ skip` / `▣ deliverable`
- Bottom line states the **single pass criterion**.

Usage: cover the right column, self-test from the cue column only. Can't answer → re-derive, don't re-watch.

---

## Repo layout

```
prompt/     full Chinese prompt (main) + condensed English prompt
skill/      SKILL.md for agent runtimes
templates/  record card, exam blueprint, mistake log, weekly quiz, cue card
docs/       usage manual + design notes
examples/   analog-electronics: a complete real-world run of the whole process
```

---

## Limitations

- No cross-session memory in any LLM — you must paste the record card when switching platforms. Designed for, not a bug.
- Heavily dependent on having past papers / a question bank. Without them the coach says so and accepts ~⅓ wasted effort.
- Type A is the most battle-tested (its case study is a circuit-analysis course). Types B and C are generalized inferences — real案例 welcome.

---

## License

[MIT](LICENSE).
