# Agent Builder Pipeline

A guided workflow for deciding whether an idea deserves an agent — and if it does, producing the spec document needed to build one.

**[Open the tool →](https://brentwarnes-repo.github.io/agent-builder-pipeline/)** *(Note: the hosted GitHub Pages version is currently offline pending review.)*

---

## What this is

A single-page HTML tool that walks you through the front end of an agent-building pipeline. No signup, no backend, no data sent anywhere except optionally to your own GitHub repo at the end.

You answer a few questions. If your idea passes, you fill out a structured spec form. The tool generates a pre-filled markdown spec file you can commit directly to your repo — which is the starting point for a Claude Code session that builds the agent.

---

## What it does

**Stage 1 — Gate filter**

Three questions that kill bad ideas early:

1. Is the task repeatable — same input, same process, every time?
2. Can you describe what "done" looks like in one sentence?
3. Would you run this more than once a week?

All three must be yes. If any gate fails, the tool explains why and lets you download a "parked idea" note to revisit later.

**Stage 2 — Spec builder**

If the idea passes, you fill out a structured form: what the agent does, what triggers it, what it takes as input, what it produces as output, and the completion criteria the build loop will check against.

**Output**

One markdown file: a pre-filled agent spec, ready to commit to your `active/` folder and hand off to Claude Code.

---

## What you need before you start

- A GitHub account and a repo with an `active/` folder
- Basic familiarity with committing files (web UI is fine — no terminal required)
- Claude Code installed, or a plan to validate the prompt layer manually first
- A rough idea you think might be worth building into an agent

The tool assumes you've read the [Agent-Builder Pipeline spec](https://github.com/brentwarnes-repo/ideas) at least once. It implements the pipeline — it doesn't explain it.

---

## How the output fits into the bigger workflow

```
This tool
    ↓
agent spec committed to active/
    ↓
Claude Code session (with /ralph-loop)
    ↓
agent-builder.html builds the agent
    ↓
ship or archive
```

The spec this tool generates is the input to a Claude Code build session. Claude Code reads the spec, builds the prompt layer manually, validates it, adds the Ralph Loop scaffolding, and runs until the completion criteria pass.

---

## What this tool does not do

- It does not build the agent. It produces the spec that a Claude Code session uses to build the agent.
- It does not read your GitHub repo. It only writes to it (one file, one commit, with your explicit permission and your PAT).
- It does not store anything. No accounts, no analytics, no cookies. State lives in the page only — closing the tab clears everything.
- It does not run the agent. That happens in Claude Code.

---

## Technical notes

Single self-contained HTML file. No framework, no build step, no runtime dependencies except one Google Font. Opens in any modern browser. The GitHub push uses the GitHub Contents API with a personal access token you enter — the token is used once and cleared immediately after the call.

---

## Background

Built as part of a personal system for building AI agents quickly. The pipeline spec and build documentation live in a separate repo. This tool is the human-facing intake layer — the part a person actually touches.

The design philosophy: agents that are narrowly scoped are fast to build. The bottleneck is always the front end — deciding if something deserves an agent, and speccing it tightly enough before building starts. This tool removes that bottleneck.

---

## License

MIT
