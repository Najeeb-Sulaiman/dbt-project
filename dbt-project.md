# Building a Production-Grade Analytics Platform with dbt
## Project Overview
You have been hired as a Data Engineer at `BeejanRide`, a fast-growing UK mobility startup operating in 5 cities.

`BeejanRide` provides:
- Ride-hailing
- Airport transfers
- Scheduled corporate rides

The company recently migrated to a modern data stack and now needs a `production-grade` transformation layer using dbt.

Your task is to design and implement a scalable, well-tested, documented, and production-ready analytics platform using dbt.

## Business Objectives
Your models must support the following analytics use cases:
1. Daily revenue per city
2. Gross vs net revenue
3. Corporate vs personal revenue split
4. Top drivers by revenue
5. Driver activity monitoring
6. Rider lifetime value
7. Payment failure rate
8. Surge impact analysis
9. Driver churn tracking
10. Fraud detection insights

## Ingestion
All transactional data for BeejanRide is available in a postgres transactional database.

You must use `Airbyte` to ingest this source data from the transactional database to the data warehouse raw layer.

## Provided Raw Data
The connection credentials to the data source would be provided.

Below is the raw data ERD

![ER Diagram](dbt-project-erd.png)

Find below the data dictionary of the raw data:
### 1. trips_raw

| Column           | Description                     |
| ---------------- | ------------------------------- |
| trip_id          | Unique trip identifier          |
| rider_id         | Rider ID                        |
| driver_id        | Driver ID                       |
| vehicle_id       | Vehicle used                    |
| city_id          | City identifier                 |
| requested_at     | Time ride was requested         |
| pickup_at        | Pickup timestamp                |
| dropoff_at       | Dropoff timestamp               |
| status           | completed / cancelled / no_show |
| estimated_fare   | Initial fare estimate           |
| actual_fare      | Final fare                      |
| surge_multiplier | Surge applied                   |
| payment_method   | card / wallet / cash            |
| is_corporate     | Boolean                         |
| created_at       | Record creation timestamp       |
| updated_at       | Last update timestamp           |

### 2. drivers_raw

| Column          | Description                   |
| --------------- | ----------------------------- |
| driver_id       | Driver ID                     |
| onboarding_date | Driver join date              |
| driver_status   | active / suspended / inactive |
| city_id         | City                          |
| vehicle_id      | Current vehicle               |
| rating          | Average rating                |
| created_at      | Created timestamp             |
| updated_at      | Updated timestamp             |

### 3. riders_raw

| Column        | Description       |
| ------------- | ----------------- |
| rider_id      | Rider ID          |
| signup_date   | Signup date       |
| country       | Rider country     |
| referral_code | Referral used     |
| created_at    | Created timestamp |

### 4. payments_raw

| Column           | Description       |
| ---------------- | ----------------- |
| payment_id       | Payment ID        |
| trip_id          | Trip ID           |
| payment_status   | success / failed  |
| payment_provider | stripe / paypal   |
| amount           | Charged amount    |
| fee              | Processing fee    |
| currency         | Currency          |
| created_at       | Payment timestamp |

### 5. cities_raw

| Column      | Description      |
| ----------- | ---------------- |
| city_id     | City ID          |
| city_name   | City name        |
| country     | Country          |
| launch_date | City launch date |

### 6. driver_status_events_raw (High Volume Table)

| Column          | Description      |
| --------------- | ---------------- |
| event_id        | Event ID         |
| driver_id       | Driver ID        |
| status          | online / offline |
| event_timestamp | Event timestamp  |

**Note:** You must not modify raw tables.

## Technology Stack
You must use:
- Airbyte
- dbt Core
- A cloud warehouse (BigQuery or Snowflake recommended)
- Git & GitHub for version control

## Required Architecture
You must implement a layered modeling approach:
```bash
raw - staging - intermediate - marts
```

## Required Implementation

### 1. Staging Layer
Create staging models for each raw table.

The staging models must perform the following where neccessary:
- Rename columns to `snake_case`
- Cast correct data types
- Deduplicate using primary keys
- Standardize timestamps
- Remove invalid or null primary keys
- Source definitions must include:
    - descriptions
    - freshness checks
    - column tests

### 2. Intermediate Layer

Create reusable transformation logic.

Must include:

- trip_duration_minutes
- driver_lifetime_trips
- rider_lifetime_value
- corporate_trip_flag logic
- net_revenue calculation
- fraud indicators
- duplicate trip payments
- failed payment on completed trip
- extreme surge multiplier (>10)

You must:
- Use `ref()` properly
- Create at least one reusable macro

### 3. Marts Layer

You must implement a star schema that includes Fact and Dimension tables.

### 4. Snapshots
Implement SCD Type 2 snapshot for:
- drivers

Track:
- driver_status changes
- vehicle changes
- rating updates

### 5. Incremental Models
You must use Incremental materialization strategy where appropriate.

You must explain in your README:
- Why incremental is required
- Tradeoffs of full refresh vs incremental

### 6. Data Quality

You must implement:

**Generic Tests**
- not_null
- unique
- relationships
- accepted_values

**Custom Tests**
- No negative revenue
- Trip duration > 0
- Completed trip must have successful payment

**Freshness Tests**
- trips_raw must be < 2 hours old

### 7. Documentation & Governance

Your project must include:
- Model descriptions
- Column descriptions
- Business metric definitions
- Owner metadata
- Tags (finance, operations, fraud)

**You must generate:**
- dbt docs site
- Lineage graph

## Expected Outputs

Your final warehouse must support:
- Daily revenue dashboard
- City-level profitability
- Driver leaderboard
- Rider LTV analysis
- Payment reliability report
- Fraud monitoring view

## Required Deliverables

You must submit:
1. Public GitHub repository
2. Clear README including:
    - Architecture diagram
    - ERD
    - Data flow explanation
    - Design decisions
    - Tradeoffs
    - Future improvements
3. dbt lineage screenshot
4. Sample analytical queries demonstrating insights

## Duration
2 week (8/03/2026)