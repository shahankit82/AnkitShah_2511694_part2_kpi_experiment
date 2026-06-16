# Recommendation Memo
## Onboarding & Activation Campaign — A/B Test Decision

**To:** Leadership / Product & Growth Teams  
**From:** Business Analyst  
**Date:** 2025  
**Subject:** Launch Recommendation — New Onboarding & Activation Campaign

---

## Executive Summary

The new onboarding and activation campaign (Treatment) produced a **statistically significant 2.2× improvement** in paid conversion rate versus the existing experience (Control). The test result is robust (p=0.0017, χ²=9.88 with n=1,400). Engagement quality also improved significantly. Two guardrail metrics require monitoring post-launch — support ticket volume and revenue per converted user — but neither constitutes a blocker.

**Recommendation: LAUNCH to all users, with a support capacity plan and a 30-day post-launch monitoring window.**

---

## 1. Business Problem Statement

### Decision to be made
Whether to roll out the new onboarding and activation campaign to all users of the subscription-based digital product.

### Who it impacts
- **New users**: Every new signup will experience the Treatment onboarding if launched.
- **Revenue team**: Conversion rate directly affects subscription revenue.
- **Customer support team**: Treatment shows higher ticket volume, which affects operational capacity.
- **Product team**: Onboarding flow ownership and ongoing iteration.

### What metric should improve
**Paid Conversion Rate** — the proportion of new users who convert from free/trial to a paid subscription within 30 days.

### Risks to monitor
- Revenue per converted user (ARPCU) is significantly lower in Treatment.
- Support ticket volume is ~69% higher in Treatment.
- Refund rate is non-zero in Treatment (0 in Control).

### Evidence required before recommendation
A statistically significant improvement in paid conversion rate (p < 0.05), with guardrail metrics not deteriorating to a degree that offsets the conversion gain.

---

## 2. North Star Metric

**North Star: Paid Conversion Rate**

### Why this is the North Star
Paid conversion is the single metric that directly captures whether the campaign is achieving its business objective: turning new users into paying customers. It sits at the intersection of product effectiveness and revenue generation.

### Why other metrics are supporting, not North Star
- **Engagement score**: A leading indicator — high engagement without conversion generates no revenue.
- **Trial start rate / onboarding completion rate**: Funnel steps that matter only if they ultimately drive paid conversion.
- **ARPU**: Affected by the large pool of zero-revenue non-converters; less sensitive to campaign effect.

### Connection to business growth
Each 1 percentage point improvement in conversion across 10,000 monthly signups = ~100 additional paying customers per month. At average ARPCU of ~Rs 770, that is ~Rs 77,000 incremental monthly recurring revenue per cohort.

### Blind-spot risk
Optimising conversion rate alone could attract low-value converters (lower plan tiers, higher refund/churn rates). This is exactly what the ARPCU signal is warning about in this experiment — hence the importance of guardrail metrics.

---

## 3. KPI Tree Summary

The North Star (Paid Conversion Rate) breaks down into three primary driver pillars:

**1. Activation Funnel Depth**
- Landing page visit rate → Trial start rate → Onboarding completion rate
- All three improved meaningfully in Treatment

**2. Engagement Quality**
- Avg engagement score → Days to convert → Feature adoption rate
- Engagement score improved significantly (p<0.001); faster conversion observed

**3. Revenue Quality**
- ARPU → ARPCU → Revenue retention
- ARPU marginally improved; ARPCU declined — requires investigation

**Guardrail Metrics (monitoring boundaries):**
- Refund rate ≤ 2%
- Support ticket rate ≤ 20%
- Days to convert ≤ 14 days
- Engagement score floor ≥ 55
- No segment-level conversion regression

---

## 4. Experiment Result Summary

| Metric | Control | Treatment | Lift |
|---|---|---|---|
| User count | 690 | 710 | +20 |
| Landing page visit rate | 63.6% | 72.6% | +9.0 pp |
| Trial start rate | 25.1% | 29.2% | +4.1 pp |
| Onboarding completion rate | 15.6% | 21.3% | +5.7 pp |
| **Paid conversion rate ⭐** | **3.19%** | **7.04%** | **+3.85 pp (+121%)** |
| ARPU (30d) | Rs 51.97 | Rs 54.25 | +Rs 2.28 |
| ARPCU | Rs 1,630 | Rs 770 | −Rs 860 (−53%) |
| Refund rate | 0.00% | 0.42% | +0.42 pp |
| Support ticket rate | 13.6% | 22.7% | +9.1 pp |
| Avg engagement score | 57.03 | 62.94 | +5.91 |
| Avg days to convert | 8.9 days | 6.4 days | −2.5 days |

The full conversion funnel improved at every stage in Treatment. The paid conversion 2.2× lift is the headline result.

---

## 5. Hypothesis Test Interpretation

- **Test**: Chi-square test of independence on paid conversion rate (binary outcome)
- **H₀**: Conversion rates are equal across Control and Treatment
- **H₁**: Conversion rates differ (two-tailed)
- **χ² statistic**: 9.8782 | **p-value**: 0.0017 | **α**: 0.05
- **Result**: p < α → **Reject H₀**

The improvement is statistically significant. There is only a 0.17% probability this lift arose by chance. A supplementary Welch t-test on engagement score also confirmed significantly higher engagement in Treatment (p < 0.001, t = −7.93).

---

## 6. Guardrail Metric Analysis

| Guardrail | Control | Treatment | Status | Assessment |
|---|---|---|---|---|
| Refund rate | 0.00% | 0.42% | ⚠ WATCH | 3 refunds in Treatment vs 0. Low absolute risk but non-zero. Monitor post-launch. |
| Support ticket rate | 13.6% | 22.7% | ⚠ WATCH | ~69% more tickets per user. At scale, this materially impacts support cost and capacity. Mitigation required. |
| Avg days to convert | 8.9 days | 6.4 days | ✔ PASS | Faster conversion is a quality signal. No risk here. |
| Avg engagement score | 57.03 | 62.94 | ✔ PASS | Higher engagement is consistent with genuine campaign effectiveness. |
| ARPCU | Rs 1,630 | Rs 770 | ⚠ RISK | Treatment converters spend significantly less. This may reflect a shift toward lower-tier plan conversions (Basic/Free → Basic vs Premium). Requires a plan-mix breakdown before full revenue impact can be assessed. |
| Segment parity | Baseline | All regions positive | ✔ PASS | No region showed negative conversion lift. Safe to launch without geo-restriction. |

### ARPCU Risk Interpretation
The lower ARPCU in Treatment is a significant finding. Despite more conversions (50 vs 22), total Treatment revenue from converters is: 50 × Rs 770 = Rs 38,500 vs Control: 22 × Rs 1,630 = Rs 35,860. Total revenue is marginally higher in Treatment, but the per-user quality is lower. Post-launch, plan-type conversion distribution must be tracked to determine if the campaign is converting users to lower-value plans.

---

## 7. Segment-Level Insights

All four regions (North, South, East, West) showed positive conversion lift in Treatment. No region showed a negative effect, which confirms the campaign is safe to launch without any geographic segmentation.

By device type, Mobile and Desktop both showed positive lift. Tablet had limited sample size but no adverse signal.

By traffic source, Email and Organic traffic showed the strongest response to Treatment. Paid Search showed the weakest lift — this may indicate the campaign's messaging is better suited to warm/organic audiences.

By plan type, Free plan users showed the largest absolute lift. This is expected since Free → Paid is the primary conversion journey.

---

## 8. Final Recommendation

### Decision: **LAUNCH to all users**

The evidence clearly supports launch:
1. Paid conversion rate improved by 121% (p=0.0017) — statistically significant and practically meaningful.
2. All funnel stages improved.
3. Engagement quality increased (p<0.001).
4. Faster time to convert (6.4 vs 8.9 days).
5. No segment showed a negative effect.

The guardrail concerns (support volume, ARPCU) do not outweigh the conversion gain but must be actively managed.

---

## 9. Risks and Limitations

| Risk | Likelihood | Severity | Mitigation |
|---|---|---|---|
| ARPCU decline reflects permanent plan-mix shift | Medium | High | Monitor plan-type conversion breakdown monthly for 90 days |
| Support volume cannot scale | Medium | Medium | Pre-brief support team; add proactive in-app help for common issues raised in Treatment tickets |
| Novelty effect inflating conversion | Low | Medium | Re-measure at 60d cohort; compare 30d vs 60d conversion rates |
| Refund rate grows at scale | Low | Medium | Set refund rate alert at 1.5%; auto-pause campaign if breached |
| Paid Search audience not responding well | Medium | Low | A/B test campaign messaging separately for Paid Search channel |

### Limitations
- Experiment ran for a single time window; seasonal effects not controlled.
- 8 duplicate user_ids were removed; root cause unknown (may indicate system bugs).
- 18 missing device_type and 24 missing traffic_source records excluded from segment analysis.
- ARPCU interpretation is limited without plan-type breakdown of converters.

---

## 10. Next Steps

1. **Immediately**: Brief support team on expected volume increase; add in-app contextual help for top ticket topics from Treatment group.
2. **At launch**: Track daily: conversion rate, refund rate, support ticket volume, plan-type mix of conversions.
3. **30 days post-launch**: Full cohort review — ARPCU, 30d retention, refund rate at scale.
4. **60 days**: Assess whether conversion lift sustains (novelty check) and whether ARPCU recovers as premium-plan users convert later.
5. **Ongoing**: Consider personalising onboarding by traffic source — particularly a separate variant for Paid Search audiences.
