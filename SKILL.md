[SKILL.md](https://github.com/user-attachments/files/33345220/SKILL.md)
---
name: session-handoff
description: Use when the user wants to package a whole conversation so a fresh chat can continue exactly where this one left off — e.g. "/handoff", "bu sohbeti paketle", "devam paketi çıkar". Produces one self-contained text block: purpose, goals, decisions, current state, and the latest valid version of any code written in the session (not every draft).
---

# Session Handoff

Package the current conversation into a single, paste-ready block of text that lets a brand-new chat resume work with zero loss of context. This is NOT a summary — it carries the actual working material (goals, decisions, live code) so the next session starts from the real state, not a description of it.

## When to use

- The user explicitly asks to package / hand off / continue-elsewhere the current chat ("/handoff", "bu sohbeti paketle", "devam paketi", "yeni sohbette devam edeceğim").
- A long working session (code, planning, decisions) is about to be moved to a fresh chat.

Do NOT trigger for a plain "summarize this" — a handoff is heavier and carries full code.

## Core principle: smart, not blind

Never dump the whole transcript. The value is in **de-duplication**:

- If a file/function was revised several times, keep **only the latest valid version**. Drop every superseded draft.
- Approaches that were tried and abandoned do NOT go into the code. They get **one line** in Decisions ("tried X, dropped because Y") so the next session doesn't repeat the mistake.
- Half-finished / revision-pending code stays, but gets flagged ("needs rework at …").
- Untouched files (part of the project but not changed/discussed this session) are NOT pasted — they go in a **map** (filename + one-line role). Each map entry should name **where the full version lives** (repo URL + path, or disk path) so the next session can fetch it if it ever needs the real code. The point is a small package that loses nothing: live code inline, everything else reachable by pointer.

When you genuinely can't tell which version is current, keep the most recent one and add a `⚠ verify` note pointing at it — don't guess silently.

## Output structure

Produce ONE text block, in the conversation's language, with these sections (omit a section only if truly empty):

1. **Amaç (Main purpose)** — what the project is, why, what "done" looks like.
2. **Hedefler (Goals)** — short- and long-term goals, success criteria.
3. **Şu an neredeyiz (Current state)** — what's finished, what's in progress, what was done most recently.
4. **Kararlar (Decisions)** — chosen tech/approaches + the reason each was chosen (so they don't get relitigated). Include one-liners for abandoned approaches.
5. **Kod (Code)** — the latest valid version of every active file, **full text, uncut**. Each block headed by its filename/path. Reference-only dead code becomes a map line, not a paste.
6. **Açık sorular / Sıradaki adım (Open questions / Next step)** — the single first thing the new session should do, plus unresolved questions.
7. **Kısıtlar & tercihler (Constraints & preferences)** — rules to respect ("don't use X", formatting/style rules, language).

End the block with a one-line instruction aimed at the next session, e.g.:
> Bu paket bir devam bağlamıdır. Oku, mevcut durumu benimse, "Sıradaki adım"dan devam et.

## Rules

- **Code is full text**, not paraphrased — a handoff that trims code is broken.
- Keep only the current version of each file; superseded drafts are removed.
- Preserve the user's stated constraints/preferences verbatim in meaning.
- If the packaged block gets very large, keep it as one block anyway (completeness beats brevity), but make sure no dead/duplicate code is inflating it.
- Put `⚠ verify` flags wherever version/state is ambiguous, so the user can spot-check before relying on it.
- Keep real secrets (keys, tokens, `.env` values) OUT of the package entirely. Real target/scope names (domains, hosts) are kept by default since the next session may need them, but add a one-line warning that they're present in case the package will be shared publicly.
