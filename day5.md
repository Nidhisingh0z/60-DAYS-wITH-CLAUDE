Prompt A output (no context)
Week 1 – Foundations: Pick a beginner-friendly topic (generic placeholder: "a new skill"). Daily tasks: watch an intro tutorial, take notes, do basic exercises. Resources: a general "search for free tutorials on YouTube/Coursera." Project: none specified — "try a small practice exercise."
Week 2 – Core concepts: Continue tutorials, read documentation, practice daily for ~1 hour (assumed, not specified). Resources: "official documentation," "online courses."
Week 3 – Application: Build a small project applying what you've learned. Resources: "project-based tutorials." No detail on what kind of project fits your goal.
Week 4 – Mastery and review: Build a capstone project, review weak areas, share work for feedback.
Final outcome: "You'll have a solid foundation and a project to show for it."
This is generic because it has no idea what skill, what time budget, or what learning style to assume — so it defaults to vague placeholders like "watch tutorials" and "build a project" without specifics.
Prompt B output (with context filled in)
Week 1 – Python & data basics (goal: comfort with syntax + pandas basics)

Day 1–2: Python syntax via a short video course (Excel comparisons help bridge intuition) — 1.5 hrs/day
Day 3–4: Data structures (lists, dicts) + intro to Jupyter notebooks
Day 5–6: pandas basics — reading CSVs, filtering, sorting (you already know this conceptually from Excel)
Day 7: Mini project — import a CSV (e.g. sales data) and replicate 3 things you'd normally do in Excel
Resources: freeCodeCamp's Python video course, pandas official 10-minute intro
Milestone: can load and manipulate a dataset in pandas without looking up every command

Week 2 – Data cleaning & visualization

Daily: 1.5 hrs split between a video lesson and hands-on practice in a notebook
Topics: handling missing data, groupby, merging datasets, matplotlib/seaborn basics
Project: clean a messy public dataset (e.g. Kaggle's "Titanic" or a sample sales dataset) and produce 3 charts
Resources: Kaggle's "Pandas" and "Data Visualization" micro-courses (free, project-based, matches your video+project preference)
Milestone: a cleaned dataset + visual summary you could show a colleague
Week 3 – Analysis & storytelling

Daily: apply pandas/visualization skills to answer specific business questions on a dataset
Project: pick a dataset relevant to your work domain, define 3 questions, answer them with code + charts
Resources: short videos on exploratory data analysis (EDA) workflow
Milestone: a notebook that tells a data story end-to-end

Week 4 – Capstone & polish

Day 1–3: Build a capstone analysis combining cleaning, EDA, and visualization on a new dataset
Day 4–5: Write a short summary/report of findings (practicing communicating to non-technical stakeholders, useful for your professional context)
Day 6–7: Polish, get feedback, post to GitHub or share with a peer
Resources: a free "portfolio project" guide video
Milestone: a presentable portfolio project

Final outcome: A GitHub repo with 2–3 data analysis projects demonstrating pandas, cleaning, and visualization skills — enough to discuss in a job conversation or apply directly to your current work, achievable in ~45 hours over 30 days at 1.5 hrs/day.
Comparison
1. More personalized: Prompt B, clearly. It tailors the pacing to 1.5 hrs/day, builds on your existing Excel knowledge instead of starting from zero, picks projects relevant to a "professional" context rather than generic exercises, and leans on video + project resources instead of dumping a mix of formats you didn't ask for.
2. Which I'd actually follow: Prompt B's roadmap is the one a real person could start tomorrow — it tells you exactly what to watch, what to build, and how long each step takes. Prompt A's roadmap requires you to do all the personalization work yourself (choosing topics, resources, project scope) before you could even start, which defeats the purpose of asking for a roadmap.
3. Role of context: Context did three things that genuinely changed the output rather than just adding flavor text. It set the scope (data analysis with Python, not "a skill"), it set realistic pacing (tasks sized to 1.5 hrs instead of an assumed arbitrary amount), and it let the plan build on prior knowledge (Excel → pandas analogies) instead of treating you as a blank slate. Without context, the model has to either guess (and risk being wrong) or stay vague (and be useless) — Prompt A chose vague, which is the safer but less helpful failure mode.
