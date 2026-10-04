# Aadhaar Insight AI

A Streamlit-based analytics dashboard for exploring UIDAI Aadhaar enrollment and update data across Indian states, districts, and PIN codes.

## Highlights

- Pareto analysis to identify high-volume districts
- State-to-state performance comparison with interactive radar charts
- Temporal trends and correlation analysis
- Isolation Forest anomaly detection for unusual enrollment patterns
- 30-day demand forecasting using Holt-Winters Exponential Smoothing
- Migration intensity and population-turnover insights
- Operator-efficiency metrics and urgency-based resource allocation

## Technology Stack

- Python 3.8+
- Streamlit
- Pandas and NumPy
- Plotly
- Scikit-learn
- Statsmodels
- Jupyter Notebook for data preparation

## Project Structure

```text
final_/
├── dashboard.py
├── data cleaner and combiner.ipynb
├── requirements.txt
├── README.md
├── UIDAI_REPORT.pdf
└── UIDAI HACKATHON.pptx
```

## Setup and Usage

```bash
git clone https://github.com/gogul098/UIDAI.git
cd UIDAI/final_
python -m venv venv
source venv/bin/activate      # Windows: venv\\Scripts\\activate
pip install -r requirements.txt
streamlit run dashboard.py
```

The dashboard expects a cleaned CSV dataset named `unified_enrolment_data_final.csv` in the location configured in `dashboard.py`. The input data should include date, state, district, pincode, enrollment, biometric-update, and demographic-update fields.

## Purpose

The project supports data-driven Aadhaar operations by helping teams identify enrollment trends, compliance risks, migration hotspots, anomalies, forecasted demand, and priority regions for resource deployment.

## License

This project is licensed under the MIT License. See the `final_/LICENSE` file for details.
