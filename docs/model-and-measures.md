# Model and Measures

## Tables

### Fact table

`Fact Trips - January Test` stores trip-level fields such as pickup date/hour,
pickup and drop-off location IDs, payment type, rate code, fare, tip, total
amount, trip distance, pickup/drop-off timestamps, trip duration, and
`Trip Validity`.

### Dimensions

- `Dim Date`: Date, Month Name, Month Number, Year
- `Dim Pickup Zone`: LocationID, Borough, Zone, service_zone
- `Dim Dropoff Zone`: LocationID, Borough, Zone, service_zone
- `Dim Payment Type`: Payment Type ID and readable Payment Type label
- `Dim Rate Code`: Rate Code ID and readable Rate Code label
- `KPI Measures`: centralized measure table

## Active relationships

All are one-to-many, single-direction relationships from dimension to fact:

| Dimension column | Fact column |
|---|---|
| `Dim Date[Date]` | `Fact Trips - January Test[Pickup Date]` |
| `Dim Pickup Zone[LocationID]` | `Fact Trips - January Test[PULocationID]` |
| `Dim Dropoff Zone[LocationID]` | `Fact Trips - January Test[DOLocationID]` |
| `Dim Payment Type[Payment Type ID]` | `Fact Trips - January Test[payment_type]` |
| `Dim Rate Code[Rate Code ID]` | `Fact Trips - January Test[RatecodeID]` |

## Measure definitions

The report uses measures rather than manually typed values. In plain language:

- **Raw Trip Rows:** count of rows in the January fact table.
- **Valid Trips:** count of rows whose `Trip Validity` is `Valid`.
- **Excluded Trips:** count of rows whose `Trip Validity` is `Excluded`.
- **Trip Validity Rate:** valid trips divided by raw trip rows.
- **Gross Passenger Spend:** sum of `total_amount` for valid trips.
- **Average Fare per Trip:** average `fare_amount` for valid trips.
- **Average Tip Percentage:** tip amount relative to fare for valid trips.
- **Average Trip Distance:** average `trip_distance` for valid trips.
- **Average Trip Duration:** average calculated trip duration for valid trips.

The exact measure names are visible in the `KPI Measures` table in the report.
The key design choice is that operational and financial measures use the
valid-trip population unless the visual is explicitly a raw/excluded audit.

