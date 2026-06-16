# Hypothesis Test Notes — Onboarding & Activation Campaign

## 1. Business Context

The company ran an A/B test comparing a new onboarding and activation campaign (Treatment) against the existing experience (Control). Leadership needs to decide whether to roll out the Treatment to all users. This test determines whether the Treatment produced a statistically meaningful improvement in the primary metric before a go/no-go decision is made.

---

## 2. Metric Selected for Hypothesis Test

**Primary metric: Paid Conversion Rate**  
(Users who converted to paid / total users in each group)

### Why this metric?
- It is the North Star metric for this campaign — the direct measure of whether users are moving from free/trial to paying customers.
- It directly connects to revenue and business growth.
- It is a binary outcome (converted = 1, not converted = 0), making it well-suited to a chi-square test of proportions.
- Upstream funnel metrics (landing page visit, trial start, onboarding completion) matter but are intermediate; paid conversion is the terminal business outcome.

### Why not other metrics?
- **Landing page visit rate / trial start rate**: These are leading indicators but not the revenue outcome. A user can visit and never pay.
- **Engagement score**: Continuous metric — valuable as a guardrail, but not the financial signal leadership needs.
- **ARPU**: Revenue per user includes many non-converters (zero revenue), making it noisy. Conversion rate is cleaner for this test.

---

## 3. Hypotheses

**H₀ (Null Hypothesis):**  
The paid conversion rate in the Treatment group is equal to that in the Control group.  
`p_treatment = p_control`

**H₁ (Alternative Hypothesis):**  
The paid conversion rate in the Treatment group is different from that in the Control group.  
`p_treatment ≠ p_control`

### Test type: Two-tailed
While we hope the Treatment improves conversion, a two-tailed test is used because:
- We want to detect any significant difference, including unexpected harm.
- Best practice in A/B testing is to use two-tailed tests to avoid directional bias.

### Significance level: α = 0.05
A 5% significance level is the industry standard for A/B experiments. This means we accept a 5% probability of falsely concluding the treatment works when it does not (Type I error).

---

## 4. Test Setup

| Parameter | Value |
|---|---|
| Test type | Chi-square test of independence |
| Groups | Control (n=690), Treatment (n=710) |
| Metric | Paid conversion rate (binary 0/1) |
| Significance level | α = 0.05 |
| Degrees of freedom | 1 |
| Tails | Two-tailed |

### Contingency Table

|               | Converted | Not Converted | Total |
|---------------|-----------|---------------|-------|
| **Control**   | 22        | 668           | 690   |
| **Treatment** | 50        | 660           | 710   |
| **Total**     | 72        | 1,328         | 1,400 |

### Observed Conversion Rates
- Control: 22 / 690 = **3.19%**
- Treatment: 50 / 710 = **7.04%**
- Absolute lift: **+3.85 percentage points**
- Relative lift: **+120.7% (2.2× improvement)**

---

## 5. Test Output

| Output | Value |
|---|---|
| Chi-square statistic (χ²) | 9.8782 |
| Degrees of freedom | 1 |
| p-value | **0.001672** |
| Critical value (α=0.05) | 3.841 |
| Decision rule | Reject H₀ if p < 0.05, or χ² > 3.841 |

---

## 6. Decision Rule and Result

**Since p-value (0.0017) < α (0.05): Reject H₀**

The difference in paid conversion rates between Control and Treatment is **statistically significant**. The probability of observing a lift this large by random chance (if H₀ were true) is only 0.17% — well below the 5% threshold.

---

## 7. Business Interpretation

The Treatment (new onboarding and activation campaign) produced a statistically significant 2.2× improvement in paid conversion rate. This is not due to random variation.

**In practical terms:**
- If this lift holds at scale (690 → 710 user ratio), the Treatment would generate approximately 28 additional paid conversions per 1,400 users.
- Extrapolated to 10,000 users: ~385 additional paid conversions vs ~319 under Control.

**Caveats to this test result:**
1. Statistical significance does not mean the decision is simple — guardrail metrics (ARPCU, support tickets) must be evaluated alongside this result.
2. The test covers a single time period; novelty effects may inflate the Treatment lift early on.
3. The sample sizes are moderate (690/710); replication with a larger cohort would further strengthen confidence.
4. Days-to-convert data suggests Treatment converters act faster (6.4 vs 8.9 days), which is consistent with a genuine campaign effect rather than a delayed measurement artefact.

---

## 8. Secondary Test: Engagement Score

A supplementary Welch t-test was performed on engagement score (continuous variable):

- **H₀**: Mean engagement score is equal across groups
- **H₁**: Means differ
- t-statistic: −7.9275
- p-value: < 0.0001
- **Result: Reject H₀** — Treatment users have significantly higher engagement (62.94 vs 57.03)

This corroborates the conversion result: Treatment users are more engaged AND more likely to convert, suggesting the campaign is genuinely improving user quality, not just pushing low-intent users through the funnel.

---

## 9. Conclusion

The hypothesis test provides **strong statistical evidence** (p=0.0017, χ²=9.88) that the Treatment campaign meaningfully improves paid conversion rate. Combined with the engagement score improvement and faster days-to-convert, the data supports proceeding to a launch decision — subject to resolution of the ARPCU and support ticket guardrail concerns documented in the recommendation memo.
