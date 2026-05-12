---
description: Explain code, plans, or concepts in plain English — short, no jargon, with one example.
argument-hint: <thing to explain — file path, function name, concept, plan section, or free text>
---

# /explain

Your job: explain `$ARGUMENTS` so a non-technical reader understands it.

## Rules

- **Length**: 3–5 sentences total. Never more.
- **Jargon**: avoid. If a technical term is unavoidable, define it inline in 5 words or fewer.
- **One example**: include exactly one concrete analogy OR a tiny real-world scenario. Not both. Not zero.
- **No code dumps**: do not paste the code being explained. Reference it by name only.
- **No meta-commentary**: do not say "this code does X" or "in summary". Just explain.
- **Audience**: imagine a smart product manager or designer with zero codebase knowledge.

## What to resolve `$ARGUMENTS` against

1. If `$ARGUMENTS` looks like a file path → Read the file, then explain its purpose.
2. If `$ARGUMENTS` matches a function/class/symbol → Grep for the definition, then explain its role.
3. If `$ARGUMENTS` looks like a plan section, design doc reference, or PR/diff → read the source, then explain the decision and its impact.
4. If `$ARGUMENTS` is a free-text concept → explain the concept directly.
5. If ambiguous → ask one short clarifying question before answering.

## Output format

Plain prose. No headers. No bullet lists unless the concept genuinely has 2–3 discrete parts. Bold the example sentence so the reader's eye lands there first.

## Examples of good output

> JWT authentication is how the server remembers who you are after you log in. When you sign in, the server hands you a signed sticker (the token) that you show on every later request, so it doesn't have to ask "who are you?" again. **It's like a wristband at a concert — bouncers scan it instead of re-checking your ID at every door.**

> This migration adds a `deleted_at` column to the users table so we can hide accounts without erasing them. Anything with a date in that column is treated as gone by the app, but the data stays on disk for audits and recovery. **Like moving a file to the Trash instead of shredding it — the user disappears from view but we can still pull them back.**

## Examples of bad output (do NOT do this)

- "This function implements a recursive descent parser that tokenizes..." (jargon, too long, no analogy)
- "Basically it just handles auth." (too short, no example, hedging word "basically")
- A 10-sentence paragraph with three analogies.
