Day 28 of building healthcare simulators 🏥

Today's build: a Hospital Admission Readiness Simulator — a training tool for admission coordinators to practice the real workflow of getting a patient from "referred" to "admitted."

It models the messy middle: prior auth stuck in Pending vs. Denied (each with its own recovery path), insurance verification, bed assignment, documentation, physician orders, and consent — all rolled into a live weighted readiness score.

A few details I liked getting right:
→ The CMS 2-Midnight Rule banner auto-triggers for Observation admissions
→ InterQual/Milliman medical necessity notes surface for Acute MI/CHF
→ An ICU admission with a denied PA literally cannot cross 70% readiness from admin work alone — it forces the appeal path
→ Care coordination cards for Attending, Case Manager, Nursing, UR, and Discharge Planning update live as the case progresses

Nothing here uses real provider or payer data — pure simulation for training reps and coordinators on the operational logic behind "can we admit this patient yet?"

#buildinpublic #healthtech #healthcareIT #100DaysOfCode

SCREENSHOTS:
<img width="1897" height="847" alt="Screenshot 2026-07-23 110253" src="https://github.com/user-attachments/assets/7915f01a-4fae-4089-a179-012a5d4eb142" />

<img width="1532" height="862" alt="Screenshot 2026-07-23 110406" src="https://github.com/user-attachments/assets/8ce4b0f5-b364-49c5-9ea8-a9c76769d123" />

<img width="1671" height="1000" alt="Screenshot 2026-07-23 110424" src="https://github.com/user-attachments/assets/cf75d48e-7cca-49bd-9c82-019ec68940d2" />

<img width="1527" height="912" alt="Screenshot 2026-07-23 110438" src="https://github.com/user-attachments/assets/6e5ffad4-3465-4162-a8d8-6e789d3dd8e8" />

<img width="1653" height="1032" alt="Screenshot 2026-07-23 110451" src="https://github.com/user-attachments/assets/19ce155f-3631-4d77-b4f1-7f35f748c805" />

