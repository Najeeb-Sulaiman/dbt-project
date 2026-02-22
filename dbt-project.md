# Building a Production-Grade Analytics Platform with dbt
## Project Overview

You have been hired as a Data Engineer at AtlasRide, a fast-growing UK mobility startup operating in 5 cities.

AtlasRide provides:
- Ride-hailing
- Airport transfers
- Scheduled corporate rides

The company recently migrated to a modern data stack and now needs a production-grade transformation layer using dbt.

Your task is to design and implement a scalable, well-tested, documented, and production-ready analytics platform using dbt.

## Technology Stack
You must use:
- dbt Core
- A cloud warehouse (BigQuery or Snowflake recommended)
- Git & GitHub for version control

## Provided Raw Data


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
