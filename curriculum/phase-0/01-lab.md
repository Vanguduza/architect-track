# Lab: catch a wish before it becomes a bad diff

You will practice converting a vibe into a contract using **this repo only**. Do not open some other company’s application and “improve” it. If you want a throwaway tree, use `C:\architect-track\scratch\` (create it) and keep secrets out of git.

## Setup

1. Open `C:\architect-track` in Cursor.
2. Read `curriculum/catalog.json` far enough to see how a lesson is described: `id`, `guidePath`, `labPath`, `officialDocUrl`.
3. Skim [Cursor Learn](https://cursor.com/learn) for ten minutes so you know what the product thinks “Agent” is. Then come back here.

## Exercise A — Inventory invariants (15 min)

In `scratch/invariants.md` (create the folder if needed), list at least **eight** facts that must remain true for the learning app to work. Write them as checkable sentences, for example:

- Every lesson `guidePath` is a file under `curriculum/`.
- Lesson `id` values are stable; renaming one is a product change, not a cleanup.
- You do not paste Full Stack Open or Odin lesson bodies into this tree.

Add two invariants that are *social*, not technical (license, “this is not the Nissan ERP,” no production secrets).

## Exercise B — Wish vs contract (20 min)

Pick **one** of these fake wishes. Do **not** implement it yet.

- “Make the catalog nicer.”
- “Add a quiz after every lesson.”
- “Support offline video.”

Write `scratch/wish-vs-contract.md` with two sections:

1. **Wish** — one paragraph, sloppy on purpose (how you would have typed it six months ago).
2. **Contract** — goal, non-goals, files the agent may touch, files the agent must not touch, and a verification step you could run without the model (open a file, grep, run a command).

Your contract must mention `catalog.json` if the feature would change navigation.

## Exercise C — Predict the vibe-coded failure (15 min)

Still without running an agent: write five bullets under **Predicted vibe failures** — what a helpful model would likely invent (new folders, renamed IDs, extra dependencies, “temporary” duplicate JSON).

Then write the **smallest human-readable check** that would catch each failure (grep for an `id`, count markdown files, diff against git).

## Exercise D — Optional dry run (only if you already use Agent mode)

If you use Cursor Agent: paste **only the contract**, not the wish, and ask the agent to *critique the contract* without writing code. If it starts editing files, stop it. Note what it assumed. That note belongs in `scratch/wish-vs-contract.md`.

## Done when

- `scratch/invariants.md` has eight or more checkable facts.
- `scratch/wish-vs-contract.md` has wish, contract, predicted failures, and checks.
- You did not modify `catalog.json` unless you were fixing a path typo (you should not need to).
- You did not copy lesson text from another course into this repo.

## Stop and check (lab)

- Could a stranger execute your verification steps?
- Did you protect `catalog.json` as a source of record?
- Did you keep the work in `C:\architect-track` or `scratch\`, not in some other product repo?
