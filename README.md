# Spotify Data Engineering Project

Azure based data pipeline for Spotify data. Current progress covers Azure Data Factory incremental ingestion into ADLS Gen2 Bronze. Databricks is next.

## What it does

1. Loops through a JSON config of tables
2. Checks CDC bookmark per table (`<table>_CDC.json`)
3. Runs incremental query with optional `from_date` override
4. Copies data from Azure SQL to ADLS Bronze as Parquet
5. Updates CDC bookmark with latest value
6. Sends email alert using Logic App
7. Dev to Main workflow with ADF publish

## Screenshots

ADF pipeline overview  
![ADF pipeline overview](screenshots/adf_pipeline_overview.png)

Incremental loop details  
![Incremental loop](screenshots/incremental_loop.png)

CDC bookmark file  
![CDC json](screenshots/cdc_json.png)

Logic App notification  
![Logic App](screenshots/logicapp.png)

Successful run output  
![Pipeline run](screenshots/pipeline_run.png)

## Status

ADF completed  
Next: Databricks transformations
