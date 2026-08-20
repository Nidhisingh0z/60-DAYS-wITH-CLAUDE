# TaskSpark — Day 3 Addendum to Implementation Blueprint

**Read alongside the Day 1 Implementation Blueprint and the Day 2 addendum.**

---

## What Changed Today

1. **AI provider changed: Anthropic Claude → Google Gemini.** This is the most significant change to date. Every future day's instructions that reference "Claude" or "Anthropic" should be read as "Gemini" / "Google" instead:
   - SDK: `@google/genai` (not `@anthropic-ai/sdk`)
   - Env var: `GEMINI_API_KEY` (not `ANTHROPIC_API_KEY`)
   - Model: `gemini-3.5-flash-lite` (not `claude-haiku-4-5-20251001`)
   - Call shape: `ai.models.generateContent({ model, contents })` → `response.text`

2. **Environment and foundation work (originally Day 2 in the blueprint) completed today:** Node/npm/Git confirmed, Vercel CLI installed, dependencies installed, `.env.local` configured, connectivity proven, minimal end-to-end "Hello World" pipeline built and tested locally via `vercel dev`.

3. **A file-creation issue from Day 2 was discovered and fixed** — `index.html`, `style.css`, `script.js`, and `api/` didn't actually exist on disk despite appearing to be created, due to a PowerShell/cmd command mismatch. Resolved; verified clean.

**No change to product scope, UI design, or API contract** — those remain exactly as specified in the Day 2 documents (`UI-WIREFRAMES.md`, `API.md`, `SCHEMA.md`), just now implemented against Gemini instead of Claude.

---

## Day 4 Readiness Check

✅ **Environment ready:** Node, npm, Git, Vercel CLI all confirmed working.
✅ **Dependencies installed:** `@google/genai`, `dotenv`.
✅ **Pipeline proven:** browser → serverless function → Gemini → browser, confirmed working locally.
✅ **Folder structure confirmed correct** via `Get-ChildItem -Name` (twice, after fixing the Day 2 issue).
✅ **No scope creep:** only change was the AI provider swap, which was necessary (not optional) given the builder's decision.

**Day 4 (Core UI Build) can begin immediately** using:
- `docs/UI-WIREFRAMES.md` (Day 2) as the exact visual spec
- The original Day 3 section of the Day 1 blueprint (renumbered to Day 4) as the step-by-step plan — content unchanged, just build real markup/CSS on top of today's minimal "Hello World" files instead of from scratch

---

## Reminder for Day 4's Fresh AI Conversation

When starting Day 4 in a new chat, provide:
1. The "Project Snapshot" section from the Day 1 blueprint
2. `docs/UI-WIREFRAMES.md`
3. This addendum (for the Gemini-vs-Claude context)
4. Confirmation that `index.html`, `style.css`, `script.js`, and `api/extract.js` already exist with minimal working content — Day 4 builds the real UI on top of them, not from an empty file.
