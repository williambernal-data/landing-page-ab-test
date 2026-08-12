# Landing Page A/B Test — Conversion & Revenue Impact Analysis

Statistical evaluation of two landing page variants (A/B), built to give a marketing team a data-backed answer to a single business question: **which version should we ship?** Based on a 40,000-user experiment dataset.

> **Note:** the underlying dataset is not included in this repository. The notebook is provided with all outputs (tables, charts, and results) already generated, so the full analysis can be reviewed directly on GitHub without re-running any code.

## Business Problem

A product team ran a one-month A/B test on their landing page and needed a clear, statistically defensible recommendation:

> **Which landing page variant should be shipped — and how confident can we be in that decision?**

Beyond a simple "which one wins," the analysis also needed to tell the team *where* the advantage comes from (conversion volume, transaction value, or both) and whether other factors — traffic channel, user type — should shape a more targeted rollout strategy.

## Key Business Findings

- **Variant B wins on both conversion and spend.** It converts **15.96%** of users vs. **12.57%** for Variant A (p = 3.76e-22), and converted users spend **$68.75** on average vs. **$61.09** for Variant A (p = 3.63e-21) — a 12.5% lift in transaction value. Both differences are statistically significant, not noise.
- **Combined revenue impact is material.** At scale, Variant B is estimated to generate ~339 additional conversions and ~$7,660 in extra revenue per 10,000–1,000 users respectively, relative to Variant A.
- **Traffic source has a real, but modest, effect on conversion** (χ² = 8.662, p = 0.034). Email (14.99%) and Ads (14.74%) edge out Organic (13.79%) and Referral (13.88%) — but the test doesn't confirm which specific channel pairs differ, so this is a signal to test further, not a reason to shift budget yet.
- **User type doesn't matter.** New and returning users convert at statistically indistinguishable rates (14.36% vs. 14.09%, p = 0.474) — segmenting the landing page by user history isn't supported by the data.

## Recommendation

Ship **Variant B**. Both the conversion-rate and average-spend advantages are statistically significant and directionally consistent, making a combined case that's stronger than either metric alone. Traffic-channel differences are worth a follow-up experiment before reallocating marketing budget; user-type segmentation isn't worth pursuing based on this data.

## Methodology

- Data validation and quality checks (types, duplicates, missing values, category consistency)
- **Welch's t-test** (after a Levene's test for variance equality) to compare average spend between converted users in each variant
- **Z-test for proportions** to compare conversion rates between variants
- **Chi-square tests of independence** to evaluate traffic source and user type against conversion
- Grouped and stacked bar charts to visualize both absolute volume and relative conversion rate by category
- Explicit statistical decision (reject/fail to reject H₀) paired with a business interpretation for every test

## Repository Structure

```
├── notebooks/
│   └── landing_page_ab_test_analysis.ipynb   (includes all outputs)
├── requirements.txt
└── README.md
```

## Tech Stack

Python · pandas · SciPy · statsmodels · seaborn · matplotlib · Jupyter

## Limitations

The experiment covers a single month (January 2026), so seasonal effects can't be ruled out without a post-launch monitoring period. The traffic-source chi-square test establishes a global association but doesn't pinpoint which channel pairs differ significantly — pairwise testing would be needed before acting on channel-level budget decisions.

## Next Steps

- Monitor Variant B's performance in production for 30–60 days to confirm the lift holds outside the test window
- Design channel-specific experiments to validate which traffic sources genuinely outperform others
- Track downstream metrics (retention, repeat purchase) for users converted under each variant

---

**Author:** William Andrés Bernal Sosa — [GitHub](https://github.com/williambernal-data)
