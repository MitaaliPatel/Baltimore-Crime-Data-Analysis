# Baltimore Crime Data Analytics

An end-to-end data analytics pipeline built on Azure, analyzing arrest records and crime incidents across Baltimore City to identify trends, hotspots, and patterns that can inform law enforcement resource allocation and community policy.

---

## Overview

Baltimore's violent crime rate significantly exceeds the national average, with over 17,000 reported incidents annually. This project pulls live data from the Baltimore City open data API, processes it through an Azure-based ETL pipeline, stores it in a relational SQL database, and visualizes key findings in Power BI.

The goal was not just to describe crime — but to surface patterns useful to law enforcement, policymakers, and community organizations.

---

## Tech Stack

| Layer | Tool |
|---|---|
| Data Source | Baltimore City Open Data API (Data.gov) |
| Ingestion | Python, Azure Blob Storage |
| ETL | Azure Data Factory v2 |
| Database | Azure SQL Database |
| Visualization | Power BI |
| Development | Google Colab, Python (pandas, requests) |

---

## Pipeline Architecture

1. **Data Retrieval** — Pulls live arrest, incident, police station, and location data from the Baltimore City API using authenticated requests
2. **Ingestion** — Python script cleans and uploads flat files to Azure Blob Storage automatically
3. **ETL** — Azure Data Factory pipeline extracts from Blob Storage, transforms, and loads into Azure SQL Database with automated refresh
4. **Database** — Four relational tables (Arrest, Incident, Location, PoliceStation) with foreign key relationships
5. **Visualization** — Power BI connected directly to Azure SQL for real-time interactive dashboards

---

## Dataset

Four datasets from [data.baltimorecity.gov](https://data.baltimorecity.gov):

- **Arrests** — arrest records including date, charge, location, and demographics (age, gender, race)
- **Incidents** — crime incident records by type, district, neighborhood, and coordinates
- **Police Stations** — station locations, neighborhoods, commanders, and contact details
- **Locations** — granular address and coordinate data linked to arrests and incidents

---

## Key Findings

**Teenager arrests (age 13-19, 2010-2024)**
- 27,750 total arrests
- Top offenses: narcotics (43%), assault (6.6%), armed person (4.3%)
- 88% male, 12% female

**Young adult arrests (age 20-30, 2023)**
- 5,006 arrests
- Top offenses: common assault (21.7%), assault with cutting instrument (17.3%), murder (13%)
- Significant shift from drug offenses to violent crime compared to the teenager group

**Geographic patterns**
- Crime hotspots cluster in specific neighborhoods with lower police station density
- Geospatial mapping highlights resource allocation gaps between high-crime areas and station coverage

---

## Database Schema

Four relational tables:

- `arrest` — ArrestNumber (PK), Age, Gender, Race, ArrestDateTime, Charge, ChargeDescription
- `incident` — IncidentNumber (PK), IncidentOffence, IncidentLocation, ArrestNumber (FK)
- `location` — LocationAddr, ArrestNumber (FK), Latitude, Longitude, District
- `police_station` — GIS_ID (PK), Address, Neighborhood, Commander, X_Coord, Y_Coord

---

## Project Limitations

- API data quality depends on Baltimore City's update cadence — schema changes in the source can break the pipeline
- Demographic patterns in arrest data reflect policing practices, not necessarily crime distribution — findings should be interpreted with that context in mind

---

## Running the Notebook

1. Replace the API key placeholder with your own Baltimore City Open Data API key
2. Set up an Azure Storage account and update the connection string in your environment (use environment variables, never hardcode credentials)
3. Configure Azure Data Factory with your Blob Storage and SQL Database endpoints
4. Connect Power BI to your Azure SQL Database instance
