# TaskSpark — ENVIRONMENT.md

All environment variables, tools, and configuration values used by the project.

---

## ⚠️ Architecture Change Notice (Day 3)

The original PRD, Architecture doc, and Day 1 Implementation Blueprint specified the **Anthropic Claude API** as the AI provider. On Day 3, this was changed to the **Google Gemini API** at the builder's explicit request, after confirming Anthropic's ~$5 free trial credit was more than sufficient but choosing to proceed with an already-available Google API key instead.

**This means:** the project, as currently built, uses Google Gemini rather than Claude. Since this capstone is run under the AB Talks **Claude** AI Challenge, this is flagged here clearly for visibility — confirm eligibility with the challenge organizers before final submission. All docs from this point forward describe the actual (Gemini-based) implementation.

---

## Environment Variables

| Variable | Where it's used | Purpose | Committed to Git? |
|---|---|---|---|
| `GEMINI_API_KEY` | `api/extract.js` (local via `.env.local`; production via Vercel Environment Variables) | Authenticates requests to the Google Gemini API | **No — never.** Local copy lives only in `.env.local`, which is excluded via `.gitignore` |

### `.env.local` (local development only — not committed)
```
GEMINI_API_KEY=your_real_key_here
```

### Production (Vercel)
The same variable will be added directly in the Vercel Dashboard under Project → Settings → Environment Variables on deployment day — never stored in a file in production.

---

## AI Model Configuration

| Setting | Value | Notes |
|---|---|---|
| Provider | Google Gemini API | Changed from Anthropic Claude on Day 3 (see notice above) |
| SDK package | `@google/genai` (v2.17.1 at time of setup) | Installed via `npm install @google/genai` |
| Model | `gemini-3.5-flash-lite` | Chosen for speed and free-tier friendliness; `gemini-2.5-flash-lite` was originally tried but returned a 404 — deprecated for new users as of testing on Day 3 |
| Free tier | Yes — no credit card required, rate-limited (sufficient for capstone-scale usage) | Confirmed working via Day 3 connectivity test |

**If this model is deprecated in the future:** check Google's current models documentation and update the `model:` value in `api/extract.js` accordingly — this exact issue already occurred once during setup (see `DAY3-SUMMARY.md`).

---

## Tools & Versions (as installed on the builder's machine)

| Tool | Version confirmed | Install command |
|---|---|---|
| Node.js | v24.19.0 | (pre-installed) |
| npm | 11.17.0 | (bundled with Node.js) |
| Git | 2.53.0.windows.2 | (pre-installed) |
| Vercel CLI | 59.1.4 | `npm install -g vercel` |
| @google/genai | 2.17.1 | `npm install @google/genai` |
| dotenv | latest at install time | `npm install dotenv` |

---

## Configuration Files

| File | Purpose |
|---|---|
| `package.json` | Declares project metadata and the two runtime dependencies (`@google/genai`, `dotenv`) |
| `package-lock.json` | Locks exact installed dependency versions for reproducibility |
| `.gitignore` | Excludes `.env`, `.env.*` (covers `.env.local`), and `node_modules/` from version control — confirmed already correctly configured via the Node template used when the repo was created |
| `.env.local` | Holds the real `GEMINI_API_KEY` for local development — never committed |

---

## Security Notes

- The Gemini API key is **only ever read server-side**, inside `api/extract.js`, via `process.env.GEMINI_API_KEY`. It is never sent to or accessible from the browser.
- Confirmed via `.gitignore` inspection on Day 3 that `.env.local` is excluded from version control (matches pattern `.env.*`).
- Production key storage (Vercel Environment Variables) will be configured on deployment day — this is the equivalent server-side-only protection in the live environment.
