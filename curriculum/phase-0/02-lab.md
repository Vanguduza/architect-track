# Lab: draw your harness on paper (then on disk)

You will make the four-part harness visible for **this machine and this repo**. No production systems. No other company’s codebase.

## Setup

Create `C:\architect-track\scratch\` if it does not exist. You will write `scratch/harness.md`.

Open in a browser (do not paste their pages into the repo):

- [Claude Code features overview](https://code.claude.com/docs/en/features-overview)
- [Claude Code IDE integrations](https://code.claude.com/docs/en/ide-integrations)
- [Cursor Docs](https://cursor.com/docs)

## Exercise A — Tool inventory (20 min)

In `scratch/harness.md`, make a table with columns: **Tool**, **Enabled?**, **Needs approval?**, **Danger if wrong**.

Fill it for at least: edit files, run terminal, git, network fetch, MCP (if any), browser tools (if any).

If you do not know an answer, write **UNKNOWN** and how you will find out (Cursor settings, Claude Code `/help`, a dry-run command that cannot delete anything). Unknown is a valid lab result. Fake certainty is not.

## Exercise B — Instruction inventory (15 min)

List every standing instruction you can find:

- Cursor user rules / project rules (if the `.cursor` folder exists later, note that it does not exist yet).
- Anything in a global Claude Code config you actually use.
- The last three prompts you sent to an agent this week (paraphrase; no secrets).

Mark each as **helps Architect Track**, **fights Architect Track**, or **unrelated**.

## Exercise C — Context budget (15 min)

Write a “session packing list” for editing one curriculum lesson:

- Must include
- Nice to include
- Must exclude (other products, huge binary files, credential paths)

Keep the must-include list under **eight** bullets. If you cannot, you are still vibe-packing.

## Exercise D — Model policy (10 min)

Write three bullets: which class of task you will give a cheap/fast model, which you will give a stronger model, and **one task you will not give any model** (you will do it by hand). Example of the last: pasting licensed course text, committing, or inventing lesson IDs that disagree with `catalog.json`.

## Exercise E — One-page harness (10 min)

At the top of `scratch/harness.md`, write a 10-line “default harness” you could paste as the start of a chat this week. It must mention this repo path and `catalog.json`.

## Done when

- `scratch/harness.md` exists and has all four sections (tools, instructions, context, model) plus the 10-line default.
- UNKNOWNs have a verification method.
- You did not enable a new MCP server “for fun” in this lab. (Phase 2 is when you add few, high-value servers.)

## Stop and check (lab)

- If a friend sat at your keyboard, could they see the same tools you listed?
- Did you treat yourself as part of the harness?
- Did you keep other workspaces out of the packing list?
