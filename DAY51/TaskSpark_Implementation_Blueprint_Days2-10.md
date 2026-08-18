# TaskSpark — Implementation Blueprint (Days 2–10)

**AB Talks 60-Day Claude AI Challenge — 10-Day Capstone**
**Single source of truth for the remainder of the build.** Each day below is self-contained: paste that day's section into a fresh AI conversation and it has everything needed to continue building without re-planning or re-deciding architecture.

---

## 0. Project Snapshot (read this first, every day)

**Product:** TaskSpark — paste messy text (notes, emails, chat) → Claude API extracts a clean list of tasks with detected due dates. One page, no accounts, no database, no saved history. Every extraction is a fresh, stateless result.

**Builder profile:** Intermediate coder, ~1 hour/day available, already has a GitHub account, deployment experience, and an Anthropic API key. Primary goal: an impressive, fully working, polished v1.0 live by Day 10 for a portfolio/judge demo.

**Locked v1.0 scope — do not expand:**
- ✅ Plain text input only (no files, no images, no OCR)
- ✅ AI task extraction + due date detection
- ✅ Clean results display
- ✅ Responsive, polished single-page UI
- ✅ Live deployment
- ❌ No accounts/login, no database, no saved history, no task editing/checkoff, no priority/category tagging, no integrations, no native app

If a new feature idea comes up on any day, check it against this list first. If it's not already planned, it goes on a "Future Scope" note, not into the build.

**Locked technical stack (decided now so no day has to re-decide it):**

| Layer | Choice | Why |
|---|---|---|
| Frontend | Plain HTML + CSS + vanilla JavaScript, single page (`index.html`) | Fastest to build and style well in short daily sessions; no build tooling to fight with; renders instantly anywhere |
| Backend | One serverless function (`/api/extract`) written in Node.js | Keeps the Anthropic API key off the client; free-tier friendly; no server to manage |
| AI | Anthropic Claude API, called only from the serverless function | Already have API access; structured-output prompting handles extraction + date detection |
| Hosting | Vercel (free tier), deployed from GitHub | Zero-config support for a static page + a serverless function in the same repo; builder already knows GitHub + deployment |
| Data storage | None | Stateless by design — no database needed for v1.0 |

**Repo name (suggested):** `taskspark`
**Final folder structure (target state by Day 9):**
```
taskspark/
├── index.html
├── style.css
├── script.js
├── api/
│   └── extract.js
├── .env.local              (local only — holds ANTHROPIC_API_KEY, never committed)
├── .gitignore
├── vercel.json              (only if needed — see Day 9)
├── package.json
└── README.md
```

**The "wow moment" to always protect:** a judge pastes messy text, clicks one button, and within a few seconds sees a clean, dated task list appear. Every day's work should either build toward that moment or polish it — never distract from it.

---

## DAY 2 — Project Setup & Claude API Connectivity

### 🎯 Objective
Get the project skeleton created, pushed to GitHub, and prove the Claude API can be called successfully from a Node script — before any UI work begins.

### 📖 What I'll learn
- How to structure a small full-stack (static + serverless) project
- How to securely store and use an API key with environment variables
- Basics of calling the Anthropic Messages API from Node.js

### 🛠 Features to build
- Repo scaffold (folders/files listed above, empty placeholders)
- A standalone test script that calls the Claude API and prints a response
- `.gitignore` configured so the API key is never committed

### 📝 Step-by-step implementation plan
1. Create a new local folder `taskspark` and run `git init`.
2. Create a new empty GitHub repository named `taskspark` (no README/template) and connect it as the remote.
3. Create the folder structure above with empty placeholder files (`index.html`, `style.css`, `script.js`, `api/extract.js`, `README.md`).
4. Run `npm init -y` to create `package.json`.
5. Install the Anthropic SDK: `npm install @anthropic-ai/sdk`.
6. Create `.env.local` with one line: `ANTHROPIC_API_KEY=your_key_here`.
7. Create `.gitignore` and add: `node_modules/`, `.env.local`.
8. Write a throwaway test script `test-api.js` at the repo root that:
   - Loads the API key from `.env.local` (use the `dotenv` package: `npm install dotenv`)
   - Sends a single hardcoded test message to Claude (e.g., "Say hello in 5 words") using the Anthropic SDK
   - Logs the response text to the console
9. Run `node test-api.js` and confirm you get a real response back.
10. Commit and push: `git add .`, `git commit -m "Day 2: project setup + Claude API connectivity test"`, `git push`.
11. Delete or leave `test-api.js` — it's not part of the final app, just a connectivity check (safe to delete once confirmed working).

### 📂 Files and folders to create or modify
`taskspark/` (new repo), `index.html`, `style.css`, `script.js`, `api/extract.js` (empty for now), `package.json`, `.env.local`, `.gitignore`, `test-api.js` (temporary), `README.md` (placeholder title only)

### 🔗 APIs, libraries, services, tools to integrate
- `@anthropic-ai/sdk` (npm)
- `dotenv` (npm)
- Anthropic Claude API (model: use the current recommended default text model available to your API key — check your Anthropic Console if unsure)

### 🧪 Testing tasks
- Confirm `node test-api.js` returns real text from Claude (not an error).
- Confirm `.env.local` does NOT show up in `git status` after committing (proves `.gitignore` is working).
- Confirm the GitHub repo shows your pushed commit online.

### 🐞 Common issues and debugging tips
- **"Invalid API key" error** → double-check `.env.local` has no extra quotes/spaces around the key, and that `dotenv` is loaded (`require('dotenv').config()`) at the very top of the script.
- **Module not found** → confirm you ran `npm install` inside the `taskspark` folder, not a parent folder.
- **API key accidentally committed** → if this happens, regenerate the key in the Anthropic Console immediately and re-add it locally; do not just delete it from a future commit (git history still has it).

### ✅ End-of-day checklist
- [ ] GitHub repo created and pushed
- [ ] Folder structure matches target state
- [ ] `node test-api.js` prints a real Claude response
- [ ] `.env.local` is git-ignored (confirmed via `git status`)

### 📸 Expected project state and screenshots to capture
- Terminal screenshot showing a successful Claude API response
- GitHub repo page showing the initial commit

### ➡️ Handoff notes for Day 3
Project scaffold exists, is on GitHub, and Claude API connectivity is proven from a Node script. Day 3 builds the actual UI in `index.html`/`style.css` — no API calls yet, just the interface and static layout.

---

## DAY 3 — Core UI Build

### 🎯 Objective
Build the complete visual interface — input area, action button, and results area — fully styled and responsive, using static placeholder data (no live AI calls yet).

### 📖 What I'll learn
- Structuring a clean single-page layout with semantic HTML
- Writing focused, modern CSS (flexbox/grid) for a polished look
- Designing UI states (empty, loading, results) before wiring up logic

### 🛠 Features to build
- Header/branding area (app name "TaskSpark" + one-line tagline)
- Large text input (`<textarea>`) for pasting messy text
- "Extract Tasks" button
- Results area that displays a static example list of tasks with dates (hardcoded for now, to design the look)
- Responsive layout for mobile and desktop

### 📝 Step-by-step implementation plan
1. In `index.html`, build the page structure: header, input section, results section, footer (optional small credit line).
2. Add a `<textarea>` with a placeholder like: *"Paste your messy notes, email, or chat here..."*
3. Add an `<button id="extractBtn">Extract Tasks</button>`.
4. Add a results container `<div id="results"></div>` — leave it empty in HTML; you'll temporarily inject 2–3 hardcoded example task rows via `script.js` just to design against real-looking content.
5. In `style.css`: choose a simple, confident color palette (e.g., one dark accent color + white/light background — avoid generic default blue). Style the header, textarea (rounded corners, clear focus state), button (clear hover/active state), and result cards (task text + a small date pill/badge).
6. Add responsive rules (`@media (max-width: 600px)`) so the layout stacks cleanly on mobile — textarea full width, comfortable touch-sized button.
7. Add a simple empty-state message shown when there are no results yet ("Paste some text above and click Extract Tasks to get started").
8. Temporarily render 2–3 fake example tasks (with fake dates) in `script.js` on page load, purely to check how real results will look. Remove this fake-data block on Day 5 once live data is wired in.

### 📂 Files and folders to create or modify
`index.html`, `style.css`, `script.js` (temporary fake-render logic only)

### 🔗 APIs, libraries, services, tools to integrate
None yet — pure frontend, no API calls today.

### 🧪 Testing tasks
- Resize the browser window (or use dev tools device toolbar) to confirm the layout holds up on mobile widths.
- Confirm textarea, button, and results area all look intentional and polished with the fake example data.
- Check color contrast is readable (dark text on light background or vice versa, no low-contrast combos).

### 🐞 Common issues and debugging tips
- **Textarea doesn't resize nicely** → set `resize: vertical` and a sensible `min-height` in CSS.
- **Layout breaks on mobile** → check for fixed pixel widths instead of `%`/`max-width`; prefer flexible units.
- **Button doesn't look clickable** → add a visible hover/cursor state (`cursor: pointer`, background color shift).

### ✅ End-of-day checklist
- [ ] Full page layout built and styled (header, input, button, results, empty state)
- [ ] Looks polished with fake example data
- [ ] Confirmed responsive on mobile width
- [ ] Pushed to GitHub with commit message "Day 3: core UI build"

### 📸 Expected project state and screenshots to capture
- Desktop screenshot of the full page with fake example results showing
- Mobile-width screenshot of the same page

### ➡️ Handoff notes for Day 4
UI is fully built and styled with placeholder/fake data — this is the visual target to preserve. Day 4 does NOT touch the frontend; it builds the backend serverless function and the AI prompt that will eventually replace the fake data.

---

## DAY 4 — Backend Function & Extraction Prompt Engineering

### 🎯 Objective
Build the `/api/extract` serverless function that takes raw text and returns a clean, structured JSON list of tasks with due dates — tested directly (not yet connected to the UI).

### 📖 What I'll learn
- Writing a serverless function compatible with Vercel
- Prompt engineering for reliable, structured (JSON) AI output
- Defensive parsing of AI responses

### 🛠 Features to build
- `api/extract.js` serverless function
- A carefully engineered prompt that instructs Claude to return strict JSON: a list of `{ task, dueDate }` objects
- Basic input validation (reject empty text)

### 📝 Step-by-step implementation plan
1. In `api/extract.js`, write a Vercel-style serverless function: `export default async function handler(req, res) { ... }`.
2. Validate the request: only accept `POST`, read `req.body.text`; if missing/empty, return a 400 with a clear error JSON.
3. Build the Claude API request using `@anthropic-ai/sdk`, loading the API key from `process.env.ANTHROPIC_API_KEY` (Vercel injects env vars automatically in serverless functions — no `dotenv` needed here, but keep `.env.local` for local testing via `vercel dev` later).
4. Write the extraction prompt. Key instructions to include:
   - "Extract every actionable task or to-do item from the following text."
   - "For each task, detect a due date or deadline if one is mentioned (relative dates like 'tomorrow', 'next Friday', 'asap' are valid) — otherwise use null."
   - "Respond with ONLY valid JSON, no explanation, in this exact shape: `{ \"tasks\": [ { \"task\": \"...\", \"dueDate\": \"...\" or null } ] }`"
   - "If there are no actionable tasks in the text, respond with `{ \"tasks\": [] }`."
   - Include 2–3 short examples inline in the prompt (few-shot) using the sample inputs from the PRD Section 9 — this significantly improves reliability.
5. Send the user's text as part of the prompt, call the API, and get the raw text response.
6. Defensively parse the response: `JSON.parse()` inside a `try/catch`; if parsing fails, return a 502 error with a friendly message ("AI response could not be understood, please try again") rather than crashing.
7. Return the parsed `{ tasks: [...] }` JSON to the caller with a 200 status.
8. Test locally using `vercel dev` (or a simple local Express wrapper if you prefer) and a tool like `curl` or Postman-style requests, sending the 3 PRD sample inputs and checking the output matches expectations.

### 📂 Files and folders to create or modify
`api/extract.js`, `package.json` (add `@anthropic-ai/sdk` if not already present)

### 🔗 APIs, libraries, services, tools to integrate
- `@anthropic-ai/sdk`
- Vercel CLI (`npm install -g vercel`) for local serverless testing via `vercel dev`

### 🧪 Testing tasks
- Test with all 3 PRD sample inputs (Section 9) — confirm tasks and dates extracted match expectations.
- Test with empty text — confirm a clean 400 error, not a crash.
- Test with text that has no tasks at all — confirm `{ "tasks": [] }` is returned cleanly.
- Test with a long, messy paragraph — confirm the function doesn't time out or return malformed JSON.

### 🐞 Common issues and debugging tips
- **AI adds explanation text before/after the JSON** → strengthen the prompt ("Respond with ONLY the JSON object, nothing else") and add a fallback that extracts the first `{...}` block via regex before parsing if needed.
- **Function works locally but you're unsure about Vercel env vars** → this gets fully verified on Day 9 (Deployment); for now just confirm the logic works with `vercel dev` or a local `.env.local`.
- **Date detection is inconsistent** → this is expected today; Day 6 is dedicated to refining exactly this. Don't over-tune the prompt yet — get it "good enough" and move on.

### ✅ End-of-day checklist
- [ ] `/api/extract` returns valid structured JSON for all 3 sample inputs
- [ ] Empty input handled gracefully
- [ ] "No tasks found" case returns `{ tasks: [] }` cleanly
- [ ] Pushed to GitHub with commit message "Day 4: backend extraction function + prompt"

### 📸 Expected project state and screenshots to capture
- Terminal/Postman screenshot showing a successful JSON response for a sample input

### ➡️ Handoff notes for Day 5
The backend function works and returns reliable structured JSON when tested directly. The frontend (Day 3) still shows fake hardcoded data. Day 5's only job is wiring the two together — no new features, just integration.

---

## DAY 5 — Frontend–Backend Integration (End-to-End Flow)

### 🎯 Objective
Connect the UI to the real `/api/extract` function so the full flow works end-to-end: paste text → click button → see real AI-extracted tasks.

### 📖 What I'll learn
- Making `fetch()` calls from the browser to a serverless function
- Rendering dynamic data into the DOM
- Basic async/await error handling in the browser

### 🛠 Features to build
- Real `fetch()` call from `script.js` to `/api/extract` on button click
- Dynamic rendering of the returned tasks into the results area (replacing the Day 3 fake data)
- Loading state while waiting for the response
- Basic error message rendering if the fetch fails

### 📝 Step-by-step implementation plan
1. Remove the Day 3 fake-data rendering block from `script.js`.
2. Add a click event listener on `#extractBtn`.
3. On click: read the textarea value; if empty, show a small inline message ("Please paste some text first") and stop.
4. Show a loading state (e.g., swap button text to "Extracting..." and disable it, or show a small spinner in the results area).
5. Call `fetch('/api/extract', { method: 'POST', headers: {'Content-Type':'application/json'}, body: JSON.stringify({ text }) })`.
6. On success: parse the JSON response, clear the results area, and render each task as a card (task text + date badge, or "No date" if `dueDate` is null).
7. If `tasks` is an empty array, show the friendly "No actionable tasks found" message (build this UI state now if not already done Day 3).
8. On fetch failure or non-200 response: show a friendly error message in the results area (e.g., "Something went wrong — please try again").
9. Reset the loading state (re-enable button, restore text) in both success and error cases.
10. Test the full flow manually in the browser using `vercel dev` locally.

### 📂 Files and folders to create or modify
`script.js` (main changes), `index.html`/`style.css` (only minor tweaks if a loading/error element needs adding)

### 🔗 APIs, libraries, services, tools to integrate
None new — this is pure integration of Day 3 UI + Day 4 backend.

### 🧪 Testing tasks
- Full manual test: paste each of the 3 PRD sample inputs into the real UI and confirm correct results render.
- Test empty submission — confirm the inline warning shows and no API call is made.
- Test the loading state is visible (even briefly) during a real call.
- Test what happens if you temporarily break the API URL (typo) — confirm the error state displays instead of a blank page/console-only error.

### 🐞 Common issues and debugging tips
- **CORS or 404 on fetch** → when using `vercel dev`, confirm the function path matches exactly (`/api/extract`) and the dev server is serving both static files and the function together.
- **Results don't update on second extraction** → make sure you're clearing the previous results (`innerHTML = ''` or equivalent) before rendering new ones.
- **Loading state gets "stuck"** → make sure the reset logic runs in a `finally` block (or both success and catch paths), not just on success.

### ✅ End-of-day checklist
- [ ] Real end-to-end flow works: paste → click → real AI results appear
- [ ] Loading state visible during the call
- [ ] Empty-input and error states both work
- [ ] Pushed to GitHub with commit message "Day 5: frontend-backend integration"

### 📸 Expected project state and screenshots to capture
- Screenshot of the app showing a real extracted task list from a real pasted input (this is your first true "working product" screenshot)

### ➡️ Handoff notes for Day 6
The app fully works end-to-end with real AI extraction. Task detection is functional but not yet refined — Day 6 focuses specifically on improving due-date detection accuracy and hardening the JSON output against edge cases, using the prompt built on Day 4 as the starting point.

---

## DAY 6 — Due Date Detection Refinement & Output Hardening

### 🎯 Objective
Improve the accuracy and consistency of due-date detection, and make the extraction pipeline resilient to messy or unusual input.

### 📖 What I'll learn
- Iterative prompt refinement based on real test cases
- Handling ambiguous natural-language dates
- Building a wider self-authored test set to catch regressions

### 🛠 Features to build
- Refined extraction prompt with better date-handling instructions and more few-shot examples
- A small personal test set of 8–10 varied text samples (beyond the 3 in the PRD) to validate against
- Minor backend hardening (timeout handling, clearer error messages)

### 📝 Step-by-step implementation plan
1. Write 8–10 new test inputs yourself, covering: relative dates ("in 2 days," "next Tuesday"), vague urgency ("asap," "urgent," "whenever you get a chance"), multiple tasks with different dates in one block of text, tasks with no date at all, and a non-task message (should return empty).
2. Run each through the current pipeline (locally via `vercel dev`) and record what's wrong (missed dates, wrong dates, tasks not detected, tasks invented that weren't really there).
3. Update the prompt in `api/extract.js` based on the failure patterns you see — e.g., add explicit instructions like "Interpret relative dates like 'tomorrow' or 'next Friday' as due dates. If urgency is implied but no specific date is given (e.g., 'asap'), set dueDate to 'ASAP' instead of null." Add 1–2 more few-shot examples covering your worst failure cases.
4. Re-run your full test set after each prompt change and confirm improvement (don't change more than one thing at a time — you won't know what fixed it otherwise).
5. Add a request timeout safeguard (e.g., abort/reject if the API call takes longer than ~15 seconds) so the UI never hangs indefinitely — return a friendly timeout error instead.
6. Double-check the "invented tasks" failure mode specifically: make sure the prompt explicitly says not to invent tasks that aren't implied by the text, and not to treat greetings/small talk as tasks.

### 📂 Files and folders to create or modify
`api/extract.js` (prompt + timeout logic), optionally a new `test-cases.md` or `test-cases.js` file documenting your test set for reuse on Day 8

### 🔗 APIs, libraries, services, tools to integrate
None new — refinement of existing Day 4 backend.

### 🧪 Testing tasks
- Run all 8–10 new test cases and confirm acceptable accuracy (dates correctly interpreted, no invented tasks, non-task text returns empty).
- Confirm the app doesn't hang indefinitely on a slow/failed request (timeout works).
- Re-run the original 3 PRD sample inputs to confirm no regressions.

### 🐞 Common issues and debugging tips
- **Over-correcting the prompt breaks previously-working cases** → change one instruction at a time and re-test the full set each time, not just the case you're fixing.
- **AI treats every sentence as a task** → explicitly instruct it to only extract clear action items, and give a negative example ("Just checking in, hope you're well" → no tasks).
- **Dates come back in inconsistent formats** (e.g., "Friday" vs "this Friday" vs "08/21") → decide on one consistent output style in the prompt (e.g., "return dates as they're naturally phrased in the text, don't reformat them") and stick with it — perfect calendar-date math isn't required for v1.0.

### ✅ End-of-day checklist
- [ ] 8–10 personal test cases created and documented
- [ ] Prompt refined and re-tested against all cases with clear improvement
- [ ] Timeout handling added
- [ ] Pushed to GitHub with commit message "Day 6: date detection refinement + hardening"

### 📸 Expected project state and screenshots to capture
- Screenshot of 2–3 of the trickier test cases (e.g., "asap," multiple dates) working correctly in the live app

### ➡️ Handoff notes for Day 7
Extraction accuracy is now solid and tested against a real personal test set. The app works correctly but may still feel rough visually in edge-case states (loading, empty, error). Day 7 is dedicated purely to UX polish — no further prompt/logic changes unless something is clearly broken.

---

## DAY 7 — UX Polish (Loading, Empty, and Error States)

### 🎯 Objective
Make every state of the app — not just the "happy path" — feel intentional, smooth, and professional. This is what separates a working demo from an impressive one.

### 📖 What I'll learn
- Designing for all UI states, not just the success case
- Small UX details (transitions, micro-copy) that significantly raise perceived quality
- Writing clear, human error/empty-state messaging

### 🛠 Features to build
- Polished loading indicator (spinner or animated dots, not just disabled button text)
- Polished empty state (before first use) with friendly guidance copy
- Polished "no tasks found" state with helpful copy (not just a blank message)
- Polished error state with a retry-friendly message
- Subtle transition/animation when results appear (fade-in or slide-in)
- Final visual pass: spacing, alignment, consistent styling across all states

### 📝 Step-by-step implementation plan
1. Review all 4 states in the browser: initial/empty, loading, results, no-tasks-found, and error — list anything that looks unfinished or abrupt.
2. Replace the loading indicator with something more polished — e.g., a small animated CSS spinner next to "Analyzing your text..." instead of static "Extracting..." text.
3. Improve empty-state copy so it briefly explains the product ("Paste a messy note, email, or chat below — TaskSpark will pull out the tasks and deadlines for you.").
4. Improve "no tasks found" copy so it's reassuring, not confusing ("No action items found in this text — try pasting something with a task or deadline in it.").
5. Improve error-state copy so it's calm and actionable ("Something went wrong extracting your tasks. Please try again.") with a way to retry (the button should already be re-enabled from Day 5's reset logic).
6. Add a simple CSS fade-in/slide-in transition when task cards render, so results don't just "pop" in instantly.
7. Do a full visual pass: consistent spacing between elements, consistent font sizes/weights, consistent corner radius/shadows across cards and buttons, and confirm the color palette feels intentional (not default browser styling anywhere).
8. Test the whole flow once more end-to-end, paying attention only to *feel*, not just correctness.

### 📂 Files and folders to create or modify
`style.css` (main focus), `script.js` (copy text updates, minor class-toggling for transitions), `index.html` (minor markup for spinner/empty-state elements if needed)

### 🔗 APIs, libraries, services, tools to integrate
None — pure frontend polish, no new libraries needed (plain CSS animations are enough).

### 🧪 Testing tasks
- Manually trigger and review all 4+ states (empty, loading, success, no-tasks, error) and confirm each looks finished.
- Test on both desktop and mobile widths again after polish changes.
- Ask (if possible) one other person to try it with zero explanation and watch where they hesitate or look confused.

### 🐞 Common issues and debugging tips
- **Spinner doesn't animate** → confirm the CSS `@keyframes` rule is defined and applied, and that the element isn't `display: none` while animating (use `visibility` or conditional rendering instead if needed).
- **Transition looks janky** → keep it simple (opacity + small transform), avoid combining too many animated properties at once.
- **Polish changes accidentally break mobile layout** → re-check the mobile view after every CSS change today, not just at the end.

### ✅ End-of-day checklist
- [ ] All UI states (empty, loading, success, no-tasks, error) reviewed and polished
- [ ] Copy for each state is clear and human
- [ ] Subtle animation on results appearing
- [ ] Re-confirmed mobile responsiveness after polish
- [ ] Pushed to GitHub with commit message "Day 7: UX polish across all states"

### 📸 Expected project state and screenshots to capture
- Screenshot of the polished empty state
- Screenshot of the polished loading state
- Screenshot of the polished results state

### ➡️ Handoff notes for Day 8
The app is functionally complete and visually polished across all states, running correctly in local development. Day 8 is dedicated entirely to structured testing (not new features) — systematically working through the test set and cross-browser/device checks to catch anything before deployment.

---

## DAY 8 — Testing

### 🎯 Objective
Systematically test the complete app — functionality, accuracy, and cross-device behavior — and fix anything broken before deployment.

### 📖 What I'll learn
- Structured manual QA practices for a small web app
- Cross-browser/device testing basics
- Prioritizing and triaging bugs with limited time

### 🛠 Features to build
No new features today — this day is entirely testing and bug-fixing.

### 📝 Step-by-step implementation plan
1. Re-run the full test set from Day 6 (8–10 cases) plus the 3 PRD samples — log pass/fail for each in a simple checklist.
2. Functional edge-case pass: extremely short input (one word), extremely long input (a few paragraphs), input with special characters/emojis, input in ALL CAPS, input that's just a URL or random text.
3. Cross-browser check: open the app in at least two different browsers you have available (e.g., Chrome and Firefox, or Chrome and Safari) and confirm it looks and works the same.
4. Cross-device check: test on an actual phone browser if possible (not just dev-tools resize) — check touch interactions (tapping the button, scrolling, textarea focus/keyboard behavior).
5. Network/error resilience check: temporarily simulate a slow connection (browser dev tools throttling) and confirm the loading state still behaves correctly and doesn't break.
6. Triage any bugs found: fix anything that breaks core functionality or looks clearly broken today; note (don't fix) anything cosmetic/minor that's genuinely low-risk, to protect your remaining time for deployment.
7. Final code cleanup pass: remove any leftover `console.log()` debug statements, commented-out dead code, and the temporary `test-api.js` file from Day 2 if still present.

### 📂 Files and folders to create or modify
Any file with a bug fix; likely light touches across `script.js`, `api/extract.js`, `style.css`

### 🔗 APIs, libraries, services, tools to integrate
None new — browser dev tools (network throttling, device toolbar) are the only "tools" used today.

### 🧪 Testing tasks
- Full regression pass on all test cases (Day 6 set + PRD samples) — target: all pass or have a known, accepted limitation.
- Cross-browser check complete on 2+ browsers.
- Real mobile device check complete (or thorough dev-tools emulation if a real device isn't available).
- Throttled-network check complete — loading state holds up.

### 🐞 Common issues and debugging tips
- **Works in Chrome, breaks in Safari/Firefox** → check for any CSS/JS features that aren't broadly supported (rare with this simple a stack, but worth a quick check); stick to well-supported basics.
- **Mobile keyboard covers the button** → make sure the page can scroll normally when the textarea is focused; avoid fixed-position elements that trap the button off-screen.
- **A previously-passing test case now fails** → this means a Day 7 polish change had a side effect; check recent CSS/JS diffs first before touching the prompt again.

### ✅ End-of-day checklist
- [ ] Full test set re-run and passing (or limitations knowingly accepted)
- [ ] Cross-browser check done
- [ ] Mobile check done
- [ ] Debug code/leftover files cleaned up
- [ ] Pushed to GitHub with commit message "Day 8: testing pass + cleanup"

### 📸 Expected project state and screenshots to capture
- Screenshot or note of your test checklist with pass/fail results

### ➡️ Handoff notes for Day 9
The app is fully tested locally and considered stable. Nothing about functionality or UI should need to change during deployment — Day 9 is purely about getting this exact, tested version live on the internet.

---

## DAY 9 — Deployment

### 🎯 Objective
Deploy TaskSpark to a live, public URL on Vercel, with the API key securely configured, and verify it works in production exactly as it did locally.

### 📖 What I'll learn
- Deploying a static + serverless project to Vercel
- Managing environment variables/secrets in a hosting platform
- Production smoke-testing

### 🛠 Features to build
No new features — deployment and production configuration only.

### 📝 Step-by-step implementation plan
1. Ensure all Day 8 changes are committed and pushed to GitHub (`git status` should be clean).
2. Log into Vercel (or create a free account if not already set up) and connect your GitHub account.
3. Import the `taskspark` repository as a new Vercel project.
4. In the Vercel project's Environment Variables settings, add `ANTHROPIC_API_KEY` with your real key value (this keeps it out of the codebase entirely — it's injected at runtime).
5. Deploy (Vercel will auto-detect the static files + the `api/` folder as a serverless function — no custom `vercel.json` should be needed for this simple structure, but add one only if the default deploy doesn't correctly route `/api/extract`).
6. Once deployed, open the live production URL and re-run the full Day 6 test set plus the 3 PRD samples directly against production (not local) to confirm identical behavior.
7. Test the live URL on your phone's actual mobile browser (not just emulation) if possible.
8. Confirm no console errors appear in production and that the API key is not visible anywhere in browser dev tools (Network tab should only show your own `/api/extract` calls, never a direct call to Anthropic's API from the browser).
9. Note the final live URL somewhere safe — this is what you'll share for the demo/submission.

### 📂 Files and folders to create or modify
Possibly `vercel.json` (only if routing needs adjustment), otherwise no code changes — configuration only, done in the Vercel dashboard

### 🔗 APIs, libraries, services, tools to integrate
- Vercel (hosting, free tier)
- Vercel Environment Variables (for `ANTHROPIC_API_KEY`)

### 🧪 Testing tasks
- Full regression test suite re-run against the live production URL.
- Confirm the API key is never exposed client-side (check Network tab in browser dev tools).
- Confirm the live URL loads correctly on both desktop and mobile.

### 🐞 Common issues and debugging tips
- **API calls fail in production but worked locally** → almost always a missing/mistyped environment variable name in Vercel — confirm it's exactly `ANTHROPIC_API_KEY` and redeploy after adding it (env var changes require a new deployment to take effect).
- **404 on `/api/extract` in production** → confirm the file is at `api/extract.js` at the repo root (not nested inside another folder) — Vercel auto-routes based on this exact structure.
- **Works but is slow on first request** → this is normal "cold start" behavior for serverless functions on the free tier; subsequent requests will be faster. Worth knowing for your live demo — consider doing one "warm-up" extraction before presenting to judges.

### ✅ End-of-day checklist
- [ ] App successfully deployed to a public Vercel URL
- [ ] `ANTHROPIC_API_KEY` configured securely in Vercel, not in code
- [ ] Full test set passes in production
- [ ] Confirmed working on a real mobile browser
- [ ] Live URL saved/noted for demo use

### 📸 Expected project state and screenshots to capture
- Screenshot of the live production URL in the browser address bar with a successful extraction shown
- Screenshot of the Vercel dashboard showing the successful deployment

### ➡️ Handoff notes for Day 10
The app is live, fully tested in production, and functionally complete. Day 10 is final polish, documentation, and demo preparation only — no functional changes unless something is actively broken.

---

## DAY 10 — Final Polish, Documentation & Demo Readiness

### 🎯 Objective
Wrap the project with a professional README, a final visual/UX check, and a rehearsed demo — ready to confidently present as a finished v1.0.

### 📖 What I'll learn
- Writing a clear, professional project README
- Preparing and rehearsing a short live product demo
- Doing a final "judge's-eye view" pass on a finished product

### 🛠 Features to build
No new functional features — documentation and presentation readiness only. (Only fix something here if it's a genuine, demo-breaking bug.)

### 📝 Step-by-step implementation plan
1. Write `README.md` covering: project name and one-line description, the problem it solves, key features, tech stack used, how to run it locally, and the live demo link.
2. Do one final full walkthrough of the live production app exactly as a judge would experience it — first impression, one clean successful extraction, one edge case (no tasks found) — and fix only if something looks unfinished.
3. Double-check the PRD's "In Scope" list (Section 5) against the live app — confirm every listed v1.0 feature is genuinely present and working.
4. Prepare a short demo script for yourself (60–90 seconds): what you'll say while pasting in a sample text, what you'll point out as it loads, and what you'll highlight in the result (task + date detection).
5. Rehearse the demo at least once, live, exactly as you'll present it (not just describing it) — this is where you catch a slow load, a typo in your sample text, or a UI issue you missed.
6. Do a final git commit and push of the README and any last small fixes: `git commit -m "Day 10: final polish, README, demo readiness"`.
7. Reconfirm the live URL still works one more time right before you consider the project "done."

### 📂 Files and folders to create or modify
`README.md` (main focus), minor touch-ups only elsewhere if a genuine issue is found

### 🔗 APIs, libraries, services, tools to integrate
None new.

### 🧪 Testing tasks
- Final full run-through of the live app as a first-time visitor would experience it.
- Confirm README instructions (if someone else tried to run it locally) are accurate.
- Confirm the live URL is stable and accessible from a fresh/incognito browser window (no cached-session assumptions).

### 🐞 Common issues and debugging tips
- **Tempted to add "just one more feature"** → don't. Today is about polish and presentation of the locked v1.0 scope, not new functionality — new ideas go into the README's "Future Scope" section instead, referencing PRD Section 12.
- **Demo sample text doesn't showcase the product well** → prepare and test your exact demo input in advance; don't improvise it live for the first time in front of judges.
- **Cold-start delay during live demo** → do a "warm-up" extraction a minute or two before presenting, as noted on Day 9.

### ✅ End-of-day checklist
- [ ] README written and pushed
- [ ] Full PRD "In Scope" feature list verified live
- [ ] Demo script written and rehearsed at least once
- [ ] Live URL reconfirmed working
- [ ] Project considered v1.0 complete and submission-ready

### 📸 Expected project state and screenshots to capture
- Final screenshot of the polished, live app (this can double as the pitch deck's product screenshot)
- Screenshot of the completed README on GitHub

### ➡️ Project status at end of Day 10
TaskSpark v1.0 is complete: a live, deployed, tested, and documented AI-powered task-extraction tool, built end-to-end in 10 days at roughly one hour of work per day — ready to demo and submit for the AB Talks 60-Day Claude AI Challenge.

---

## Appendix: Full PRD Sample Test Cases (for quick reference on Days 4, 6, 8)

1. *"Hey can you send the deck by Friday, and don't forget we need the budget numbers from Raj before the Monday meeting"* → 2 tasks, both with dates.
2. *"Just checking in, hope you're doing well, let's catch up soon"* → 0 tasks.
3. *"remember to call the dentist, pick up groceries tomorrow, and finish the report asap"* → 3 tasks, mixed date specificity.
