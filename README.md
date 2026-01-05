# Spotify Data Engineering Project (Azure)

This repo contains a Spotify data pipeline built on Azure. Current milestone completes the Azure Data Factory incremental ingestion into ADLS Gen2 Bronze. Databricks transformations will be added next.

## What is built so far

1. Parent ADF pipeline loops over a JSON config of tables (schema, table, cdc_col, from_date)
2. For each table, ADF checks if a bookmark file exists in Bronze: `<table>_CDC.json`
3. If bookmark exists, ADF reads the last CDC value, else uses a default start date
4. ADF runs an incremental query with optional override using from_date
5. ADF copies data from Azure SQL to ADLS Bronze as Parquet with a timestamped filename
6. ADF updates the bookmark by writing the latest max CDC value
7. ADF triggers a Logic App notification on successful completion
8. Code is version controlled in GitHub using dev to main pull requests and ADF publish

## Incremental logic

Filter used in source query

`WHERE cdc_col > @{if(empty(item().from_date), variables('last_cdc_value'), item().from_date)}`

## ADF screenshots

Pipeline overview

![ADF pipeline overview](screenshots/adf_pipeline_overview.png)

Web activity calling Logic App

![ADF alerts](screenshots/adf_alerts_web_activity.png)

Dynamic query with CDC

![ADF dynamic query](screenshots/adf_dynamic_query.png)

## Status

ADF completed  
Next: Databricks bronze to silver to gold
