# ⚡ Electricity Load Prediction using Machine Learning

## 📌 Overview
This project predicts electricity load using machine learning based on time, past values, and trends.
It also detects high load conditions using a threshold.

---

## 🎯 Objective
- Predict electricity demand using historical data
- Capture time-based patterns
- Detect high load (anomalies)

---

## 📊 Dataset
The dataset contains:
- Date & Time
- Load (target variable)

This is a **time series dataset**, meaning the order of data is important.

---

## ⚙️ Feature Engineering
We created useful features from raw data to help the model learn better.

### 🕒 Time Features
- `hour` → Hour of the day
- `day` → Day of the month
- `month` → Month
- `dayofweek` → Day of the week

👉 These help capture daily and seasonal patterns.

---

### 🔁 Lag Feature
- `lag_1` → Load from previous time step

👉 Helps the model understand past dependency.

---

### 📉 Rolling Feature
- `rolling_mean_24` → 24-hour moving average

👉 Helps capture trend and smooth fluctuations.

---

## 🧠 Final Features Used
```python
features = [
    'hour',
    'day',
    'month',
    'dayofweek',
    'lag_1',
    'rolling_mean_24'
]
```

---

## ✂️ Train-Test Split
- 80% → Training data
- 20% → Testing data
- No shuffle (important for time series)

```python
split = int(len(df) * 0.8)

X_train = X[:split]
X_test = X[split:]

y_train = y[:split]
y_test = y[split:]
```

---

## 🌳 Model Used
**Random Forest Regressor**

- Ensemble model using multiple decision trees
- Handles non-linear patterns
- Gives stable and accurate predictions

```python
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor(n_estimators=100, random_state=42)
```

---

## 🏋️ Model Training
```python
model.fit(X_train, y_train)
```

👉 The model learns the relationship between features and load.

---

## 🚨 Anomaly Detection
We calculate a threshold using the 90th percentile:

```python
threshold = df['Load'].quantile(0.9)
```

👉 Values above this are considered high load.

---

## 💾 Saving Output
```python
import joblib
joblib.dump(threshold, "threshold.pkl")
```

---

## 🔄 Workflow
1. User inputs date & time
2. Features are generated automatically
3. Model predicts load
4. If load > threshold → High load alert

---

## 📈 Output
- Predicted Load Value
- High Load Alert (if applicable)

---

## ⚡ Advantages
- Handles complex patterns
- Uses past data for better prediction
- Works well without heavy tuning

---

## 🚧 Limitations
- Requires historical data
- Cannot predict unexpected events
- Depends on feature quality

---

## 🔮 Future Improvements
- Add weather data
- Use advanced models (LSTM, XGBoost)
- Deploy as real-time system

---

## 🛠️ Technologies Used
- Python
- Pandas
- NumPy
- Scikit-learn
- Joblib

---

## 🎤 Key Concepts
- **Time Series Data** → Data dependent on time
- **Lag Feature** → Previous values
- **Rolling Mean** → Trend smoothing
- **Random Forest** → Multiple trees for prediction

---

## 🙌 Conclusion
This project shows how machine learning can be used to predict electricity demand using time-based patterns and historical data, and detect high load conditions efficiently.
