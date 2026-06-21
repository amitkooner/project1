# NFL Play-by-Play Data Pipeline

An end-to-end batch data pipeline that ingests, transforms, and visualizes NFL
play-by-play data from the 2013 season using a modern data stack on Google Cloud.

> Built as the capstone project for the [DataTalks.Club Data Engineering Zoomcamp](https://github.com/DataTalksClub/data-engineering-zoomcamp).

## Architecture

| Layer | Tool | Role |
|-------|------|------|
| Infrastructure | **Terraform** | Provisions and manages GCP resources declaratively |
| Orchestration | **Airflow** | Ingests raw data to Google Cloud Storage, then loads it into BigQuery |
| Transformation | **dbt** | Models and transforms the raw data in BigQuery for analysis |
| Warehouse | **BigQuery** | Stores raw and transformed datasets |
| Visualization | **Looker Studio** | Dashboards the transformed play-by-play data |

## How it works

1. **Infrastructure** is defined in the `.tf` files and applied with Terraform to stand up the GCS bucket and BigQuery datasets.
2. **Airflow** (`nfl_data_pipeline.py`) orchestrates ingestion: raw data lands in a GCS bucket and is loaded into BigQuery.
3. **dbt** transforms the data — see `models/summarize_play_by_game.sql` — with the warehouse connection configured in `profiles.yml`.
4. **Looker Studio** visualizes the result. [View the dashboard »](https://lookerstudio.google.com/reporting/55388976-42bb-470c-bbbf-347ee5d5ce23)

## Repository layout

- `*.tf` — Terraform infrastructure definitions
- `nfl_data_pipeline.py` — Airflow DAG for ingestion and loading
- `models/` — dbt models (including `summarize_play_by_game.sql`)
- `profiles.yml` — dbt warehouse connection profile

## Setup

1. Set up a GCP project and authenticate locally.
2. Configure and apply the Terraform files to provision infrastructure.
3. Deploy the Airflow DAG and trigger the pipeline.
4. Run the dbt models to build the transformed tables.
5. Connect Looker Studio to BigQuery to explore the dashboard.

## Author

Amit Kooner

## License

Released under the [MIT License](LICENSE).
