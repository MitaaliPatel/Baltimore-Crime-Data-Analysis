# Baltimore Crime Data Ingestion Pipeline

A Python-based data ingestion pipeline that pulls live crime and arrest data from the Baltimore City open data API and loads it into Azure Blob Storage for downstream processing.

---

## What This Does

Baltimore City publishes arrest records, crime incidents, and police station data through a public API. This pipeline authenticates with that API, retrieves the relevant datasets, applies cleaning and filtering logic, and uploads the processed files to Azure Blob Storage — ready for ETL and analysis.

---

## Tech Stack

- Python (pandas, requests, azure-storage-blob)
- Baltimore City Open Data API
- Azure Blob Storage

---

## Pipeline Steps

1. Authenticates with the Baltimore City open data API using an API key
2. Retrieves two datasets: BPD Arrest records and Police Station locations
3. Filters and cleans each dataset — selects relevant columns, removes nulls, deduplicates on ArrestNumber
4. Exports cleaned data as CSV files
5. Uploads to Azure Blob Storage container for downstream use

---

## Datasets

Both pulled live from [data.baltimorecity.gov](https://data.baltimorecity.gov):

- **BPD Arrests** — arrest records including date, charge, location, age, gender, race, district, and neighborhood
- **Police Stations** — station names, addresses, neighborhoods, commanders, and geographic coordinates

---

## Running It

1. Get a free API key from [data.baltimorecity.gov](https://data.baltimorecity.gov)
2. Set up an Azure Storage account
3. Store your credentials as environment variables — never hardcode them:

```python
import os
connection_string = os.environ.get('AZURE_STORAGE_CONNECTION_STRING')
api_key = os.environ.get('BALTIMORE_API_KEY')
```

4. Run the notebook end to end — the cleaned CSVs will land in your specified Blob Storage container

---

## Notes

This pipeline was built as the ingestion layer for a larger group project that included an Azure Data Factory ETL pipeline, Azure SQL Database, and Power BI dashboards for crime trend analysis across Baltimore neighborhoods.
