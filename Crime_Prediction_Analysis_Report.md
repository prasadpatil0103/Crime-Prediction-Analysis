# IST 707.M001.SP25 Applied Machine Learning  
## **Crime Detection in Syracuse Using Machine Learning**

---

### **Team DPD**
- **Darsh Yogesh Thakor [darsh059]**  
- **Dream Jitendrakumar Patel [dreamp117]**  
- **Prasad Pramod Patil [prasadpatil0103]**

---

## **Introduction**

Crime prediction has become a critical focus of urban analytics, especially in cities where law enforcement and resource allocation face mounting pressure to be both proactive and data-driven. This project leverages real-world crime data and socio-economic indicators to create a machine learning–powered system that analyzes historical crime patterns and forecasts future crime distribution across time and geography.

Our primary objective is to predict when and where crimes are likely to occur in Syracuse, New York, using machine learning models that incorporate both time series forecasting and spatial classification. The analysis spans data from 2023 and 2024, integrating seasonal crime trends and unemployment rates to understand deeper correlations between socio-economic conditions and criminal activity.

We apply **SARIMA** and **Random Forest** models to forecast monthly and hourly crime frequencies and to spatially categorize the city into grid cells with low, medium, or high crime risks. Visual outputs—including interactive heatmaps and folium-based risk grids—support our analytical outcomes and serve as decision-making tools for law enforcement and public safety stakeholders.

This technical solution demonstrates how machine learning can support smart policing strategies, enhance public safety efforts, and guide urban planning in mid-sized American cities like Syracuse.

---

## **Literature Review**

Crime prediction has garnered substantial academic interest over the past decade, with research spanning spatial analysis, temporal forecasting, and socio-economic correlations. Previous studies underscore the critical value of integrating public datasets to model crime incidence and to inform law enforcement strategies.



### **Stakeholder Needs**

- **Law Enforcement:** Need to deploy patrol units efficiently and anticipate high-crime zones.  
- **City Planners:** Require insights to improve surveillance infrastructure and urban design.  
- **Residents & Businesses:** Desire safer neighborhoods and commercial zones to live and operate.



### **Justification for Chosen Methods**

The use of **SARIMA** and **Random Forest** models was informed by both the nature of the data and existing research precedents:

- **SARIMA** has been proven effective in time series forecasting for seasonal datasets like crime logs, with successful applications in predicting monthly burglary or assault patterns.
- **Random Forest** is widely used in classification tasks and has demonstrated high accuracy and robustness in crime type prediction, especially when data includes categorical variables like time, day, and spatial zone.



### **Solution Overview**

We built machine learning models using Syracuse’s publicly available crime and unemployment datasets for 2023 and 2024 to:

- Analyze hourly and seasonal crime trends.  
- Map crime incidents using grid-based geospatial visualization.  
- Predict crime hotspots for 2025 both hourly and monthly.  
- Visualize risk levels across the city using an interactive map.

While crime cannot be predicted with absolute certainty, our model serves as a prototype to identify high-risk zones and time periods, enabling proactive measures. This project represents a critical step toward data-informed policing and safer community planning. Future iterations can improve accuracy and integrate additional data like weather, events, or demographic shifts.

---

## **Data and Methods**

### **Data**

We utilized publicly available crime datasets from the Syracuse Open Data Portal and unemployment data from SYRA036URN sources for the years 2023 and 2024.

**Source Files and Description:**

- `Crime_Data_2023_Offenses_(With_Lat_&_Long_Info).csv`  
- `Crime_Data_2024_Offenses_With_Lat_and_Long_Info.csv`  
    - Contain timestamped crime records including offense type, latitude, longitude, and location.

- `SYRA036URN_2023.csv` & `SYRA036URN_2024.csv`  
    - Provide monthly unemployment rates used as socio-economic features.

- `crime_df_23_un.csv`, `crime_df_24.csv`, `crime_df_2324_un.csv`  
    - Preprocessed and merged datasets used in modeling and hourly analysis.

- `hourly_crime_comparison_actual_2023_2024_predicted_2025.csv`  
    - Contains final hourly predictions for 2025.

**Final Dataset Statistics:**

- **Total Records:** Over 9,100 unique rows after merging (2023 + 2024).  
- **Features:** `DATEEND`, `HOUR`, `OFFENSE`, `Latitude`, `Longitude`, `Grid_ID`, `Unemployment_Rate`, derived `Month`, `Year`, `Day`, and `Crime Frequency`.  
- **Balance:** Crime types were moderately imbalanced; SMOTE was applied during classification modeling to address this.

**Cleaning and Processing Steps:**

- Converted and aligned all `DATEEND` formats.  
- Extracted `year`, `month`, `hour`, and `day_of_week` for trend analysis.  
- Generated `Grid_ID` based on 0.01 latitude/longitude intervals.  
- Merged unemployment data by month-year keys.  
- Removed rows with missing coordinates or null values.

---

## **Visual Analysis**

To understand temporal and spatial crime behavior:

###  **Seasonal Trend Charts**

![Crime Type Trends by Season](Crime_Type_Trends_by_Season.png)

This chart presents seasonal crime variations by type, highlighting that **Larceny** is consistently the most reported offense, especially during Fall and Summer seasons.

---

### **Hourly Heatmaps**

![Hourly Crime Distribution](Heatmap_23.png)

The heatmap shows hourly crime patterns by day of the week, where **afternoon to evening hours (12 PM to 8 PM)** experience the highest crime rates, particularly on weekends and Mondays.

---

### 2023–2024 Crime Type and Counts

![Grid-Based Crime Map with Top Crime Types](grid_23.png)

This map visualizes Syracuse divided into grid cells, showing the top crime type and count per cell. The red zone above indicates a hotspot where **Larceny** is predominant with over 400 incidents.

---

### Monthly Crime Prediction (SARIMA)

![Monthly Crime Count Prediction for 2024](Trend_24.png)

This SARIMA forecast shows predicted crime counts for 2024 alongside actual 2023 values. The shaded region indicates confidence intervals around the forecast.

---

### Actual vs Predicted Crimes per Hour (2024)

![Actual vs Predicted Crimes per Hour - 2024](A_P.png)

This chart evaluates hourly prediction accuracy by comparing actual and SARIMA-forecasted hourly crime data for 2024.

---

### Hourly Comparison for 2023, 2024, and 2025

![Hourly Crime Comparison: 2023 Actual vs 2024 Actual vs 2025 Predicted](3_4_5.png)

This visualization compares hourly crime trends across three years, clearly reflecting seasonal similarity and SARIMA’s consistency across time.

---

### 2025 Predicted Risk Zones

![2025 Predicted Crime Risk Zones](risk_25.png)

The predicted map for 2025 classifies grid zones into **Low (green), Medium (yellow), and High (red)** risk areas based on expected crime volumes. This provides actionable intelligence for law enforcement.

---

### 2024 Predicted crime for Grid

![2025 Predicted crime for Grid](5_crime.png)

## **Methods**

#### **1. Time Series Forecasting using SARIMAX**
- **Used For:** Monthly crime count prediction  
- **Captured:** Seasonal patterns and lag-based correlations  
- **Target Variable:** Total crimes per month  
- **Input:** Time-indexed series with seasonal order 
- **Outcome:** Projected monthly crime counts for 2025  

#### **2. Spatial Classification using Random Forest**
- **Target Variable:** Crime frequency at a given hour and grid location  
- **Features:** `Hour`, `Day`, `Unemployment rate`, `Grid_ID`, `Crime Type (encoded)`  
- Applied Label Encoding and handled class imbalance via SMOTE  
- Achieved better generalization through 5-fold cross-validation  

**Additional Preprocessing:**
- Converted timestamps into hourly buckets  
- Generated grid-based zones using a custom lat/lon bucketing function  
- Merged unemployment rate based on date  
- Normalized features and handled nulls  

---
## **Results**

The machine learning framework developed in this project yielded valuable insights into the temporal and spatial dynamics of crime in Syracuse. The results are presented across two modeling phases: time-series forecasting and spatial classification.

### **1. Time-Series Forecasting with SARIMA**

Using 2023 crime data, we trained a **Seasonal ARIMA (SARIMA)** model to predict monthly crime counts for 2024. We then compared the predicted values with actual 2024 crime data obtained from the Syracuse Open Data Portal.

**Evaluation Metrics (2024 Prediction vs. 2024 Actual):**
- **Mean Absolute Error (MAE):** 25.29 crimes  
- **Root Mean Squared Error (RMSE):** 30.83 crimes  
- **Mean Absolute Percentage Error (MAPE):** 12.36%  
- **R² Score:** 0.8574

These results indicate strong predictive accuracy and seasonal fit, with SARIMA effectively modeling monthly crime fluctuations.

### **2. 2025 Hourly Crime Forecast**

We combined the cleaned 2023 and 2024 datasets to forecast **hourly crime counts for 2025**. A comprehensive line chart was generated to compare:
- Actual 2023 hourly trends  
- Actual 2024 hourly trends  
- Predicted 2025 hourly trends

This visualization captures cyclical crime behavior by hour of day and day of week, revealing consistent high-crime hours across years and allowing for pattern-based interventions.

### **3. Spatial Classification with Random Forest**

We implemented a **Random Forest classifier** to predict 2025 crime risk levels across city-wide grid cells (based on latitude/longitude bucketing). Each grid cell was labeled:
- **Low risk** (green)
- **Medium risk** (orange)
- **High risk** (red)

**Model Performance (using 5-fold cross-validation and SMOTE):**
- **Accuracy:** 88.6%  
- **F1-Score (macro):** 0.84  
- **Confusion Matrix:** Provided in the report

Additionally, we overlaid crime-type distributions per grid cell to identify which offenses were most common in high-risk zones. All outputs were displayed using interactive **folium-based maps**, enhancing stakeholder interpretability.

### **4. Random Forest Classification Results (2023 → 2024)**

We trained a **Random Forest classifier** on 2023's dominant crime types per grid and tested it on 2024 data. To handle class imbalance, we used **SMOTE (k=1)** during training.

-  **Accuracy:** 77.2%
-  **LARCENY F1-score:** 0.87
-  **Low performance** on underrepresented classes like BURGLARY
-  **Macro avg F1-score:** 0.39

The model effectively identified high-frequency crime types like *Larceny*, but struggled with rare classes due to imbalanced data. Still, it offers useful spatial insights for grid-level crime prediction.

---

## **Discussion**

Our project successfully met its key objectives of predicting when and where crimes are likely to occur in Syracuse. The use of **SARIMA** enabled accurate modeling of seasonal crime trends, while **Random Forest** offered robust spatial classification despite moderate class imbalance, addressed via **SMOTE oversampling**.

From a stakeholder perspective:
- **Law enforcement agencies** gain access to predictive tools that highlight peak crime hours and high-risk locations.
- **City planners** can use spatial risk insights to guide infrastructure development and surveillance deployment.
- **Community members** can view transparent, data-driven insights into crime risk by neighborhood.

Notably, while our models cannot predict exact events, they provide actionable patterns that support **prevention-first strategies**, increasing the city’s preparedness and response capabilities.

---

## **Limitations**

While the results are promising, the project has several limitations:

1. **Data Constraints:** The dataset only includes reported crimes; unreported incidents or errors in geolocation may bias results.
2. **Limited Feature Set:** We primarily used time, location, and unemployment rate. Additional factors such as weather, major events, or demographics could improve prediction accuracy.
3. **Hourly Prediction Limitations:** Hour-level SARIMA modeling was avoided due to data sparsity and variability at finer temporal resolution.
4. **Class Imbalance:** Despite SMOTE application, rare crime types still suffer from underrepresentation in classification results.
5. **Model Interpretability:** While Random Forest provides feature importance, deeper interpretability techniques (e.g., SHAP values) were not explored.

---

## **Future Work**

Several enhancements are planned for future iterations of this work:

- **Model Expansion:** Experiment with ensemble methods like Gradient Boosting and deep learning architectures (e.g., LSTM for sequential data).
- **Feature Enrichment:** Integrate weather, social media sentiment, and special event calendars to improve context-aware predictions.
- **Real-Time Prediction Engine:** Develop a dashboard or API for law enforcement to input real-time data and receive risk alerts.
- **Community Feedback Integration:** Include surveys or feedback loops to correlate predicted hotspots with perceived community safety.
- **Ethical Evaluation:** Explore the ethical implications of predictive policing models and incorporate fairness-aware learning frameworks.

## **Conclusion**

Our final approach combines **SARIMAX** for time trend forecasting and **Random Forest** for spatial classification, both integrated into visualizations for interpretability. This fusion allows city officials and stakeholders to understand crime dynamics in Syracuse more effectively and plan interventions accordingly.
