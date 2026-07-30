# Report Guide and Findings

## Page 1 - January Overview

Use this page to answer: How large is the January trip population, how many
rows are usable, and when do valid trips occur?

- Six KPI cards summarize volume, quality, and spend.
- The pickup-hour chart shows the daily operating pattern by hour.
- The date chart shows daily valid-trip volume across January.

## Page 2 - Zones & Operations

Use this page to answer: Which zones and payment/rate categories dominate the
validated trip population?

- Pickup and drop-off rankings are limited to the top 10 so the labels remain
  readable.
- The payment donut uses percentage labels for small categories.
- The rate-code chart retains `(Blank)` because missing classification is
  analytically relevant.

## Page 3 - Data Quality & Methodology

Use this page to answer: Can a reviewer verify how the numbers were produced?

- The donut shows the valid/excluded split.
- The reconciliation table exposes exact counts.
- The notes table documents scope, source, relationships, measures, and the
  February boundary treatment.

## Main findings

The January population contains 3.475 million raw rows. After the validity
rule, 3.251 million trips are valid (93.55%), while 224,106 rows (6.45%) are
excluded. Gross passenger spend is approximately $88M and average fare per
valid trip is $18.21. The most-used zones and hourly pattern are visible in the
operations page; this project intentionally avoids inferring causes from those
descriptive patterns.

