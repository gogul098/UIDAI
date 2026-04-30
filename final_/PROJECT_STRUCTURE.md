# Project Structure

```
final_codes/
│
├── dashboard.py                          # Main Streamlit application
│   ├── Page configuration & styling
│   ├── Data loading & feature engineering
│   ├── Sidebar controls & filters
│   ├── KPI metrics display
│   ├── Pareto analysis visualization
│   ├── Head-to-head state comparison
│   ├── Temporal & statistical analysis
│   ├── AI diagnostics & forecasting
│   └── Deep insights & optimization
│
├── unified_enrolment_data_final.csv     # Input dataset
│   └── Contains enrollment and biometric data across states
│
├── data cleaner and combiner.ipynb      # Data preprocessing notebook
│   └── Combines and cleans raw enrollment data
│
├── requirements.txt                      # Python dependencies
├── README.md                             # Project documentation
├── CONTRIBUTING.md                       # Contribution guidelines
├── CHANGELOG.md                          # Version history
├── LICENSE                               # MIT License
├── .gitignore                            # Git ignore rules
└── PROJECT_STRUCTURE.md                  # This file
```

## Key Components

### dashboard.py
Main application file containing:
- **Imports**: All required libraries (streamlit, pandas, plotly, sklearn, statsmodels)
- **Configuration**: Page layout, styling, metrics boxes
- **Data Loading**: CSV loading with data validation and feature engineering
- **Sidebar**: Interactive filters for date range and state selection
- **Sections 1-5**: Different analysis views with visualizations

### Data Files
- **unified_enrolment_data_final.csv**: Processed enrollment data with columns for dates, states, districts, pincodes, and demographic/biometric metrics

### Notebooks
- **data cleaner and combiner.ipynb**: Jupyter notebook for data preprocessing and transformation from raw sources

## Data Flow

```
Raw Data
   ↓
data cleaner and combiner.ipynb
   ↓
unified_enrolment_data_final.csv
   ↓
dashboard.py (load_data function)
   ↓
Feature Engineering (Calculations)
   ↓
Visualizations & Analysis
```

## Metrics Calculated

### Core Metrics
- **Total Enrolments**: Sum of age groups (0-5, 5-17, 18+)
- **Total Updates**: Biometric + Demographic updates
- **Biometric Updates**: Sum of age 5-17 and 17+ biometric updates
- **Demographic Updates**: Sum of age 5-17 and 17+ demographic updates

### Strategic Metrics
- **MBU_Gap_Index**: Compliance ratio for biometric updates
- **Migration_Intensity**: Population turnover indicator
- **Weighted_Effort**: Resource effort score
- **Efficiency_Gap**: Effort to result ratio
- **Urgency_Score**: Resource allocation priority

## Technology Stack

| Layer | Technology |
|-------|-----------|
| Web Framework | Streamlit |
| Data Processing | Pandas, NumPy |
| Visualization | Plotly |
| Machine Learning | Scikit-learn |
| Time Series | Statsmodels |
| Language | Python 3.8+ |

## Development Workflow

1. **Data Preparation**: Use Jupyter notebook to clean and combine data
2. **Feature Engineering**: Transformations in `load_data()` function
3. **Visualization**: Build charts using Plotly
4. **Deployment**: Run with Streamlit

## Version Control

```
main (production)
  ↑
feature branches
  ↑
development work
```

## File Conventions

- Python files: snake_case naming
- Variables: descriptive snake_case
- Functions: lowercase with underscores
- Constants: UPPERCASE
- Data files: descriptive names with timestamps if versioned
