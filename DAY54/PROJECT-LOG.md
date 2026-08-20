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
- **AI provider changed from Anthropic Claude to Google Gemini** (builder decision).
- Fixed a Day 2 file-creation issue (PowerShell/cmd mismatch).
- Built and verified a minimal end-to-end "Hello World" pipeline (browser → serverless function → Gemini → browser).
- Status: ✅ Complete.

## Day 4 — Core Feature Implementation (Core UI Build)
- Built the complete, polished UI across `index.html`, `style.css`, `script.js` — all 5 states (Empty, Loading, Results, No-Tasks-Found, Error) matching `UI-WIREFRAMES.md`.
- Wired the "Extract Tasks" button to temporary fake data (`simulateExtraction`) to test all states before real AI integration exists.
- Verified all 5 states + empty-input validation + mobile responsiveness via builder screenshots.
- Decision: skip deployment today since the app doesn't yet do real extraction — will deploy once real functionality is wired in.
- Status: ✅ Complete.

## Day 5 — (Not yet started)
- Planned: Backend function & extraction prompt engineering — build the real Gemini prompt in `api/extract.js`, tested directly (not yet wired to the UI).

---

*This log is updated at the end of each day and lives in the `docs/` folder.*
