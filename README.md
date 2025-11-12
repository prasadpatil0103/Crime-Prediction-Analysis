# Crime Detection in Syracuse Using Machine Learning

## Overview
This project leverages machine learning to predict crime patterns in Syracuse, New York using historical crime data from 2023-2024 and socio-economic indicators. The system forecasts when and where crimes are likely to occur, helping law enforcement with proactive resource allocation and urban planning decisions.

## Key Features
- Monthly crime forecasting using SARIMA time series model
- Hourly crime trend analysis across 2023, 2024, and 2025
- Spatial crime risk classification using Random Forest
- Grid-based crime hotspot visualization
- Interactive risk maps showing low, medium, and high-risk zones
- Integration of unemployment data as socio-economic features

## Datasets
- **Crime Data:** Syracuse Open Data Portal (2023-2024)
  - Over 9,100 crime records with timestamps, offense types, and geolocation
- **Unemployment Data:** SYRA036URN (2023-2024)
  - Monthly unemployment rates for correlation analysis

## Technologies Used
- Python
- **Time Series:** SARIMAX
- **Classification:** Random Forest with SMOTE
- **Data Processing:** pandas, numpy
- **Visualization:** matplotlib, seaborn, folium
- **Geospatial Analysis:** Grid-based mapping (0.01° lat/long intervals)

## Model Performance

### SARIMA (Monthly Forecasting)
- **MAE:** 25.29 crimes
- **RMSE:** 30.83 crimes
- **MAPE:** 12.36%
- **R² Score:** 0.8574

### Random Forest (Spatial Classification)
- **Accuracy:** 88.6% (2025 predictions)
- **F1-Score (macro):** 0.84
- **2023→2024 Testing:** 77.2% accuracy

## Key Findings
- **Peak Crime Hours:** 12 PM to 8 PM, especially on weekends and Mondays
- **Most Common Crime:** Larceny, particularly in Fall and Summer
- **High-Risk Zones:** Identified specific grid cells with 400+ incidents
- **Seasonal Patterns:** Strong seasonal correlations captured by SARIMA model

## Installation
```bash
git clone https://github.com/yourusername/crime-prediction-syracuse.git
cd crime-prediction-syracuse
pip install -r requirements.txt
```

## Project Structure
```
├── data/                    # Crime and unemployment datasets
├── notebooks/               # Jupyter notebooks for analysis
├── models/                  # Trained SARIMA and Random Forest models
├── visualizations/          # Generated maps and charts
└── requirements.txt
```

## Visualizations
The project includes:
- Seasonal crime trend charts
- Hourly heatmaps by day of week
- Grid-based crime maps with hotspots
- Monthly prediction forecasts with confidence intervals
- 2025 predicted risk zone maps
- Comparative analysis charts (2023 vs 2024 vs 2025)

## Stakeholders
- **Law Enforcement:** Efficient patrol deployment and crime anticipation
- **City Planners:** Infrastructure and surveillance improvements
- **Residents & Businesses:** Enhanced neighborhood safety awareness

## Limitations
- Dataset limited to reported crimes only
- Features restricted to time, location, and unemployment rate
- Class imbalance affects rare crime type predictions
- Does not include weather, events, or demographic data

## Future Enhancements
- Integrate weather and event data
- Develop real-time prediction dashboard
- Implement deep learning models (LSTM)
- Add fairness-aware learning frameworks
- Include community feedback mechanisms

## License
MIT License

## Acknowledgments
- Syracuse Open Data Portal for crime datasets
- SYRA036URN for unemployment statistics
- IST 707 Applied Machine Learning course
