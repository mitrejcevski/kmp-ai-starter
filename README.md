# KMP AI Starter: Rules + Skills

A drop-in set of AI rules and skills for Kotlin Multiplatform (and native Android/iOS) repos.
The goal: **AI that writes code your way, while you stay the engineer who understands the system.**

Works with Claude Code, Cursor, Copilot and Codex.

---

## What's inside

```
AGENTS.md                 ← The rulebook. Every AI tool reads this first.
CLAUDE.md                 ← Points Claude Code to AGENTS.md
docs/ai/ARCHITECTURE.md   ← Modules, layers, where code lives, how data flows
docs/ai/TESTING.md        ← What gets tested, how, and what "done" means
.claude/skills/
  write-spec/             ← Turn a ticket into a small, testable spec BEFORE any code
  new-feature/            ← Scaffold a feature module that follows your architecture
  unit-test/              ← Write focused tests with fakes, not mocks
  tdd/                    ← Addition to the unit testing for test-driven development
  review-diff/            ← Review AI-generated changes like a senior would
  learn-mode/             ← Build it WITH you, step by step, so you actually learn
```

## Setup (10 minutes)

1. Copy everything into the root of your repo.
2. Open `AGENTS.md`, `docs/ai/ARCHITECTURE.md` and `docs/ai/TESTING.md`. Replace every `[PLACEHOLDER]` with your real stack and conventions. **This step is what makes it work.** Generic rules give generic code.
3. Delete any rule that isn't true for your project. A rule the AI sees violated everywhere in your code is a rule it will ignore.
4. Commit it. Now your whole team shares one rulebook.

### Per tool

| Tool | What it reads |
|---|---|
| Claude Code | `CLAUDE.md` (which imports `AGENTS.md`) + skills in `.claude/skills/` |
| Codex | `AGENTS.md` |
| Cursor | `AGENTS.md` (or reference it from a project rule) |
| Copilot | `AGENTS.md`, or point `.github/copilot-instructions.md` to it |

Skills are plain markdown. If your tool doesn't load skills automatically, paste or reference the `SKILL.md` you need ("follow .claude/skills/write-spec/SKILL.md").

## The workflow these files enforce

1. **Spec first, prompt second** → `write-spec`
2. **Small batches.** One slice of behavior at a time. Big batches let the AI make decisions you never see.
3. **Failing test first, then implementation** → `unit-test`
4. **Same review bar for AI code as human code** → `review-diff`
5. **If you can't explain it, it doesn't get merged**
6. **Still write code yourself** → `learn-mode`. You can't review well what you can't write.

---

Made by Jov Mit · 16+ years in mobile · More in the AI App Developer community: skool.com/ai-flow-builder
