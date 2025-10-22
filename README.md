

```mermaid
flowchart TD
  A["Data Source - data.gov.in (aqi.csv)"] --> B["Data Ingestion"]
  B --> C["Raw Data Storage - CSV / Drive"]
  C --> D["Preprocessing"]
  D --> D1["Parse datetime - last_update"]
  D --> D2["Type conversion - pollutant_avg → numeric"]
  D --> D3["Missing value imputation - city/month mean, fallback overall mean"]
  D --> D4["Remove duplicates & invalid rows"]
  D --> E["Feature Engineering"]
  E --> E1["Create features: month, pollutant_city, pollutant_avg_filled"]
  E --> F["Analysis & Aggregation"]
  F --> F1["Q1 - Overall average AQI"]
  F --> F2["Q2 - City filter & profiles"]
  F --> F3["Q3 - Missing value report"]
  F --> F4["Q4 - Monthly city-wise aggregation"]
  F --> F5["Q5 - Pollutant-wise comparisons"]
  F --> G["Visualization"]
  G --> G1["Scatter plots, Bar charts, Line charts"]
  G --> G2["Publication-ready figures"]
  G --> H["Outputs"]
  H --> H1["Report - PDF / DOCX"]
  H --> H2["Notebook - .ipynb"]
  H --> H3["Dashboard - optional"]
  H --> H4["GitHub repo / Dataset links"]

```

Short explanation:

Data Source → ingest CSV → store raw file.

Preprocessing cleans and fills missing values (city-month mean fallback).

Feature Engineering creates month and pollutant_avg_filled.

Analysis answers Q1–Q5.

Visualization creates publication-ready figures.

Outputs are report, notebook, GitHub repo, and optional dashboard.

2) Logical Dataset Schema (ER-style) — Mermaid ER


```mermaid
erDiagram
    AQI_RECORDS {
        string country
        string state
        string city
        string station
        datetime last_update
        float latitude
        float longitude
        string pollutant_id
        float pollutant_min
        float pollutant_max
        float pollutant_avg
        float pollutant_avg_filled
        int month
    }
```

Notes:

pollutant_avg_filled is the cleaned column after imputation.

month is derived from last_update for grouping/aggregation.

3) Component Block Diagram (Plain text / ASCII)

```mermaid
+--------------------+     +-----------------------+     +---------------------+
|  Data Source:      | --> |  Raw Data Storage     | --> |  Preprocessing      |
|  data.gov.in (csv) |     |  (aqi.csv on Drive)   |     |  - parse dates      |
+--------------------+     +-----------------------+     |  - to_numeric       |
                                                         |  - impute missing   |
                                                         +---------------------+
                                                                |
                                                                v
                                                     +----------------------------+
                                                     | Feature Engineering:       |
                                                     | - month                    |
                                                     | - pollutant_avg_filled     |
                                                     | - pollutant_city label     |
                                                     +----------------------------+
                                                                |
                                                                v
                                                     +----------------------------+
                                                     | Analysis & Aggregation     |
                                                     | - Q1: overall avg AQI      |
                                                     | - Q2: city filters         |
                                                     | - Q3: missing value stats  |
                                                     | - Q4: monthly city grouping|
                                                     | - Q5: pollutant plots      |
                                                     +----------------------------+
                                                                |
                                                                v
                                                     +----------------------------+
                                                     | Visualization & Outputs    |
                                                     | - matplotlib / seaborn figs |
                                                     | - Notebook (.ipynb)        |
                                                     | - Final report (PDF)       |
                                                     | - GitHub repository        |
                                                     +----------------------------+
```
