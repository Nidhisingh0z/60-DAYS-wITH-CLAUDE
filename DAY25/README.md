🦈 Day 25 of my Claude journey — built an AI Shark Tank Simulator.

Pitch your startup. Get grilled by 4 AI judges. Walk away with a deal (or without one).

Here's what's inside:

→ Enter your Startup Name, Problem, Solution, Revenue Model, Target Audience, and Funding Ask → 4 distinct AI sharks — a VC (market size), a Founder (execution), a Customer (usefulness), and an Angel Investor (profitability) — each ask you 2 pointed questions and react in character to your answers, live → A 5-part scorecard: Market Potential, Innovation, Business Model, Execution, Investment Worthiness → A real verdict: Invest, Acquire, Reject, or Come Back Later — with a suggested valuation, funding amount, and the sharks' reasoning → Confetti when you land the deal, a downloadable PDF pitch report, a live leaderboard, and one-tap sharing

The whole thing is a single self-contained HTML file — no backend, no install. Open it and you're in the tank.

The most interesting part wasn't the UI — it was designing 4 judges who actually disagree with each other for different reasons, and making sure the experience still works end-to-end even if the AI call fails (every response has a solid fallback).

25 days in, and building with Claude keeps teaching me the same lesson: the hard part was never the code. It's the thinking before the code.

A few things worth knowing about how it's built:

Flow: Surface (pitch form) → 20 Fathoms (pitch review + judge intros) → 60 Fathoms (8 questions, 2 per shark, with live "interest" meters that shift per answer) → 100 Fathoms (animated scorecard) → The Floor (verdict, deal terms, per-judge calls, reasoning).
AI-driven: questions, in-character reactions, and the final scoring/verdict/valuation are generated live by calling Claude directly from the page. Every call has a heuristic fallback (word-richness scoring, canned reaction banks, rule-based valuation math), so the simulator still fully works even if that call fails — genuinely no backend required.
Bonus features: confetti fires on Invest/Acquire, a downloadable PDF pitch report (jsPDF), a Share button (native share sheet or clipboard fallback), and a leaderboard stored via persistent shared storage so pitches rank across sessions/users.
Design: dark "deep sea" theme (navy/teal/gold/coral), a fathom-depth rail instead of generic step numbers, shark fins that surface, and conic-gradient score gauges — fully responsive down to mobile.

I validated the JS syntax and confirmed every element ID referenced in script matches one defined in the HTML, so it should load cleanly when opened.

<img width="1882" height="1013" alt="Screenshot 2026-07-21 110850" src="https://github.com/user-attachments/assets/c660616b-421c-404c-8186-20821bba7dda" />
