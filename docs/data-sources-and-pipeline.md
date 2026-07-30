# Data Sources and Pipeline

## Source files

### Yellow Taxi trips

- File: `yellow_tripdata_2025-01.parquet`
- Grain: one raw taxi trip record
- Period used: January 2025, with one February 1 boundary row present in the
  source and excluded from the January report scope
- Storage: Azure Blob Storage, `nyctaxisp2025` account / `taxi-raw-2025`

### Taxi zones

- File: `taxi_zone_lookup.csv`
- Grain: one row per taxi location identifier
- Role: translates pickup and drop-off location IDs into borough, zone, and
  service-zone labels

Official source reference: [NYC TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)

## Pipeline implemented

1. Connect to the Azure Blob Storage account through Power Query.
2. Select the January Parquet trip file and the taxi-zone lookup CSV.
3. Load the trip data into the January fact table.
4. Load the taxi-zone lookup into reusable pickup and drop-off dimensions.
5. Create a date dimension from the fact pickup-date range.
6. Create payment-type and rate-code dimensions from the fact keys.
7. Create validity-aware measures and preserve blank rate codes.
8. Apply the report-wide January filter (`Month Number < 2`).
9. Validate totals through the reconciliation table.
10. Build report pages only after the model returned stable values.

## Why raw files are not committed

The trip file contains millions of rows and is unnecessary for reviewing the
project. Keeping it out of GitHub makes the repository smaller and avoids
accidentally publishing credentials or an uncontrolled copy of source data.

