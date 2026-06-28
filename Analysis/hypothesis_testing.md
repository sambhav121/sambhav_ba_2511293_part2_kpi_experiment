# Hypothesis Testing

## Primary Test

The primary outcome is `converted_to_paid`, a binary variable measured independently for Control and Treatment users. A two-proportion z-test was selected because the task is to compare two independent conversion rates with large sample sizes.

## Guardrail Tests

Binary guardrails use two-proportion z-tests. Continuous outcomes (`revenue_30d`, `support_tickets_30d`, `engagement_score`, and converter-only `days_to_convert`) use Welch two-sample t-tests because group variances may differ.

## Group Summary

| experiment_group | users | landing_page_rate | trial_start_rate | onboarding_completion_rate | paid_conversion_rate | revenue_30d_mean | revenue_30d_total | support_tickets_mean | refund_rate | engagement_score_mean |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Control | 693 | 0.6364 | 0.2511 | 0.1558 | 0.0317 | 51.7493 | 35862.2800 | 0.2193 | 0.0000 | 57.0262 |
| Treatment | 715 | 0.7259 | 0.2909 | 0.2126 | 0.0699 | 53.8751 | 38520.7100 | 0.3720 | 0.0042 | 62.9320 |

## Test Results

| metric | test | control_n | treatment_n | control_value | treatment_value | difference | relative_lift | test_statistic | p_value | ci_low | ci_high |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| visited_landing_page | Two-proportion z-test | 693.0000 | 715.0000 | 0.6364 | 0.7259 | 0.0895 | 14.07% | 3.6051 | <0.001 | 0.0410 | 0.1380 |
| started_trial | Two-proportion z-test | 693.0000 | 715.0000 | 0.2511 | 0.2909 | 0.0398 | 15.86% | 1.6803 | 0.0929 | -0.0065 | 0.0862 |
| completed_onboarding | Two-proportion z-test | 693.0000 | 715.0000 | 0.1558 | 0.2126 | 0.0567 | 36.41% | 2.7433 | 0.0061 | 0.0164 | 0.0971 |
| converted_to_paid | Two-proportion z-test | 693.0000 | 715.0000 | 0.0317 | 0.0699 | 0.0382 | 120.28% | 3.2519 | 0.0011 | 0.0154 | 0.0610 |
| refund_requested | Two-proportion z-test | 693.0000 | 715.0000 | 0.0000 | 0.0042 | 0.0042 |  | 1.7070 | 0.0878 | -0.0005 | 0.0089 |
| revenue_30d | Welch two-sample t-test | 693.0000 | 715.0000 | 51.7493 | 53.8751 | 2.1258 | 4.11% | 0.1051 | 0.9163 |  |  |
| support_tickets_30d | Welch two-sample t-test | 693.0000 | 715.0000 | 0.2193 | 0.3720 | 0.1527 | 69.62% | 4.2287 | <0.001 |  |  |
| engagement_score | Welch two-sample t-test | 687.0000 | 707.0000 | 57.0262 | 62.9320 | 5.9058 | 10.36% | 7.9454 | <0.001 |  |  |
| days_to_convert (converted_to_paid == 1) | Welch two-sample t-test | 22.0000 | 50.0000 | 8.8636 | 6.4000 | -2.4636 | -27.79% | -2.8004 | 0.0083 |  |  |

## Segment Conversion Tests

| dimension | segment | control_n | treatment_n | control_conversion | treatment_conversion | difference | relative_lift | p_value |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| plan_type | Free | 361.0000 | 368.0000 | 3.05% | 9.24% | 6.19% | 203.21% | <0.001 |
| device_type | Mobile | 428.0000 | 436.0000 | 2.57% | 7.34% | 4.77% | 185.57% | 0.0013 |
| traffic_source | Organic | 246.0000 | 241.0000 | 2.03% | 6.22% | 4.19% | 206.22% | 0.0198 |
| traffic_source | Paid Search | 156.0000 | 176.0000 | 1.28% | 6.25% | 4.97% | 387.50% | 0.0199 |
| region | North | 203.0000 | 180.0000 | 3.45% | 8.89% | 5.44% | 157.78% | 0.0253 |
| traffic_source | Referral | 81.0000 | 91.0000 | 2.47% | 10.99% | 8.52% | 345.05% | 0.0286 |
| region | South | 184.0000 | 184.0000 | 3.26% | 7.61% | 4.35% | 133.33% | 0.0658 |
| region | East | 158.0000 | 172.0000 | 2.53% | 6.40% | 3.86% | 152.62% | 0.0923 |
| device_type | Tablet | 56.0000 | 56.0000 | 1.79% | 7.14% | 5.36% | 300.00% | 0.1699 |
| plan_type | Premium | 109.0000 | 112.0000 | 2.75% | 6.25% | 3.50% | 127.08% | 0.2110 |
| traffic_source | Email | 74.0000 | 56.0000 | 2.70% | 7.14% | 4.44% | 164.29% | 0.2322 |
| device_type | Desktop | 200.0000 | 214.0000 | 4.50% | 6.54% | 2.04% | 45.38% | 0.3647 |
| region | West | 148.0000 | 179.0000 | 3.38% | 5.03% | 1.65% | 48.83% | 0.4633 |
| traffic_source | Social | 130.0000 | 133.0000 | 7.69% | 6.02% | -1.68% | -21.80% | 0.5902 |
| plan_type | Basic | 223.0000 | 235.0000 | 3.59% | 3.83% | 0.24% | 6.76% | 0.8909 |

## Decision

Launch the treatment. Paid conversion differs by 3.82% with p-value 0.0011. Mean revenue difference is 2.13 with p-value 0.9163; support-ticket difference is 0.1527 with p-value <0.001; refund-rate difference is 0.42% with p-value 0.0878.

## Missing Data

| field | missing_rows |
| --- | --- |
| device_type | 18 |
| traffic_source | 24 |
| days_to_convert | 1336 |
| engagement_score | 14 |

## Limitation

Segment-level results are exploratory and were not adjusted for multiple comparisons. They should guide follow-up targeting or test design, not serve as the only launch basis.
