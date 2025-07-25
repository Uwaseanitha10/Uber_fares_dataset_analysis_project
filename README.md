# 🚖 Uber Fares Dataset Analysis  

## 👋 Personal Introduction  

**By UWASE ANITHA** 
**ID: 26945 **
**Role: Data Analyst | Student At AUCA | Introduction to Big Data Analysis**
**My Kaggle Notebook: https://www.kaggle.com/code/uwaseanitha/introduction-to-big-data-analytic-kaggle**


## 📌 Introduction

This project analyzes Uber trip data to uncover actionable insights about fare patterns, demand fluctuations,and operational efficiency. 
The analysis supports data-driven decision-making for Uber's pricing strategies, driver allocation, and service optimization.

**Motivation**:  
- Explore real-world big data applications  
- Master Power BI for interactive dashboards  
- Solve business problems through data-driven decisions  

---

## 📌 Project Overview  

**Objective**:

Identify peak demand periods and seasonal trends

Analyze fare distribution and distance-fare relationships

Discover geographic hotspots for ride requests

Build an interactive Power BI dashboard for stakeholder use

**Key Features**:  

✔️ **Data Cleaning**: Handled missing values and outliers  
✔️ **Feature Engineering**: Extracted time-based features (hour/day/peak)  
✔️ **Interactive Dashboard**: Single-page Power BI report with cross-filtering  
✔️ **Business Insights**: Recommendations for dynamic pricing and driver allocation  

**Tools Used**:  
- **Python** (Pandas, Matplotlib) for EDA  
- **Power BI** for visualization  
- **GitHub** for version control 

---

## 🔍 Project Breakdown  

### 1. Data cleaning Preparation  
 
**Code Highlight**:  

```python

# Check for missing values
print(df.isnull().sum())

# Drop rows with missing key values
df.dropna(subset=['pickup_datetime', 'pickup_latitude', 'pickup_longitude',
                  'dropoff_latitude', 'dropoff_longitude', 'fare_amount'], inplace=True)

# Remove rows with invalid fare amounts
df = df[(df['fare_amount'] > 0) & (df['fare_amount'] < 1000)]

# Filter latitude and longitude (NYC bounds as rough check)
df = df[(df['pickup_latitude'].between(40, 42)) & 
        (df['pickup_longitude'].between(-75, -72)) &
        (df['dropoff_latitude'].between(40, 42)) &
        (df['dropoff_longitude'].between(-75, -72))]

print("Shape after cleaning:", df.shape)
```

**Screenshots**:  

---

<img width="869" height="392" alt="shape after cleaning" src="https://github.com/user-attachments/assets/5116a105-352d-4a92-98e0-082120ef2762" />

### 2. Exploratory Analysis

**Code Highlight**:  

```python
from geopy.distance import geodesic

# Convert pickup_datetime to datetime
df['pickup_datetime'] = pd.to_datetime(df['pickup_datetime'])

# Extract temporal features
df['hour'] = df['pickup_datetime'].dt.hour
df['day'] = df['pickup_datetime'].dt.day
df['month'] = df['pickup_datetime'].dt.month
df['weekday'] = df['pickup_datetime'].dt.day_name()
df['year'] = df['pickup_datetime'].dt.year

# Peak hours (7-9 AM or 5-7 PM)
df['is_peak'] = df['hour'].apply(lambda x: 1 if 7 <= x <= 9 or 17 <= x <= 19 else 0)

# Calculate distance (in km)
def calculate_distance(row):
    pickup = (row['pickup_latitude'], row['pickup_longitude'])
    dropoff = (row['dropoff_latitude'], row['dropoff_longitude'])
    return geodesic(pickup, dropoff).km

df['distance_km'] = df.apply(calculate_distance, axis=1)

print(df[['fare_amount', 'hour', 'weekday', 'is_peak', 'distance_km']].head())

```

**Screenshots**:  


<img width="931" height="415" alt="distance calculations" src="https://github.com/user-attachments/assets/87020d56-c4d9-480b-a5a6-cc96f1b1c12e" />

**3. Power BI Dashboard**
 
**Screenshots**

<img width="939" height="461" alt="power BI" src="https://github.com/user-attachments/assets/96ed1a81-8b95-436f-80ce-3bd2eab5231e" />

🔗 Links & Resources

Dataset Source: [Uber Fares Dataset - (Kaggle)] (https://www.kaggle.com/datasets/yasserh/uber-fares-dataset)

Power BI Documentation: Microsoft Learn

---

📬 Contact & Connect
Feel free to contact me  for more information or if any problem
Email:uwaseanitha1010@gmail.com

---

🎨License: MIT
Last Updated: July 2025

---
