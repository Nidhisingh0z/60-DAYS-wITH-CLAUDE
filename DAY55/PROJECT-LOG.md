# TaskSpark — Project Log

Running log of daily progress for the AB Talks 60-Day Claude AI Challenge capstone.

---

## Day 1 — Requirements
- Discovered the project idea: an AI-powered tool that extracts tasks + due dates from messy pasted text.
- Locked v1.0 scope: plain text input only, no accounts, no database, no saved history.
- Deliverables: PRD, Implementation Blueprint (Days 2–10), Pitch Deck.
- Status: ✅ Complete.

## Day 2 — System Design
- Created GitHub repository, cloned locally, set up initial project structure.
- Designed full system architecture, data schema rationale, API contract, UI wireframes, and project structure.
- Status: ✅ Complete.

## Day 3 — Project Setup & Foundation
- Verified/configured development environment (Node, npm, Git, Vercel CLI).
- AI provider changed from Anthropic Claude to Google Gemini (builder decision).
- Fixed a Day 2 file-creation issue (PowerShell/cmd mismatch).
- Built and verified a minimal end-to-end "Hello World" pipeline.
- Status: ✅ Complete.

## Day 4 — Core Feature Implementation (Core UI Build)
- Built the complete, polished UI — all 5 states (Empty, Loading, Results, No-Tasks-Found, Error).
- Wired the button to temporary fake data to test all states before real AI integration.
- Cleaned up an accidentally committed `files.zip`; added `.gitignore` protection.
- Status: ✅ Complete.

## Day 5 — Continue Core Feature Development
- Built the real Gemini extraction prompt in `api/extract.js` — structured JSON output, task + due date detection, with input validation, timeout handling, and defensive parsing.
- Verified the real extraction logic directly (PowerShell tests) against all 3 PRD sample cases — all passed exactly as expected.
- Replaced Day 4's fake data (`simulateExtraction`) in `script.js` with a real `fetch('/api/extract', ...)` call — required no changes to UI/state logic.
- Verified the full real pipeline end-to-end through the actual UI (builder screenshots confirmed): real extraction, real "no tasks" handling, empty-input warning.
- **TaskSpark's core feature is now fully functional, locally, end-to-end.**
- Status: ✅ Complete.

## Day 6 — (Not yet started)
- Planned: Due date detection refinement & output hardening — wider test set, iterative prompt improvement.

---

*This log is updated at the end of each day and lives in the `docs/` folder.*
