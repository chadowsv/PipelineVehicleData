# Azure-Based BI Pipeline for Vehicle Registration Analytics

A cloud-based Business Intelligence pipeline that integrates, cleans, and
analyzes Ecuadorian vehicle first-registration data (2017–2026) published by
the Servicio de Rentas Internas (SRI). Built on a Medallion architecture
(Bronze/Silver/Gold) over Azure Synapse Analytics and Azure Data Lake Storage
Gen2, with pandas for transformation and Apache Spark for partitioned Parquet
persistence, consumed through Power BI.

## Data source
Annual "Vehículos" CSV files published by SRI (public open data):
<SRI open-data portal URL>. The raw CSVs are public but large and are **not**
included in this repository; download them from the SRI portal and place them
in the Bronze layer before running.

## Repository contents
- `PipelineVehicleData.ipynb` — the full data engineering notebook.
- `tabla_homologacion.csv` — canton homologation reference table (222 cantons).

## Architecture
- **Bronze (raw):** original SRI CSV files + canton homologation table.
- **Silver (clean):** preprocessed, geographically enriched dataset, Parquet,
  partitioned by year (21-column schema).
- **Gold (curated):** analytical datasets (curated, demand, snapshot), Parquet
  (11-column schema). The demand dataset (first-registration events) feeds Power BI.

## How to run
The notebook runs on an Azure Synapse Analytics Spark pool.
Requirements: `pandas`, `pyspark`, `notebookutils`.
1. Upload the SRI CSVs and `tabla_homologacion.csv` to the Bronze container.
2. Run the notebook top to bottom; it writes the Silver and Gold layers.

## License
MIT
