# Forecasting Water Consumption Patterns in Urban Areas

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

A machine learning solution to forecast daily water consumption (in thousands of liters) for different urban zones, enabling proactive water resource management and uninterrupted supply planning.

---

## Problem Statement

A municipal water department in a growing metropolitan city aims to optimize water distribution and ensure adequate supply across different neighborhoods. Using historical water consumption data collected from various residential and commercial areas, the goal is to **build a predictive model** that forecasts daily water consumption based on factors such as:

- Weather conditions (temperature, humidity, rainfall)
- Population density
- Seasonal & temporal patterns
- Infrastructure characteristics (pipe age, residential/commercial units)

The water department will use these predictions to **proactively manage water resources**, plan maintenance schedules, and ensure uninterrupted water supply to all citizens.

---

## Dataset Description

| Column | Description |
|---|---|
| `zone_id` | Unique identifier for the urban zone |
| `date` | Date of measurement (YYYY-MM-DD) |
| `population_density` | Residents per km² in the zone |
| `temperature_avg` | Average temperature for the day (°C) |
| `humidity_avg` | Average humidity percentage |
| `rainfall` | Total rainfall for the day (mm) |
| `day_of_week` | Day of the week (1=Monday, 7=Sunday) |
| `month` | Month of the year (1–12) |
| `residential_units` | Number of residential buildings |
| `commercial_units` | Number of commercial establishments |
| `park_area` | Total park/green space area (hectares) |
| `pipe_age_avg` | Average age of water pipes (years) |
| `previous_day_consumption` | Previous day's consumption (thousands of liters) |
| **`water_consumption`** | **Target: Daily consumption (thousands of liters)** |

**Dataset Split:**
| File | Shape |
|---|---|
| `train.csv` | 12,000 × 14 |
| `test.csv` | 3,000 × 13 |
| `sample_submission.csv` | 3 × 2 |

---

## Tech Stack

- **Language:** Python 3.8+
- **Libraries:**
  - `pandas` — data manipulation & preprocessing
  - `scikit-learn` — model building (Random Forest Regressor)

---

## Approach & Methodology

### 1. Data Preprocessing
- Converted `date` column to datetime format
- Extracted additional temporal features: **day** and **year** from the date
- Dropped the original `date` column after feature extraction
- Removed `zone_id` from the training features (used only for submission mapping)

### 2. Feature Engineering
The following features are used for training:

| Feature | Type |
|---|---|
| `population_density` | Numeric |
| `temperature_avg` | Numeric |
| `humidity_avg` | Numeric |
| `rainfall` | Numeric |
| `day_of_week` | Categorical (encoded) |
| `month` | Categorical (encoded) |
| `residential_units` | Numeric |
| `commercial_units` | Numeric |
| `park_area` | Numeric |
| `pipe_age_avg` | Numeric |
| `previous_day_consumption` | Numeric |
| `day` | Extracted from date |
| `year` | Extracted from date |

### 3. Model Training
- **Algorithm:** Random Forest Regressor
- **Configuration:**
  - `n_estimators = 200` (200 decision trees in the ensemble)
  - `max_depth = 12` (controls tree complexity to prevent overfitting)
  - `random_state = 42` (ensures reproducibility)
  - `n_jobs = -1` (utilizes all CPU cores for parallel training)

### 4. Prediction & Submission
- Generated predictions on the unseen test data
- Created submission file with `zone_id` and predicted `water_consumption`

---

## Evaluation Metric

The model is evaluated using **Root Mean Squared Error (RMSE)**:

```
Score = 100 × max(0, 1 − (RMSE / max_RMSE))
```

Where `max_RMSE = 500` (thousands of liters) is used for normalization.

| Metric | Description |
|---|---|
| **RMSE** | Measures average prediction error magnitude |
| **Score Range** | 0 – 100 (higher is better) |

---

## How to Run

1. **Install dependencies**
   ```bash
   pip install pandas scikit-learn
   ```

2. **Place dataset files** in a `dataset/` folder:
   ```
   dataset/
   ├── train.csv
   ├── test.csv
   └── sample_submission.csv
   ```

3. **Run the notebook**
   ```bash
   jupyter notebook jupyter_notebook.ipynb
   ```

4. **Output** — `submission.csv` (3000 × 2) is generated in the root directory.

---

## Project Structure

```
Forecasting-Water-Consumption-Patterns-in-Urban-Areas/
├── dataset/
│   ├── train.csv
│   ├── test.csv
│   └── sample_submission.csv
├── jupyter_notebook.ipynb    # Solution notebook
├── submission.csv            # Generated predictions
└── README.md
```

---

## Constraints

| Constraint     | Value    |
|----------------|----------|
| Time Limit     | 5.0 sec  |
| Memory Limit   | 256 MB   |
| Source Limit    | 1024 KB  |

---

## License

MIT License - See LICENSE file for details
