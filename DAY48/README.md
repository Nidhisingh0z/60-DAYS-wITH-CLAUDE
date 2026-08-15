Day 48/100 🔨

Build The Verdict Engine
The AI that renders a verdict on your toughest decisions

Today I built a tool that ends the "which laptop should I actually buy" spiral — a live Compare & Decide Engine for budget/student laptops.

The idea: most comparison tools give you a wall of specs and expect you to do the math yourself. This one does the math for you, live, based on what YOU actually care about.

𝗪𝗵𝗮𝘁 𝗶𝘁 𝗱𝗼𝗲𝘀:
→ Compares 4 real laptops — MacBook Air M4, Dell Inspiron 15, Lenovo IdeaPad Slim 5, ASUS Vivobook 15
→ Drag sliders to weight what matters — price, RAM/storage, performance, battery
→ Ranking updates instantly as you adjust priorities
→ Every single data point is sourced and linked — Apple.com, Dell.com, Geekbench, NanoReview, Notebookcheck, no invented numbers

𝗧𝗵𝗲 𝗽𝗮𝗿𝘁 𝗜'𝗺 𝗺𝗼𝘀𝘁 𝗽𝗿𝗼𝘂𝗱 𝗼𝗳:
It's honest about what it doesn't know. I couldn't find an independent battery test for one of the laptops — so instead of making up a number to fill the gap, the tool flags it "Not independently tested" and scores it neutral rather than penalizing (or flattering) it. There's also a "How this was researched" panel that shows the actual conflicts I had to resolve — like a manufacturer's battery claim vs. what real owners report.

Verdict engines are only trustworthy if they show their work. An AI tool that quietly smooths over gaps in the data isn't helping you decide — it's just guessing with better formatting.

Built with plain HTML/CSS/JS, zero external libraries, fully responsive.


SCREENSHOTS:
<img width="1604" height="1024" alt="Screenshot 2026-08-15 192710" src="https://github.com/user-attachments/assets/8ed93793-1e28-4d50-9222-50d9532b19c6" />
<img width="1681" height="1021" alt="Screenshot 2026-08-15 192720" src="https://github.com/user-attachments/assets/a868d81c-00fe-4bfb-a218-670165f8c776" />
<img width="1625" height="991" alt="Screenshot 2026-08-15 192728" src="https://github.com/user-attachments/assets/14f27139-2ae5-40ae-834f-bc4f3da583d5" />
<img width="1687" height="982" alt="Screenshot 2026-08-15 192738" src="https://github.com/user-attachments/assets/90d19d85-2a98-41b5-9a09-74bc7a7b1151" />

