# Data Quality and Methodology

## Validity treatment

The report does not silently discard questionable rows. It assigns each row a
`Trip Validity` value and exposes both populations:

- `Valid`: included in operational and financial measures.
- `Excluded`: retained for audit counts but excluded from valid-trip measures.

This makes the quality decision measurable and reversible.

## January boundary treatment

The raw source includes one February 1 boundary record. The report-wide filter
`Dim Date[Month Number] < 2` keeps the analysis within January 2025. The
boundary decision is documented on Page 3 rather than hidden in a visual.

## Reconciliation check

The most important validation is:

```text
Valid trips + Excluded trips = Raw trip rows
3,251,098 + 224,106 = 3,475,204
```

This check passes in the January report.

## Relationship checks

Each dimension filters the fact table in one direction. The report was checked
for active relationships and no visible relationship errors. Blank rate-code
values are intentionally retained as a meaningful source-quality signal.

## Interpretation limits

- The figures describe January 2025 only.
- Rounded cards are presentation values; the exact audit values are on Page 3.
- The report describes observed trip records, not total taxi demand or revenue
  for every NYC trip.
- No causal claims are made from the descriptive charts.

