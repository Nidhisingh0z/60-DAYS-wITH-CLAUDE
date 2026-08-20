# TaskSpark — SETUP.md

Installation and local setup guide. Follow this to get TaskSpark running on a fresh machine.

---

## Prerequisites

| Tool | Purpose | Verify with |
|---|---|---|
| Node.js (v18+) | JavaScript runtime; required to run the serverless function locally and use npm | `node -v` |
| npm | Package manager, bundled with Node.js | `npm -v` |
| Git | Version control | `git -v` |
| Vercel CLI | Simulates the serverless hosting environment locally (`vercel dev`), and deploys to production | `vercel -v` |
| A Google AI Studio account | Provides the Gemini API key that powers task extraction | N/A |
| A Vercel account | Hosting for the deployed app | N/A |
| A GitHub account | Source control + triggers Vercel deployments | N/A |

---

## 1. Clone the Repository

```
git clone https://github.com/Nidhisingh0z/taskspark.git
cd taskspark
```

## 2. Install Dependencies

```
npm install
```
This reads `package.json` and installs:
- `@google/genai` — Google's official SDK for calling the Gemini API
- `dotenv` — loads the API key from `.env.local` into the app at runtime

## 3. Configure Environment Variables

Create a file named `.env.local` in the project root (see `ENVIRONMENT.md` for full details):
```
GEMINI_API_KEY=your_real_key_here
```
This file is already excluded from Git via `.gitignore` — it will never be committed.

## 4. Install the Vercel CLI (if not already installed)

```
npm install -g vercel
```
Verify with:
```
vercel -v
```

## 5. Run Locally

```
vercel dev
```
On first run, Vercel CLI will prompt you to log in and link the project — accept the defaults (see project's internal setup notes / Day 3 log for the exact prompts encountered).

Once running, open:
```
http://localhost:3000
```

## 6. Verify It Works

- You should see the TaskSpark page load
- Type any text into the textarea and click the action button
- You should receive a real response back within a few seconds (proves the full pipeline: browser → serverless function → Gemini API)

---

## Common Setup Issues

| Symptom | Cause | Fix |
|---|---|---|
| `'vercel' is not recognized` | Vercel CLI not installed, or terminal not restarted after install | Run `npm install -g vercel`; if it still fails, close and reopen the terminal |
| `type nul > file` doesn't create a file, or errors out | You're in PowerShell, not Command Prompt — `type nul >` is a cmd.exe-only trick | Use `New-Item -ItemType File -Name filename` in PowerShell instead |
| Files end up in the wrong folder (e.g., inside `api/` instead of the root) | Terminal's current directory wasn't where you expected | Always confirm your current path first with `pwd` (PowerShell) and run `Get-ChildItem -Name` to check what's actually there before creating more files |
| `404 ... model ... no longer available` from the Gemini API | Google deprecated the model version in use | Check the current model name in Google's docs and update it in `api/extract.js` (see `ENVIRONMENT.md` for the current locked model name) |
| API key errors (`API key not valid`) | Typo in `.env.local`, or key not saved | Re-check `.env.local` has no quotes/extra spaces around the key, and that the file is saved |

---

## Project Repository

- **GitHub:** `https://github.com/Nidhisingh0z/taskspark`
- **Local path (builder's machine):** `D:\claude\taskspark`
