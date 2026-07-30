# NYC Taxi Raw Model - January 2025

An end-to-end Power BI data-quality and operations analysis of NYC Yellow Taxi
trip records for **January 2025**. The project starts with raw monthly trip
data, builds a small star-schema model, applies an explicit January boundary
filter, and presents the results in a three-page report.

> **Scope note:** This is intentionally a January-only implementation. The
> future plan is to extend the same validated pattern to the remaining 2025
> months when capacity and time allow. No later-month results are claimed here.

## Why this project exists

Raw transportation data is useful only after it can be trusted. This project
was built to demonstrate that process clearly:

1. Start with official raw trip records rather than a pre-aggregated dataset.
2. Separate valid and excluded rows and reconcile the counts back to the raw total.
3. Add reusable dimensions for date, pickup zone, drop-off zone, payment type,
   and rate code.
4. Produce an executive-friendly report that explains both the findings and
   the data-quality decisions behind them.

The result is a portfolio project showing practical Power Query, data modeling,
DAX, validation, and dashboard-design skills.

## Deliverables

- [Power BI report PDF](artifacts/NYC%20Taxi%20Raw%20Test.pdf)
- [PowerPoint presentation (SharePoint link)](https://arizonastateu-my.sharepoint.com/:p:/g/personal/spabitwa_sundevils_asu_edu/IQAmjewK6ftXRoBg1DYv-YpfARJt2VfS_PyPVFOjSAb091w?e=DOMgNl)
- [Data sources and transformation notes](docs/data-sources-and-pipeline.md)
- [Model and DAX documentation](docs/model-and-measures.md)
- [Report page guide and findings](docs/report-guide.md)
- [Data-quality methodology](docs/data-quality-methodology.md)
- [Portfolio-ready project summary](docs/portfolio-summary.md)

The PowerPoint link is hosted in SharePoint and may require an ASU/Microsoft
account. The PDF is the portable artifact for viewers who cannot access the
Power BI service.

## Screenshots

These screenshots provide a quick visual walkthrough of the completed work:

| View | Screenshot |
|---|---|
| January Overview | [Open screenshot](screenshots/01-january-overview.png) |
| Zones & Operations | [Open screenshot](screenshots/02-zones-and-operations.png) |
| Data Quality & Methodology | [Open screenshot](screenshots/03-data-quality-methodology.png) |
| Semantic Model | [Open screenshot](screenshots/04-semantic-model.png) |
| Power Query Pipeline | [Open screenshot](screenshots/05-power-query-pipeline.png) |

The screenshots are presentation evidence only. The raw Parquet/CSV files and
storage credentials are intentionally not included in this repository.

## Data sources

The report uses the following source inputs configured in Power Query:

- Official NYC Taxi and Limousine Commission (TLC) Yellow Taxi monthly trip
  data: `yellow_tripdata_2025-01.parquet`.
- Official TLC taxi-zone lookup: `taxi_zone_lookup.csv`.
- Azure Blob Storage account/container used by the project: the
  `nyctaxisp2025` Blob account and `taxi-raw-2025` container.

The source data is public, but the raw files are intentionally not committed
to this repository because they are large and are not needed to review the
analysis. No storage keys, tokens, or private credentials belong in GitHub.

Official source reference: [NYC TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)

## What was built

### Data preparation and validation

- Loaded the monthly Parquet trip data and zone lookup through Power Query.
- Built a January fact table named `Fact Trips - January Test`.
- Added a `Trip Validity` classification so valid and excluded rows can be
  measured separately.
- Applied the report-wide filter `Dim Date[Month Number] < 2` to keep the report
  within January and exclude the single February 1 boundary row.
- Kept blank rate codes visible as a data-quality signal instead of silently
  deleting them.
- Reconciled valid plus excluded rows to the raw row count on the methodology
  page.

### Semantic model

The model uses a single-direction star-schema pattern:

```text
Dim Date          ─┐
Dim Pickup Zone    ├──> Fact Trips - January Test
Dim Dropoff Zone   ┤
Dim Payment Type   ┤
Dim Rate Code      ┘

KPI Measures (measure table; no relationship required)
```

The dimension side is `1` and the fact side is `many` for each active
relationship. This keeps filtering predictable and avoids bidirectional
ambiguity.

## Report pages

### 1. January Overview

Executive KPIs and time patterns:

- Raw Trip Rows
- Valid Trips
- Excluded Trips
- Trip Validity Rate
- Gross Passenger Spend
- Average Fare per Trip
- Valid Trips by Pickup Hour
- Valid Trips by Date

### 2. Zones & Operations

Operational breakdowns using the validated trip measure:

- Top 10 Pickup Zones by Valid Trips
- Top 10 Drop-off Zones by Valid Trips
- Valid Trips by Payment Type
- Valid Trips by Rate Code

The `(Blank)` rate-code category remains visible because it helps reviewers
understand the source-data quality rather than hiding missing classifications.

### 3. Data Quality & Methodology

The audit page makes the result defensible:

- Valid versus excluded trip-row donut
- Exact reconciliation table
- Methodology notes covering measures, relationships, scope, sources,
  boundary-row treatment, and validity definitions

## January results

The report's exact reconciliation is:

| Metric | January result |
|---|---:|
| Raw trip rows | 3,475,204 |
| Valid trips | 3,251,098 |
| Excluded trips | 224,106 |
| Validity rate | 93.55% |
| Excluded share | 6.45% |
| Gross passenger spend | approximately $88M |
| Average fare per trip | $18.21 |

The report cards intentionally abbreviate large values for readability (for
example, `3M` and `224K`); the exact values are shown on the reconciliation
page.

## Future roadmap

The next logical phase is to extend this validated January model to the other
2025 months:

1. Add the next monthly Parquet file through the same controlled Power Query
   pattern.
2. Re-run row-count, validity, date-boundary, and relationship checks.
3. Add a month field and a year-to-date comparison layer.
4. Reuse the existing dimensions and measures where their definitions remain
   valid.
5. Add month-over-month trends only after each month passes validation.

This roadmap is planned work, not part of the current January results.

## Reproducibility and sharing

The Power BI service report is the interactive source. The PDF and PowerPoint
are presentation artifacts. A normal PowerPoint export is static; a secure
Power BI embed requires viewer permissions. A public interactive link would
require the tenant administrator to enable Power BI **Publish to web**, which
also exposes the published model data. For a portfolio, the static artifacts
and transparent documentation are the safe default.

## Technologies

- Power BI Service
- Power Query (M)
- DAX measures and calculated tables
- Star-schema semantic modeling
- Azure Blob Storage source connection
- PowerPoint and PDF export
