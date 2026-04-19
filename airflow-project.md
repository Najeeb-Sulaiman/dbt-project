# Orchestrating the BeejanRide Data Platform with Airflow
## Project Overview
You have already built the BeejanRide analytics platform using:
- Airbyte for ingestion
- dbt for transformation

BeejanRide now wants the platform to run automatically in production. Your next task is to extend the existing project by implementing orchestration with Apache Airflow.

Your Airflow implementation should orchestrate the complete ELT workflow without any manual intervention. Nothing should be triggered manually.

## Project Objective

Design and implement a production-grade orchestration layer for the BeejanRide platform using Airflow.
Your solution should demonstrate:
- Orchestration of Airbyte syncs
- Trigger dbt runs and tests
- Scheduling
- Task dependencies
- Failure handling
- Retries
- Monitoring
- Backfills
- Idempotency
- Clear separation between ingestion, transformation, testing, and alerting
- Any other best practices

## Required Deliverables
Submit the following:
1. Public GitHub repository (It can be the same repo as the dbt project)
2. Updated README explaining your orchestration design
3. Updated architecture diagram
4. Screenshots of DAGs in the Airflow UI
5. Example of a successful DAG run
6. Example of a failed DAG run and notification
7. Example of a backfill execution
8. Explanation of how idempotency is maintained
