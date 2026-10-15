# FlyRank AI Machine Learning Internship — Reflection & Experience

- **Track:** Machine Learning
- **Lane:** Content Refresh Ranking
- **Repository:** https://github.com/abdulrehman-mk/FlyRank_ml_Internship

## Experience & Reflection
Participating in the FlyRank AI Machine Learning Internship was an invaluable journey from theoretical concepts to building real-world, production-ready ML systems. Working with anonymized search data allowed me to tackle genuine search visibility decay challenges without relying on toy datasets or oversimplified heuristics.

## Key Learnings & Takeaways
- **Rigorous Problem Framing & Data Hygiene:** Learned how to structure a real-world search intelligence problem, define clear data contracts, and audit signals before writing a single line of model code.
- **Leakage Prevention & Honest Validation:** Mastered the importance of client-holdout validation splits to ensure models generalize safely across unseen domains without data leakage.
- **Baseline vs. Complexity:** Understood that machine learning should only be introduced when it beats a transparent, hand-written baseline. Achieving a **3.1x lift in Precision@50** (0.740 vs 0.240) with a Random Forest classifier proved the tangible value of learned models over static rules.
- **Translating Code into Insights:** Learned to communicate technical findings through structured research reporting, handling false positives/negatives through rigorous error analysis rather than relying solely on metrics tables.

## Structure
- `data/` — Raw and processed search performance datasets.
- `submission/` — Contains `paper_url.txt` linking to the capstone report.
- `work/` — Weekly assignment notebooks, outputs, and `capstone_report.md`.
- `requirements.txt` — Project dependencies.

## Results Summary
- **Baseline Rule (Precision@50):** 0.240
- **Random Forest Model (Precision@50):** 0.740 (~3.1x lift)

## Reproducibility
1. Clone the repo: `git clone https://github.com/abdulrehman-mk/FlyRank_ml_Internship`
2. Install dependencies: `pip install -r requirements.txt`
3. Execute notebooks in `work/notebooks/` sequentially.

## Acknowledgments
Built on the FlyRank ML Internship dataset (https://flyrank.ai).
