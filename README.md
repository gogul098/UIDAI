# Aadhaar Insight AI

Aadhaar Insight AI is an interactive analytics and decision-support dashboard for exploring UIDAI Aadhaar enrolment, biometric-update, and demographic-update data across Indian states, districts, and PIN codes.

The project transforms large, raw UIDAI datasets into a cleaned, standardized dataset and presents operational insights through a Streamlit web application. It is designed to help analysts, administrators, and operations teams understand enrolment demand, identify unusual activity, monitor update patterns, and prioritize Aadhaar infrastructure and kit deployment.

## Project Goals

The dashboard focuses on answering practical operational questions:

- Which districts contribute most of the total enrolment volume?
- How do two states compare in enrolments, updates, child enrolment, migration, and effort?
- Which locations show low biometric-update compliance or high migration activity?
- Which PIN codes have unusual enrolment or update patterns?
- What enrolment demand can be expected during the next 30 days?
- Where should Aadhaar kits, operators, or update-only services be deployed first?

## Main Features

### 1. Interactive filtering

Users can filter the analysis by:

- Date range
- All Indian states or selected states
- Current record count within the selected scope

The dashboard recalculates its metrics and visualizations based on the active filters.

### 2. Key performance indicators

The dashboard displays high-level indicators for the selected data scope, including:

- Total enrolments
- Total biometric and demographic updates
- PIN codes with potential compliance risk
- Migration hotspots

### 3. Pareto analysis

The Pareto section ranks districts by total enrolment volume and displays the cumulative contribution of the leading districts. This applies the 80/20 principle to identify the “vital few” districts that account for a large share of enrolment activity.

### 4. State head-to-head comparison

Two selected states can be compared using an interactive radar chart. The comparison includes:

- Total enrolment volume
- Total updates
- Child enrolment
- Migration intensity
- Weighted operational effort

The dashboard normalizes the values for visual comparison while retaining the underlying metrics for analysis.

### 5. Temporal and statistical analysis

The application analyzes enrolment activity over time through:

- Day-of-week enrolment trends
- Correlation analysis between enrolments, updates, child enrolment, migration intensity, and biometric-update indicators

These views help identify recurring demand patterns and relationships between operational metrics.

### 6. Anomaly detection

The application uses **Isolation Forest** machine learning to flag unusual PIN-code-level activity. It analyzes aggregated enrolment, update, and biometric-update values after scaling the features with `StandardScaler`.

The anomaly scan uses a configurable contamination level of approximately 5% and displays normal and anomalous PIN codes in an interactive scatter plot.

### 7. Demand forecasting

The dashboard aggregates daily enrolments and uses **Holt-Winters Exponential Smoothing** with an additive trend to forecast demand for the next 30 days. The forecast helps estimate upcoming enrolment workload and expected operational load.

Forecasting requires sufficient historical data. If the selected filters do not contain enough usable history, the dashboard displays an insufficient-data warning.

### 8. Operator-efficiency analysis

The project creates a weighted effort score that gives different operational weights to:

- New enrolments
- Biometric updates
- Demographic updates

The resulting efficiency gap helps compare the amount of operational effort with the actual volume of enrolments and updates.

### 9. Migration dynamics

Migration intensity estimates population turnover using demographic updates among adults compared with new adult enrolments. Districts with high scores can indicate transit hubs or areas with significant address-update activity.

The dashboard highlights the highest-scoring districts and provides operational interpretations, such as prioritizing update-only kiosks in high-migration areas.

### 10. Resource allocation

The urgency score combines multiple signals:

- MBU gap index
- Total enrolment demand
- Children aged 0–5

Districts are ranked by urgency so teams can identify where Aadhaar kits or enrolment resources should be deployed first.

## Derived Metrics

The dashboard calculates the following metrics in `final_/dashboard.py`:

- **Biometric Updates:** `bio_age_5_17 + bio_age_17_`
- **Demographic Updates:** `demo_age_5_17 + demo_age_17_`
- **Total Updates:** biometric updates plus demographic updates
- **Total Enrolments:** `age_0_5 + age_5_17 + age_18_greater`
- **MBU Gap Index:** biometric updates for ages 5–17 divided by enrolments for ages 5–17
- **Migration Intensity:** adult demographic updates divided by adult enrolments plus one
- **Weighted Effort:** weighted combination of enrolments, biometric updates, and demographic updates
- **Efficiency Gap:** weighted effort divided by total activity
- **Urgency Score:** normalized combination of compliance, enrolment volume, and young-child enrolment indicators

## Data Preparation Pipeline

The notebook `final_/data cleaner and combiner.ipynb` prepares the source data before it is used by the dashboard. It demonstrates the following workflow:

1. Combine source CSV files containing enrolment data.
2. Select the required date, location, and age-group columns.
3. Load biometric, demographic, and enrolment datasets.
4. Normalize dates, state names, district names, and PIN-code types.
5. Standardize state names using text normalization and RapidFuzz matching.
6. Remove records that cannot be mapped to an official Indian state or union territory.
7. Merge the cleaned datasets using `date`, `state`, `district`, and `pincode`.
8. Fill missing metric values with zero.
9. Sort and export the unified dataset for dashboard analysis.

The notebook was designed for large datasets and includes examples of combining millions of records before analysis.

## Repository Structure

```text
UIDAI/
├── README.md                         # Project documentation
└── final_/
    ├── dashboard.py                  # Streamlit dashboard and analytics logic
    ├── data cleaner and combiner.ipynb# Data cleaning and dataset preparation
    ├── requirements.txt              # Python dependencies
    ├── README.md                     # Detailed application notes
    ├── UIDAI_REPORT.pdf              # Project report
    ├── UIDAI HACKATHON.pptx          # Project presentation
    ├── LICENSE                       # Project license
    └── .gitignore                    # Ignored files and datasets
```

Large CSV datasets may be excluded from version control. The dashboard therefore requires the cleaned dataset to be supplied locally before it can run.

## Technology Stack

- **Python 3.8+** — application and data-processing language
- **Streamlit 1.28.1** — interactive web dashboard
- **Pandas 2.0.3** — data loading, cleaning, grouping, and aggregation
- **NumPy 1.24.3** — numerical calculations and safe feature engineering
- **Plotly 5.17.0** — interactive charts and visualizations
- **Scikit-learn 1.3.0** — feature scaling and Isolation Forest anomaly detection
- **Statsmodels 0.14.0** — Holt-Winters time-series forecasting
- **Jupyter Notebook** — exploratory data preparation and transformation
- **RapidFuzz** — used in the notebook for state-name matching and normalization

## Installation

### Prerequisites

- Python 3.8 or newer
- `pip`
- A cleaned UIDAI enrolment dataset

### Setup

```bash
git clone https://github.com/gogul098/UIDAI.git
cd UIDAI

python -m venv venv
source venv/bin/activate          # Windows: venv\\Scripts\\activate

pip install -r final_/requirements.txt
```

If you want to run the data-cleaning notebook, install Jupyter and RapidFuzz as well:

```bash
pip install notebook rapidfuzz
jupyter notebook "final_/data cleaner and combiner.ipynb"
```

## Dataset Requirements

The dashboard expects a CSV containing the following fields:

| Column | Description |
|---|---|
| `date` | Enrolment or update date |
| `state` | State or union-territory name |
| `district` | District name |
| `pincode` | PIN code or service location identifier |
| `bio_age_5_17` | Biometric updates for people aged 5–17 |
| `bio_age_17_` | Biometric updates for people aged 17 and above |
| `demo_age_5_17` | Demographic updates for people aged 5–17 |
| `demo_age_17_` | Demographic updates for people aged 17 and above |
| `age_0_5` | Enrolments for children aged 0–5 |
| `age_5_17` | Enrolments for people aged 5–17 |
| `age_18_greater` | Enrolments for people aged 18 and above |

Place the cleaned file where the application expects it, or update the `file_path` value in `load_and_process_data()` inside `final_/dashboard.py`. The current dashboard code references `final_codes/unified_enrolment_data_final.csv`; because this repository uses the `final_` directory, update that path to the actual local dataset location before running if necessary.

## Running the Dashboard

From the repository root, run:

```bash
streamlit run final_/dashboard.py
```

Streamlit will provide a local URL, normally:

```text
http://localhost:8501
```

The dashboard opens with the date and state filters in the sidebar. Select a scope, review the KPI cards, and explore each analytical section. The anomaly scan runs when the user clicks **Run Anomaly Scan**.

## Performance Notes

- Streamlit data caching is used through `@st.cache_data`.
- Large datasets can require additional memory and processing time.
- Filtering the date range or reducing the number of selected states can improve responsiveness.
- Isolation Forest may take longer during its first execution.
- Forecasting works best when the selected data contains a continuous and sufficiently long daily history.

## Limitations and Future Enhancements

Potential improvements include:

- Exporting filtered reports to PDF or Excel
- Adding configurable metric weights and thresholds
- Adding state, district, and PIN-code drill-down pages
- Connecting to real-time UIDAI data sources
- Adding ARIMA, Prophet, or other advanced forecasting models
- Adding geographical heatmaps and map-based exploration
- Adding automated tests and a reproducible data-ingestion command
- Packaging the dashboard for cloud deployment

## License

This project is licensed under the MIT License. See `final_/LICENSE` for details.

## Acknowledgements

- UIDAI for the Aadhaar enrolment and update data
- The Streamlit community for the dashboard framework
- The open-source Python data-science ecosystem
