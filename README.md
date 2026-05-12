# claude-code-explain

Claude Code `/explain` plugin — turns deep code or dense plans into 3-sentence, no-jargon answers with one concrete example.

Designed for moments where a teammate (PM, designer, new hire, exec) needs to understand *what* a chunk of code or a plan section actually does, without wading through implementation details.

---

## Example

```text
> /explain src/auth/middleware.ts

JWT authentication is how the server remembers who you are after you log in.
When you sign in, the server hands you a signed sticker (the token) that you
show on every later request, so it doesn't have to ask "who are you?" again.
**It's like a wristband at a concert — bouncers scan it instead of re-checking
your ID at every door.**
```

---

## What `/explain` accepts

- **File path** — `/explain src/auth/middleware.ts`
- **Function or symbol** — `/explain validateToken`
- **Plan section or design doc** — `/explain step 3 of the migration plan`
- **Free-text concept** — `/explain why we need a message queue here`
- **PR or diff** — `/explain this PR`

---

## Installation

You have three install options. Pick whichever fits your workflow.

### Option 1 — One-line install (fastest)

Installs only the `/explain` command into `~/.claude/commands/`. No plugin, no clone.

```bash
curl -fsSL https://raw.githubusercontent.com/nasrat-v/claude-code-explain/main/setup.sh | bash
```

Project-local install (only available inside one repo):

```bash
curl -fsSL https://raw.githubusercontent.com/nasrat-v/claude-code-explain/main/setup.sh | bash -s -- --project
```

### Option 2 — Plugin via marketplace (recommended for plugin users)

Inside Claude Code:

```text
/plugin marketplace add nasrat-v/claude-code-explain
/plugin install claude-code-explain@claude-code-explain
```

This is the cleanest path if you already use `/plugin` to manage other extensions — updates, uninstalls, and listing all flow through the same command.

### Option 3 — Manual clone

```bash
git clone https://github.com/nasrat-v/claude-code-explain.git
cd claude-code-explain
./setup.sh             # installs to ~/.claude/commands/
# or
./setup.sh --project   # installs to ./.claude/commands/ in current repo
```

---

## Verifying the install

Open Claude Code and type `/` — you should see `/explain` in the command list. Then try:

```text
/explain prompt caching
```

You should get a 3–5 sentence answer with one analogy and zero jargon. If you get something longer or more technical, the command file didn't load — check `~/.claude/commands/explain.md` exists.

---

## Uninstall

**Plugin install:**
```text
/plugin uninstall claude-code-explain
```

**Standalone install:**
```bash
./setup.sh --uninstall
# or just:
rm ~/.claude/commands/explain.md
```

---

## How it works (the rules the command follows)

The command file is a prompt with hard constraints. Every answer must:

- Be 3–5 sentences. Never more.
- Use zero jargon (or define unavoidable terms inline in ≤5 words).
- Include exactly **one** analogy *or* one concrete scenario — not both, not zero.
- Skip code dumps and meta-commentary ("this code does X", "in summary").
- Target a smart non-engineer reader (PM, designer, exec).

The value is the constraint. Loosen it and you get the same verbose explanations Claude gives by default.

---

## Contributing

PRs welcome. The command lives in [`commands/explain.md`](commands/explain.md) — tweak the rules, add example pairs, or refine the output format. If you change behavior, update the example in this README so users see the new shape.

---

## License

MIT — see [LICENSE](LICENSE).
