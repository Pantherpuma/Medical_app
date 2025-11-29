# Health Data Simulation and Anomaly Detection

This project simulates multi-user health monitoring data and applies anomaly detection using machine learning techniques. The dataset includes vital signs and activity levels, which are preprocessed and analyzed to identify unusual patterns.

---

## Features

- **Simulated Health Data**: Generates time-series data for multiple users, including:
  - Heart rate
  - Blood oxygen level
  - Body temperature
  - Respiration rate
  - Activity level (low, moderate, high)
- **Preprocessing**:
  - Converts categorical activity levels to numeric values
  - Standardizes numerical features using `StandardScaler`
- **Anomaly Detection**:
  - Uses `IsolationForest` to detect outliers in the dataset
- **Evaluation**:
  - Generates a classification report for predicted anomalies

---

## Installation

Ensure you have Python 3.x installed. Install the required packages:

```bash
pip install numpy pandas scikit-learn
