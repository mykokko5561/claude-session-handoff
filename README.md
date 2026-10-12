# session-handoff

A Claude skill that packages an entire conversation into a single, paste-ready block — so a **fresh chat continues exactly where the last one left off**.

Not a summary. A continuation context: it carries the real working material — goals, decisions, and the live code — so the next session starts from the actual state instead of a description of it.

## Why

Long working sessions get expensive and lossy. The model starts missing or mixing up earlier details, and every new message reprocesses the whole transcript. The usual fix is to start a clean chat — but then you lose all the context you built up.

`session-handoff` solves that: it distills a long session into a compact, complete package you paste into a new chat. You keep the context, drop the bloat.

## What it produces

One text block, in the conversation's language, with:

- **Main purpose** — what the project is, why, what "done" looks like
- **Goals** — short- and long-term, with success criteria
- **Current state** — what's finished, what's in progress, what was done last
- **Decisions** — chosen approaches and *why* (so they don't get relitigated), including one-liners for abandoned attempts
- **Code** — the latest valid version of every active file, **full text, uncut**
- **Open questions / next step** — the single first thing the new session should do
- **Constraints & preferences** — rules to respect

## Smart, not blind

The value is in de-duplication, not dumping the transcript:

- A file revised many times → **only the latest version** is kept; superseded drafts are dropped
- Dead-end approaches → not pasted as code, just one line in *Decisions* so the next session doesn't repeat them
- Untouched project files → a **map** (name + role + where the full version lives), not a paste — the package stays small while nothing is lost
- Ambiguous state → flagged with `⚠ verify` so you can spot-check before relying on it
- Real secrets (keys, tokens, `.env`) are never included

## Install

This is a Claude skill. This repo is a **backup / shareable / portfolio** copy — it does **not** load into Claude automatically. To use it:

1. Take `SKILL.md`.
2. Register it as a skill in Claude (approve it from the skill-proposal card, or place it in your skill directory).

## Usage

Inside a conversation, trigger it with:

- `/handoff`
- or a plain request like *"package this chat"* / *"make me a handoff"*

Paste the resulting block into a new chat — the new session picks up right where you left off.

## License

MIT
