# Why vibe coding fails at scale

**Read time:** about 8 minutes.

You already know the loop. You type a wish into the chat. The model paints a diff across five files. You click accept because the UI looks finished. For a weekend toy, that can feel like magic. For anything that has to survive a second week of changes, it is how you quietly bankrupt the codebase.

This lesson is not “never use an agent.” You will use agents constantly in this track. The point is to name the failure mode so you can refuse it on purpose.

## What “vibe coding” means here

Vibe coding is **intent without a contract**. You describe a feeling (“make search nicer,” “add export,” “fix the crash”) and treat the model’s first plausible patch as the design. There is no written invariant, no test that can fail, no owner of the architecture, and no moment where you predict the diff before you see it.

The wish is not a spec. A spec says what must stay true after the change. A wish says what you hope to feel when you tap the screen.

Agents are extremely good at satisfying wishes in the local sense: they produce code that compiles, screens that render, and commit messages that sound responsible. They are weak at protecting **cross-file laws** you never stated: money rounding, offline queues, “do not rewrite this parser,” “this JSON shape is loaded by the Android app.”

## Why the loop works on Tuesday and dies on Thursday

Three properties of language models collide with real software.

**1. The model optimizes for looking done.**  
Your prompt is graded, in effect, by whether the assistant produced a complete-looking answer. Incomplete-looking honesty (“I need the schema and a failing test first”) scores worse in the chat UI than a bold rewrite. So the default policy is: touch more files than necessary, invent helpers, and leave TODOs that read like progress.

**2. Your context window is not the repository.**  
The agent sees a slice: open tabs, a rules file if you attached one, whatever search returned. Scale is not “more files on disk.” Scale is **more invariants than fit in the slice**. The moment the true constraint lives in a file the agent did not read, vibe coding becomes vandalism with syntax highlighting.

**3. Accepting a diff is not the same as understanding it.**  
Git will happily store a 400-line change you could not re-derive. Next week you will ask a *different* chat to “just fix the bug,” and it will compensate for the first chat’s inventions. That is how you get two naming schemes, three JSON loaders, and a catalog that drifts from `catalog.json`.

## What “at scale” actually means

Scale is not microservices. For this repo, scale already means:

- Lesson IDs in `curriculum/catalog.json` must keep matching files on disk.
- The Android shell (when you extend it) will parse that catalog. A renamed `guidePath` is a shipped crash, not a style nit.
- You will run **more than one chat**. Each chat will forget the last chat’s private decisions unless you wrote them down.
- You will be tempted to paste habits from other products you have seen. Those products have different threat models, licenses, and owners.

Vibe coding fails here the same way it fails in a large ERP: **the system has a memory, the chat does not**, and the accept button does not reconcile the two.

## Failure signatures you should start noticing

You are vibe coding when any of these are true:

- You cannot state the before/after in one sentence that a test could check.
- The agent created a new abstraction because the existing one was one directory away.
- You accepted generated UI copy, IDs, or file names that disagree with a source of record you already have (`catalog.json` in this project).
- You said “looks good” without running the command you would run if a human intern had sent the same patch.
- You asked for “the same thing as that other app” instead of naming the behavior you need in *this* tree.

None of these require malice. They are the default.

## The replacement loop (preview)

You will practice the replacement for the rest of Phase 0:

1. **Write the contract** — even six lines: goal, non-goals, files allowed to change, how you will know it worked.
2. **Constrain the harness** — instructions, tools, context, model (next lesson).
3. **Stop on purpose** — loops, red tests, unreadable diffs, human gates (lesson 3).
4. **Publish personal laws** — an “I will not” list you actually follow (lesson 4).

Official product education for the tooling lives at [Cursor Learn](https://cursor.com/learn) and [Cursor Docs](https://cursor.com/docs). Those pages teach the product. This page teaches the *habit* the product will not enforce for you.

## A small example in this repo

Suppose you tell an agent: “Add a lesson about Docker.” A vibe-coded outcome might invent `phase-8/docker.md`, invent a new phase object, and “helpfully” reformat all of `catalog.json`. A contract-coded outcome would say: catalog schema is frozen unless the lesson is added with a stable `id`, matching `guidePath`/`labPath` files, and no drive-by pretty-print of unrelated phases.

The difference is not intelligence. It is **whether you made the frozen parts visible** before the first tool call.

## What you are training yourself out of

You are not training yourself out of speed. You are training yourself out of **unearned speed**: the kind that moves complexity from the chat into next month’s debugging.

If you only remember one sentence from this guide, make it this: **a wish is an input; a passing check is an output; a diff is a hypothesis.** Treat the accept button like merge authority, not like a skip button on a tutorial.

## Stop and check

- You can explain vibe coding without using the word “stupid” — it is a missing contract, not a moral failing.
- You can name two invariants in *this* repo that a random chat would not know unless you said them.
- You can tell the difference between “the UI looks done” and “I could re-derive this patch.”
- You know where official Cursor education lives, and that this guide is not a substitute for it.
- You are willing to reject a fluent diff this week in order to keep the catalog honest.

## Citations and links

- [Cursor Learn](https://cursor.com/learn)
- [Cursor Docs](https://cursor.com/docs)
- [Cursor Forum](https://forum.cursor.com) — community reports of what breaks in long sessions (read as anecdotes, not spec).
- Context-switching across tools, first person: [Dredyson on context management](https://dredyson.com/my-ai-coding-tools-context-management-journey-what-i-learned-after-6-months-of-switching-between-claude-code-cursor-and-codex-without-losing-my-mind/)
- [Real Python — context engineering](https://realpython.com/python-context-engineering-ai/) (Python-flavored; the *idea* of packing the right facts transfers).
