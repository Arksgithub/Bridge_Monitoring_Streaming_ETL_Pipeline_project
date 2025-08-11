# Bridge Monitoring Streaming Pipeline

A production-grade streaming ETL pipeline built with Databricks Delta Live Tables (DLT) that simulates IoT bridge sensors and processes real-time data through a medallion architecture.

## 🏗️ Architecture

**Bronze → Silver → Gold** medallion pattern with:
- 3 streaming data sources (temperature, vibration, tilt)
- Real-time data enrichment with static metadata
- 10-minute windowed aggregations
- Stream-stream joins for unified metrics

## 📁 Project Structure

```
├── queries.sql                   # Validation queries for DLT output
├── 00_data_generator.ipynb      # Synthetic sensor data generator
├── 01_bronze_processing.ipynb   # Raw data ingestion layer
├── 02_silver_processing.ipynb   # Data enrichment & quality checks
└── 03_gold_processing.ipynb     # Aggregations & stream joins
```

## 🚀 Quick Start

### Prerequisites
- Databricks workspace with Unity Catalog
- DLT-compatible runtime cluster

### Setup Unity Catalog Structure
```sql
CREATE CATALOG bridge_monitoring;
CREATE SCHEMA bridge_monitoring.00_landing;
CREATE SCHEMA bridge_monitoring.01_bronze;
CREATE SCHEMA bridge_monitoring.02_silver;
CREATE SCHEMA bridge_monitoring.03_gold;
CREATE VOLUME bridge_monitoring.00_landing.streaming;
```

### Run Pipeline
1. **Generate Data**: Run `00_data_generator.ipynb` to simulate sensor streams
2. **Bronze Layer**: Create DLT pipeline with `01_bronze_processing.ipynb`
3. **Silver Layer**: Add `02_silver_processing.ipynb` for data enrichment
4. **Gold Layer**: Add `03_gold_processing.ipynb` for final aggregations

## 💡 Key Features

- **Watermarked Streams**: 2-minute watermarks for late data handling
- **Data Quality**: Automated expectations and quality checks
- **Real-time Processing**: Sub-minute data processing latency
- **Scalable Architecture**: Handles increasing data volumes automatically

## 📊 Output

Final `bridge_metrics` table contains:
- 10-minute tumbling window aggregates
- Average temperature per bridge
- Maximum vibration and tilt measurements
- Bridge metadata enrichment

## 🛠️ Technologies

- Databricks Delta Live Tables
- Apache Spark Structured Streaming
- Unity Catalog
- Python/PySpark
