# Overview
Proyek ini mengintegrasikan data kualitas udara dan data meteorologi untuk:
- Mengumpulkan data PM2.5 dari OpenAQ
- Mengumpulkan data cuaca dan radiasi matahari dari Open-Meteo
- Melakukan simulasi performa panel surya
- Menyimpan hasil ke PostgreSQL
- Menyediakan dashboard analitik menggunakan Streamlit

# Architecture
<img width="325" height="800" alt="image" src="https://github.com/user-attachments/assets/0db60756-422b-4031-b05c-b54868b633e4" />

# ETL Flow
## 1. Extract
### Air Quality Data
Source:
- OpenAQ API v3
- CSV Fallback (`data_lengkap_bali_ubud.csv`)

Collected Parameters:
- PM1
- PM2.5
- Humidity
- Temperature
- UM003

### Weather Data
Source:
- Open-Meteo Archive API

Collected Parameters:
- Direct Normal Irradiance (DNI)
- Diffuse Radiation
- Shortwave Radiation
- Temperature
- Cloud Cover
- Humidity
- Precipitation

## 2. Transform & Simulate
### Data Processing
- Timestamp synchronization
- Timezone conversion
- Missing value handling
- Dataset merging
- Hourly resampling

### Missing Value Strategy
| Variable | Handling |
|-----------|-----------|
| PM2.5 | Fill with 0 |
| DNI | Fill with 0 |
| DHI | Fill with 0 |

### PV Simulation
Generated Features:
- Solar Position
- Angle of Incidence (AOI)
- POA Irradiance
- Cell Temperature
- Simulated Power Output

## 3. Load
Target Database:
```text
PostgreSQL
Database : pv_analysis_db
Table    : hourly_pv_data
```

Loading Method:
```python
df.to_sql(
    "hourly_pv_data",
    engine,
    if_exists="replace",
    index=False,
    method="multi"
)
```

## 4. Analyze
Dashboard Features:
- Time-series visualization
- PM2.5 vs DNI scatter plot
- Pearson correlation
- Linear regression
- Cloud cover filtering
- Daylight filtering

# Fault Tolerance
## OpenAQ API Failure Handling
When OpenAQ API returns:
```text
HTTP 410 Gone
```

Pipeline automatically switches to:
```text
data_lengkap_bali_ubud.csv
```

This ensures ETL execution continues without interruption.

# Database Schema
## hourly_pv_data
| Column | Type |
|----------|----------|
| timestamp | TIMESTAMP |
| pm25 | NUMERIC |
| direct_normal_irradiance | NUMERIC |
| cloud_cover | NUMERIC |
| temperature_2m | NUMERIC |
| poa_irradiance | NUMERIC |
| simulated_power_watt | NUMERIC |

# File Description
## pv_etl_pipeline.py
Main ETL orchestration script.
Responsibilities:
- Extract
- Transform
- Simulate
- Load

## openaqbali.py
OpenAQ ingestion module.

Features:
- Sensor pagination
- Timestamp conversion
- CSV fallback

## meteobali.py
Open-Meteo ingestion module.

Features:
- Historical weather retrieval
- Radiation dataset extraction
- Retry mechanism
- Request caching

## pv_simulation.py
PV performance simulation engine.

Calculates:
- Solar Position
- AOI
- POA Irradiance
- Cell Temperature
- Power Output

## dashboardbali_upgrade.py
Streamlit analytics dashboard.

Features:
- Interactive visualization
- Correlation analysis
- Linear regression
- Trend monitoring

# Technologies
| Component | Technology |
|------------|------------|
| Language | Python |
| ETL | Pandas |
| Numerical Computing | NumPy |
| Weather API | Open-Meteo |
| Air Quality API | OpenAQ |
| Database | PostgreSQL |
| ORM | SQLAlchemy |
| Driver | psycopg2 |
| Dashboard | Streamlit |
| Visualization | Plotly |

# Limitations
- OpenAQ API availability is unstable
- Single-location simulation only
- Hourly weather resolution
- Simplified isotropic irradiance model
- Does not implement Perez transposition model

# Future Improvements
- Apache Airflow orchestration
- Automated scheduling with Cron
- Multi-location analysis
- Advanced PV models
- Real-time streaming ingestion

# Authors
- Faris Arinanta 235150300111045
- Achmad Fiky Akbar 235150301111043
- Adhitya Noer Effendi 235150307111024
- Irham Dzaki Alfaruq 235150307111025
- Fadlan Umar Rozikin 235150307111032
- Ahmad Tsaqif 235150307111046

