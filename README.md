# A/B Test Analysis — Marketing Campaign Effectiveness

> **Tools:** Python · Pandas · SciPy · Seaborn · Tableau  
> **Dataset:** [Marketing A/B Testing — Kaggle](https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing)
> **Live Dashboard:** [AB-Test-Marketing-Campaign-Sandeep-Singh — Tableau](https://public.tableau.com/authoring/AB-Test-Marketing-Campaign-Sandeep-Singh/Dashboard1#1)
> **Techniques:** Chi-Square Test · Confidence Intervals · Cohen's h · Difference-in-Differences (Causal Inference)

---

## Business Problem

An e-commerce company ran a digital marketing campaign and wanted to know:

> *Does showing users an advertisement actually cause more conversions — or would they have purchased anyway?*

Two groups were created:
- **Test group (Ad)** — users shown the new advertisement
- **Control group (PSA)** — users shown a Public Service Announcement (no commercial intent)

The goal was to measure whether the ad drove a **statistically significant and causally attributable** lift in conversion rate.

---

## Dataset Overview

| Attribute | Value |
|-----------|-------|
| Total users | 588,101 |
| Test group (Ad) | 564,577 users (96%) |
| Control group (PSA) | 23,524 users (4%) |
| Features | user_id, test_group, converted, total_ads, most_ads_day, most_ads_hour |
| Target variable | converted (0 = No, 1 = Yes) |

---

## Hypotheses

```
H₀ (Null)        : Conversion rate (Ad) = Conversion rate (PSA)
                   → The ad has NO effect on conversions

Hₐ (Alternative) : Conversion rate (Ad) ≠ Conversion rate (PSA)
                   → The ad DOES have a significant effect

Significance level (α) = 0.05
Test used              = Chi-Square Test of Independence
```

---

## Key Results

### Conversion Rates

| Group | Users | Conversions | Conversion Rate |
|-------|-------|-------------|-----------------|
| Test (Ad) | 564,577 | 14,423 | **2.5547%** |
| Control (PSA) | 23,524 | 420 | **1.7854%** |
| **Lift** | — | — | **+0.7693 pp (+43.09% relative)** |

### Statistical Test

| Metric | Value | Interpretation |
|--------|-------|----------------|
| Chi-Square (χ²) | 54.006 | Far above critical value of 3.84 |
| P-value | < 0.0001 | Reject H₀ at 99.99%+ confidence |
| Degrees of freedom | 1 | (2 groups − 1) × (2 outcomes − 1) |
| 95% Confidence Interval | [+0.5951%, +0.9434%] | Entire CI above zero → significant |
| Cohen's h | 0.0530 | Small effect size |
| Statistical Power | 100% | Sample size far exceeds minimum needed |

**Conclusion:** The ad produced a statistically significant 43% relative lift in conversion rate. The result holds at the 99.99%+ confidence level.

### Causal Inference — Difference-in-Differences

To isolate the ad's **true causal effect** from background market trends, a Difference-in-Differences (DiD) analysis was applied using ad exposure quartiles as a time proxy.

```
DiD = (Ad_post − Ad_pre) − (PSA_post − PSA_pre)
    = (4.8055% − 0.3761%) − (3.3782% − 0.4047%)
    = +1.4559 pp
```

**Interpretation:** After controlling for pre-existing conversion trends, the advertisement caused a **+1.46 percentage point increase** in conversion rate — confirming causation, not just correlation.

---

## Analysis Steps

```
1. Data Loading & Inspection       → Shape, nulls, duplicates, group distribution
2. Data Cleaning & Feature Eng.   → Convert booleans, create ad exposure quartiles, hour buckets
3. Descriptive Statistics          → Conversion rates, absolute lift, relative lift
4. Hypothesis Test (Chi-Square)    → Contingency table, χ², p-value
5. Confidence Interval             → 95% CI for rate difference
6. Effect Size & Power             → Cohen's h, statistical power
7. Segmentation Analysis           → By day of week, time of day, ad exposure quartile
8. Visualisations                  → 4 publication-quality Seaborn charts
9. Diff-in-Diff Causal Inference   → True causal effect isolated from trends
10. Business Recommendation Report → Findings, strategy, risk flags, next steps
```

---

## Visualisations

| Figure | Description |
|--------|-------------|
| `fig1_executive_overview.png` | Conversion rates, user volume, ad exposure KDE, quartile breakdown |
| `fig2_statistical_evidence.png` | 95% CI bars, chi-square distribution, conversion waterfall |
| `fig3_segment_deep_dive.png` | Conversion by day of week and time of day |
| `fig4_diff_in_diff.png` | Causal inference chart with counterfactual line |

---

## Business Recommendations

1. **Scale the ad campaign** — The ad is causally driving conversions at 99.99%+ confidence. Recommend increasing budget allocation to the ad format.
2. **Optimise ad scheduling** — Segmentation reveals conversion rates vary by day and time. Reallocate impressions to peak-performance windows to maximise ROI without increasing total spend.
3. **Set a frequency cap** — Users in the highest ad exposure quartile (Q4) show strong lift. Monitor for ad fatigue beyond this threshold and A/B test a frequency cap.
4. **Run monthly hold-out tests** — Maintain a 5% control group continuously to track whether lift is sustained or diminishing as the campaign matures.

---

## Risk Flags

- **Imbalanced experiment design** — 96% ad vs 4% PSA is far from the ideal 50/50 split. The small PSA group widens confidence intervals and reduces statistical power. Future experiments should aim for balanced groups.
- **No revenue data** — This dataset captures binary conversion (yes/no), not order value. Recommend augmenting with AOV data to calculate true ROAS (Return on Ad Spend) before scaling budget decisions.

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/SandeepSingh/ab-testing-marketing.git
cd ab-testing-marketing

# 2. Install dependencies
pip install pandas numpy scipy seaborn matplotlib

# 3. Download dataset from Kaggle and place in project folder
# https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing

# 4. Run the analysis
python ab_testing_project.py

# OR open in Jupyter
jupyter notebook Ab testing.ipynb
```

---

## Project Structure

```
ab-testing-marketing/
│
├── Ab testing.ipynb                    # Main analysis notebook
├── ab_testing_project.py              # Standalone Python script
├── marketing_AB.csv                   # Dataset (download from Kaggle)
│
├── figures/
│   ├── fig1_executive_overview.png
│   ├── fig2_statistical_evidence.png
│   ├── fig3_segment_deep_dive.png
│   └── fig4_diff_in_diff.png
│
└── README.md
```

---

## Skills Demonstrated

`Python` `Pandas` `SciPy` `Seaborn` `Matplotlib` `Tableau`  
`A/B Testing` `Hypothesis Testing` `Chi-Square Test` `Confidence Intervals`  
`Cohen's h` `Statistical Power` `Difference-in-Differences` `Causal Inference`  
`Customer Segmentation` `Data Storytelling` `Business Recommendations`

---

## Author

**Sandeep Singh** — Data Analyst  
[LinkedIn](https://linkedin.com/in/SandeepSingh) · [GitHub](https://github.com/SandeepSingh)
