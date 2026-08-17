# The agent harness

**Read time:** about 10 minutes.

You do not “use AI.” You assemble a **harness**: the bundle of instructions, tools, context, and model that turns a vague human into a constrained worker. When the bundle is sloppy, you get vibe coding. When the bundle is explicit, you get something closer to a junior engineer with a very fast keyboard and no memory between shifts.

Claude Code’s public overview describes a productized version of this idea — an agent with tools in a real environment, not a chatbot in a vacuum. Read [Claude Code features overview](https://code.claude.com/docs/en/features-overview) as the vendor’s picture. This guide is the portable picture you will keep even if you switch IDEs.

## Four parts, always

Memorize the tuple. Every session has all four, even if you never named them.

### 1. Instructions

Instructions are **standing orders**: system/developer text, project rules, `AGENTS.md`, your user prompt, and any skill file the agent was told to follow.

Good instructions are **local and falsifiable**. “Be careful” is not an instruction. “Do not edit `curriculum/catalog.json` unless a `guidePath` is missing on disk” is an instruction.

Bad instructions fight each other. If one rule says “always write tests” and another says “never add files,” the model will pick whichever is closer in the prompt. You will think it disobeyed you. It resolved a contradiction.

You will spend Phase 2 making instructions modular (rules vs skills vs MCP vs hooks). For Phase 0, only learn to *see* them: open the rules the IDE injects, read what you pasted, and ask “would I give this same paragraph to a new hire on day one?”

### 2. Tools

Tools are **verbs with side effects**: read file, apply patch, run shell, search, talk to an MCP server, open a browser.

An agent without tools can only talk. An agent with a shell can destroy a git repo, leak a `.env`, or install a package you did not want. The harness is not complete until you know **which tools are enabled** and **what approval looks like**.

Cursor documents the product surface in [Cursor Docs](https://cursor.com/docs). Claude Code documents CLI/IDE tool use in the [features overview](https://code.claude.com/docs/en/features-overview) and [IDE integrations](https://code.claude.com/docs/en/ide-integrations). You should know, for your setup:

- Can it run terminal commands without asking?
- Can it change files outside the workspace?
- Can it call network MCP servers?

If you cannot answer those, you do not have a harness. You have a hope.

### 3. Context

Context is **what the model can attend to right now**: open files, @-mentions, search hits, conversation history, retrieved rules, screenshots, terminal output.

Context is not “the truth of the repo.” It is a **budget**. Stuffing the whole monorepo into the window does not make the agent omniscient; it makes the important sentence compete with noise. Community write-ups of people switching between Cursor, Claude Code, and other tools keep rediscovering the same pain: the limiter is not IQ, it is **what still fits after three refactors of the prompt**. See [Dredyson’s context-management journey](https://dredyson.com/my-ai-coding-tools-context-management-journey-what-i-learned-after-6-months-of-switching-between-claude-code-cursor-and-codex-without-losing-my-mind/) as a field report, and [Real Python on context engineering](https://realpython.com/python-context-engineering-ai/) for a structured take in another language ecosystem.

Your job is to put **the source of record** in the window (for this app: `catalog.json`, the lesson file you are editing, `ATTRIBUTION.md` when licenses matter) and to keep **irrelevant product memories** out (other companies’ ERPs, yesterday’s abandoned spike).

### 4. Model

The model is the **stochastic engine**. Different models trade cost, latency, tool-use reliability, and taste. The harness includes the *choice*: a cheap model for “rename a heading,” a stronger one for “design the export format.”

Swapping the model without changing instructions, tools, or context is a common superstition. If the contract is missing, a smarter model writes a more confident wrong patch.

## The user is inside the harness

You are not standing outside this system. Your habits are instructions. Your “sure, whatever” is a tool permission. Your four-hour chat is context rot. Your panic-switch to a different model is a harness change.

Treat a session like a small production system:

- **Input:** the contract (Phase 0 lesson 1).
- **Runtime:** tools + context + model.
- **Output:** a diff plus evidence (test, grep, screenshot).
- **Supervisor:** you, with a stop policy (next lesson).

Vendors will keep adding buttons. The tuple stays.

## Harness anti-patterns

**Invisible instructions.** You have user rules in the IDE you forgot about. The agent “mysteriously” refuses to write Android code in a curriculum-only task — or worse, it *does* write it because a stale rule said “always implement.” Read your rules.

**Unbounded tools.** Full-auto shell on a repo that contains credentials is not productivity. It is an unattended intern with sudo.

**Nostalgic context.** You @-mention a huge unrelated folder “for inspiration.” The model copies architecture from the wrong planet.

**Model roulette.** You retry the same bad prompt on three models and pick the prettiest. You have not improved the harness; you have sampled it.

## A harness sketch for Architect Track

When you work in `C:\architect-track`, a sane default harness looks like this:

- **Instructions:** curriculum files are original; do not paste NC-licensed course text; `catalog.json` IDs are stable; no commits unless you ask.
- **Tools:** file edit in `curriculum/` and maybe `scratch/`; no production deploy; no touching other workspaces.
- **Context:** the lesson you are writing, `catalog.json` excerpt, `ATTRIBUTION.md` when citing.
- **Model:** whatever you trust for prose vs code — but the *same* contract.

You will encode this in `AGENTS.md` and `.cursor/rules` in Phase 2. For now, keep it on paper in the lab.

## Stop and check

- You can list the four harness parts without looking.
- You can point to one standing instruction in your IDE and say whether it helps this repo.
- You know which tools can mutate git or the network in your setup (if unsure, you will verify in the lab).
- You can explain why “just use a smarter model” does not fix a missing contract.
- You treat yourself as part of the harness, not as a spectator.

## Citations and links

- [Claude Code — features overview](https://code.claude.com/docs/en/features-overview)
- [Claude Code — IDE integrations](https://code.claude.com/docs/en/ide-integrations)
- [Cursor Docs](https://cursor.com/docs)
- [Cursor Learn](https://cursor.com/learn)
- [Anthropic — agent skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) (how instructions get packaged; deeper in Phase 2)
- [Dredyson — context management across tools](https://dredyson.com/my-ai-coding-tools-context-management-journey-what-i-learned-after-6-months-of-switching-between-claude-code-cursor-and-codex-without-losing-my-mind/)
- [Real Python — context engineering](https://realpython.com/python-context-engineering-ai/)
