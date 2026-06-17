# Final Capstone Project

# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

## Business Context

A subscription-based digital product company ran an A/B test to evaluate a new onboarding and activation campaign. Users were split into:
- **Control** (n=690): Existing onboarding experience
- **Treatment** (n=710): New campaign experience

Leadership needs a data-backed decision on whether to launch the Treatment to all users.

---

## Dataset Description

| Attribute | Value |
|---|---|
| File | `campaign_experiment_data.xlsx` |
| Raw rows | 1,408 |
| After deduplication | 1,400 |
| Columns | user_id, experiment_group, visited_landing_page, started_trial, completed_onboarding, converted_to_paid, revenue_30d, refund_requested, support_tickets_30d, engagement_score, days_to_convert, region, device_type, traffic_source, plan_type |
| Segments | Region (4), Device Type (3), Traffic Source (4), Plan Type (3) |

### Data Quality Findings
| Issue | Count | Action |
|---|---|---|
| Duplicate user_ids | 8 | Removed (kept first occurrence) |
| Missing device_type | 18 | Excluded from device segment analysis |
| Missing traffic_source | 24 | Excluded from traffic segment analysis |
| Missing engagement_score | 14 | Excluded from engagement t-test |
| Invalid binary values | 0 | None found |
| Revenue outliers (>2500) | 1 (Control) | Retained — legitimate high-value converter |

---

## North Star Metric Selected

**Paid Conversion Rate** — proportion of users in each group who converted to a paid subscription within 30 days.

### Rationale
- Directly measures the campaign's primary business objective
- Binary outcome → clean statistical testing via chi-square
- Drives subscription revenue and business growth
- All other metrics (engagement, trial start, onboarding completion) are upstream drivers or guardrails

### Risk of blind optimisation
Optimising conversion rate alone risks attracting low-value converters on cheaper plans — exactly what the ARPCU guardrail flagged in this experiment (Treatment ARPCU: Rs 770 vs Control: Rs 1,630).

---

## KPI Tree Summary

```
⭐ NORTH STAR: Paid Conversion Rate
│
├── ACTIVATION FUNNEL DEPTH
│   ├── Landing Page Visit Rate
│   ├── Trial Start Rate
│   └── Onboarding Completion Rate
│
├── ENGAGEMENT QUALITY
│   ├── Avg Engagement Score
│   ├── Days to Convert
│   └── Feature Adoption Rate
│
└── REVENUE QUALITY
    ├── ARPU (Avg Revenue per User)
    ├── ARPCU (Avg Revenue per Converted User)
    └── Revenue Retention

🛡 GUARDRAIL METRICS
├── Refund Rate (≤ 2% threshold)
├── Support Ticket Rate (≤ 20% target)
├── Days to Convert (≤ 14 days)
├── Engagement Score (≥ 55 floor)
└── Segment-Level Conversion Parity
```

Full visual: `outputs/kpi_tree.png`

---

## Experiment Analysis Approach

1. **Data cleaning**: Removed 8 duplicate user_ids; validated all binary columns; checked revenue outliers; confirmed segment balance across groups.
2. **Metric calculation**: Computed all 11 required metrics per group (conversion rates, ARPU, ARPCU, refund rate, support rate, engagement, days to convert).
3. **Segment analysis**: Broken down paid conversion rate by Region, Device Type, Traffic Source, and Plan Type.
4. **Guardrail evaluation**: Assessed 6 guardrail dimensions against pre-defined thresholds.

---

## Hypothesis Test Summary

| Parameter | Value |
|---|---|
| Test | Chi-square test of independence |
| Metric | Paid Conversion Rate |
| H₀ | Conversion rates are equal (Control = Treatment) |
| H₁ | Conversion rates differ (two-tailed) |
| Significance level | α = 0.05 |
| χ² statistic | 9.8782 |
| p-value | **0.0017** |
| Decision | **Reject H₀** — result is statistically significant |

**Secondary test**: Welch t-test on engagement score — t = −7.93, p < 0.001 (also significant).

---

## Key Experiment Results

| Metric | Control | Treatment | Lift |
|---|---|---|---|
| Paid Conversion Rate ⭐ | 3.19% | 7.04% | +3.85 pp (+121%) |
| Landing Page Visit Rate | 63.6% | 72.6% | +9.0 pp |
| Trial Start Rate | 25.1% | 29.2% | +4.1 pp |
| Onboarding Completion Rate | 15.6% | 21.3% | +5.7 pp |
| ARPU | Rs 51.97 | Rs 54.25 | +Rs 2.28 |
| ARPCU | Rs 1,630 | Rs 770 | −Rs 860 ⚠ |
| Avg Engagement Score | 57.03 | 62.94 | +5.91 |
| Avg Days to Convert | 8.9d | 6.4d | −2.5d |
| Support Ticket Rate | 13.6% | 22.7% | +9.1 pp ⚠ |
| Refund Rate | 0.00% | 0.42% | +0.42 pp ⚠ |

---

## Guardrail Metrics Considered

| Guardrail | Status | Notes |
|---|---|---|
| Refund rate | ⚠ WATCH | 3 refunds in Treatment vs 0 in Control |
| Support ticket rate | ⚠ WATCH | ~69% more tickets per user at Treatment scale |
| Days to convert | ✔ PASS | Faster is better — 6.4d vs 8.9d |
| Engagement score | ✔ PASS | Significantly higher (p<0.001) |
| ARPCU | ⚠ RISK | 53% lower per-converter revenue — plan mix investigation needed |
| Segment parity | ✔ PASS | All regions, devices, and traffic sources show positive lift |

---

## Final Recommendation

**LAUNCH to all users** — with active post-launch monitoring.

- Paid conversion rate improved by 121% (statistically significant, p=0.0017)
- Full funnel improved at every stage
- Engagement quality significantly higher
- Faster time to conversion
- No segment showed negative lift

**Action items:**
1. Brief support team on volume increase before launch
2. Set refund rate alert at 1.5%
3. Track plan-type mix of conversions daily post-launch
4. Review 30-day and 60-day cohort data to confirm lift sustains

---

## Assumptions and Limitations

- Experiment covers a single time window — seasonal effects not controlled
- 8 duplicate user_ids removed; root cause unknown
- ARPCU interpretation limited without plan-type breakdown of converters
- Novelty effects may partially inflate early conversion lift
- Paid Search segment showed weakest response — may need separate messaging

---

## Screenshots Included

| File | Shows |
|---|---|
| `screenshots/summary_metrics.png` | Full Control vs Treatment metrics table |
| `screenshots/hypothesis_test_output.png` | Chi-square contingency table, test output, and conversion funnel chart |
| `screenshots/kpi_tree_preview.png` | Full KPI tree with North Star, primary drivers, sub-drivers, and guardrails |

---

## Repository Structure

```
part2_kpi_experiment/
├── data/
│   └── campaign_experiment_data.xlsx
├── analysis/
│   ├── experiment_analysis.xlsx    ← Data quality + group summary + segment analysis
│   └── hypothesis_test_notes.md   ← Full hypothesis test documentation
├── outputs/
│   ├── kpi_tree.png               ← KPI tree visual
│   ├── experiment_summary.xlsx    ← Summary + segment + guardrail sheets
│   └── recommendation_memo.md     ← Full decision memo
├── screenshots/
│   ├── summary_metrics.png
│   ├── hypothesis_test_output.png
│   └── kpi_tree_preview.png
└── README.md
```
