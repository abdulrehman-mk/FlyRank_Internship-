# Capstone Report — Refresh / Content Opportunity Scoring

- **Author:** Abdul Rehman
- **Lane:** Content Refresh Ranking (Lane 1)
- **Repo:** https://github.com/abdulrehman-mk/FlyRank_Internship-
- **Date:** October 2026

## 0. Abstract
How can digital publishers prioritize decaying web pages for content updates using machine learning? We analyzed 30,000 anonymized search performance records to engineer non-linear traffic and staleness features. We trained a Random Forest Classifier evaluated on a client-holdout validation split to prevent data leakage. The Random Forest model achieved a Precision@50 of 0.740, delivering a ~3.1x lift over the hand-written rule baseline (0.240). This model provides an automated ranking engine to optimize editorial refresh workflows.

## 1. Problem framing
This work supports editorial resource allocation decisions for web page updates. The unit of analysis is the individual web page (`content_id`), and the output is a ranked priority queue (`refresh_queue.csv`). Editors use this to refresh stale content, while wrong calls lead to wasted editorial hours on stable pages or missed traffic recovery. Machine learning improves this decision by capturing complex, non-linear interactions between search volume, position decay, and staleness.

## 2. Data safety
We used the anonymized search performance dataset (`content_refresh_anonymized.csv`) containing 30,000 rows. We deliberately excluded target-derived percentage shifts (`trend_pct`) and internal health scores to prevent data leakage. Pseudonymous client IDs were used strictly for grouped validation splits, never as training features. No proprietary client names, domain URLs, or query strings exist anywhere in `work/`.

## 3. Baseline
Our baseline is a hand-written rule scoring pages that cross a 180-day staleness threshold and have at least 500 impressions. Evaluated on the exact same holdout split, the rule achieved a Precision@50 of 0.240 (~12 of the top 50 correctly identified as declining).

## 4. Model / analysis
We selected a Random Forest Classifier because it captures non-linear relationships among heavy-tailed search metrics and resists overfitting. Features used: `content_age_days`, `days_since_last_update`, `impressions_90d`, `avg_position`, `ctr`, and `word_count`. The target proxy is `is_declining` (1 for pages in a downward performance trend, 0 otherwise).

## 5. Evaluation
We used a client-holdout validation split (20% test holdout) so that test client pages are never seen during training. On the same split, Random Forest achieved Precision@50 of 0.740 compared to the baseline's 0.240. Error analysis reveals false positives primarily occur on seasonal queries, while false negatives happen on pages experiencing sudden competitor shifts not captured by content age.

## 6. Interpretation
The model primarily relies on `impressions_90d` and `days_since_last_update` to identify decay risk. A key negative finding was that `word_count` has a near-zero correlation with traffic decline, disproving the belief that longer articles inherently resist decay.

## 7. Recommendation
Editors should prioritize high-probability pages identified by the model, specifically focusing on high-exposure pages unupdated for over 180 days. Claims are framed strictly as decision-support guidance rather than causal guarantees of search algorithm changes.

## 8. Reproducibility
To reproduce the results:
1. Clone the repo: `git clone https://github.com/abdulrehman-mk/FlyRank_Internship-`
2. Install dependencies: `pip install -r requirements.txt`
3. Execute notebooks sequentially in `work/notebooks/` (w01 through w05).
All splits use `random_state=42`.

## 9. Acknowledgments & data credit
Built on the FlyRank ML Internship dataset ([https://flyrank.ai](https://flyrank.ai)).
