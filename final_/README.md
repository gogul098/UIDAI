# Aadhaar Insight AI

An intelligent analytics dashboard for monitoring and analyzing Aadhaar enrollment data with predictive insights and anomaly detection.

## Overview

Aadhaar Insight AI is a Streamlit-based web application designed to provide comprehensive analysis of Aadhaar enrollment patterns across regions. The dashboard offers strategic insights including Pareto analysis, head-to-head state comparisons, temporal analysis, and AI-powered diagnostics.

## Features

- **Pareto Analysis**: Identify the "vital few" districts driving majority of enrolments (80/20 rule)
- **Head-to-Head Comparison**: Compare performance metrics between two states with radar charts
- **Temporal & Statistical Analysis**: Analyze enrollment patterns by day of week and correlation metrics
- **Anomaly Detection**: Identify unusual enrollment patterns using machine learning
- **Demand Forecasting**: 30-day enrollment demand predictions using exponential smoothing
- **Operator Efficiency Analysis**: Assess resource utilization and operational efficiency
- **Migration Dynamics**: Track population movement patterns and address updates
- **Resource Allocation**: Urgency scoring for optimal kit deployment

## Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Setup

1. Clone the repository
```bash
git clone <repository-url>
cd final_codes
```

2. Create a virtual environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies
```bash
pip install -r requirements.txt
```

4. Place your data file
- Ensure `unified_enrolment_data_final.csv` is in the same directory as `dashboard.py`

## Usage

Run the Streamlit application:
```bash
streamlit run dashboard.py
```

The dashboard will open in your default browser at `http://localhost:8501`

### Data Requirements

The application expects a CSV file with the following columns:
- `date`: Enrollment date
- `state`: State identifier
- `district`: District identifier
- `pincode`: PIN code
- `bio_age_5_17`: Biometric updates (age 5-17)
- `bio_age_17_`: Biometric updates (age 17+)
- `demo_age_5_17`: Demographic updates (age 5-17)
- `demo_age_17_`: Demographic updates (age 17+)
- `age_0_5`: Enrollments (age 0-5)
- `age_5_17`: Enrollments (age 5-17)
- `age_18_greater`: Enrollments (age 18+)

## Dashboard Sections

### 1. Pareto Analysis
Displays top 30 districts by enrollment volume with cumulative percentage distribution to identify key contributors.

### 2. Head-to-Head Comparison
Compare two selected states across multiple metrics:
- Volume (Total Enrolments)
- Updates (Total Updates)
- Child Enrolment
- Migration Score
- Efficiency

### 3. Temporal & Statistical Analysis
- Day of Week analysis showing enrollment patterns
- Correlation matrix of key metrics

### 4. AI Diagnostics & Forecasting
- Anomaly detection identifying unusual enrollment patterns
- 30-day demand forecasting with exponential smoothing

### 5. Deep Insights & Optimization
- Operator Efficiency Analysis
- Migration Dynamics (Churn Map)
- Resource Allocation with Urgency Scoring

## Key Metrics

- **MBU_Gap_Index**: Compliance ratio (Biometric Updates / Child Enrolments)
- **Migration_Intensity**: Population turnover (Address Updates / New Adult Enrolments)
- **Weighted_Effort**: Resource effort score combining volume, biometric, and demographic updates
- **Efficiency_Gap**: Ratio of effort to actual enrollments/updates
- **Urgency_Score**: Composite score for resource allocation prioritization

## Technologies Used

- **Streamlit**: Web application framework
- **Pandas**: Data manipulation and analysis
- **Plotly**: Interactive visualizations
- **Scikit-learn**: Machine learning (Isolation Forest for anomaly detection)
- **Statsmodels**: Time series forecasting (Exponential Smoothing)
- **NumPy**: Numerical computations

## File Structure

```
final_codes/
├── dashboard.py                          # Main Streamlit application
├── unified_enrolment_data_final.csv     # Input data file
├── data cleaner and combiner.ipynb      # Data preprocessing notebook
├── requirements.txt                      # Python dependencies
├── README.md                             # This file
├── LICENSE                               # License file
└── .gitignore                            # Git ignore rules
```

## Configuration

### Sidebar Controls
- **Date Range**: Filter data by start and end dates
- **State Selection**: Choose specific states or select all
- **Real-time Record Count**: View total records in current selection

### Anomaly Detection Parameters
- Contamination rate: 5% (adjustable in code)
- Algorithm: Isolation Forest

### Forecasting Parameters
- Forecast horizon: 30 days
- Method: Exponential Smoothing (additive trend)

## Performance Notes

- Data is cached using Streamlit's `@st.cache_data` decorator for optimal performance
- Large datasets may require filtering by date range
- Anomaly detection may take 2-3 seconds on first run

## Troubleshooting

### File Not Found Error
Ensure `unified_enrolment_data_final.csv` is in the same directory as `dashboard.py`

### Insufficient Data Warning
This appears when there's not enough historical data for forecasting. Ensure you have at least 7 days of data.

### Performance Issues
- Filter by date range to reduce data volume
- Reduce number of selected states
- Restart the Streamlit application

## Future Enhancements

- Export reports to PDF/Excel
- Custom metric configuration
- Multi-level drill-down analysis
- Real-time data integration
- Advanced forecasting models (ARIMA, Prophet)
- Regional heatmaps

## Contributing

Contributions are welcome! Please follow these steps:
1. Create a feature branch
2. Make your changes
3. Test thoroughly
4. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contact

For questions or support, please contact the project maintainers.

## Acknowledgments

- UIDAI for Aadhaar enrollment data
- Streamlit community for the excellent framework
- Open-source contributors
