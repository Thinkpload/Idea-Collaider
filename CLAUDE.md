# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

---

## Project

**Idea Collider (Коллайдер идей)** — a skill for Claude.ai that generates ideas by *colliding* distant threads from the user's own memory/context, plus a static landing page.

**Stack:** Static HTML/CSS/JS (single-file `index.html`, vanilla canvas animation, no build step) · deployed on Vercel · the skill itself is `SKILL.md` / `idea-collider.skill`.

**Key files:**
- `index.html` — landing + live demo. Self-contained; the demo data lives in three JS arrays (`DOMAINS`, `BANK`, `INV`) near the bottom. Demo uses a **generic example profile** — never put real personal data here (public repo).
- `SKILL.md` — the method (the actual product). `idea-collider.skill` is its packaged form.
- `PLAN.md` — launch checklist + development ideas + product-backend roadmap.
- `.cursor/rules/idea-collider.mdc` — Cursor port of the method; keep it in sync with `SKILL.md` (and repack `idea-collider.skill` after any `SKILL.md` change).

**Conventions:**
- Landing copy is in Russian; keep it.
- No build tooling — edit `index.html` directly, open in a browser to verify.
- Repo is public: keep it depersonalized (no real names, portfolio, or private market details).
