<div align="center">

# ✈️ Flight Price Prediction

> **End-of-Year Project (PFA) — Amine Chebil, 2024**
> 
> A machine learning project to predict flight ticket prices.

</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Data Preprocessing](#data-preprocessing)
- [Models](#models)
- [Results](#results)
- [Tools Used](#technologies-used)

---

## 🔍 Overview

This project builds a flight price prediction system to enhance package offers for a travel agency by accurately predicting prices. We plan to achieve this by using machine learning models on a cleaned and prepared dataset.

Our goal is to develop a prediction system that effectively analyzes data and generates precise forecasts. This approach will enable the travel agency to make informed decisions regarding pricing and package customization, ultimately enhancing its competitiveness and profitability in the dynamic travel market.

The best-performing model achieves an **R² score of 0.9969**, demonstrating near-perfect price prediction capability.

---

## 📊 Dataset

The data was collected from Nouvelair's flight schedules and covers routes between Tunisia and several French cities.

### Features

| Column | Description |
|---|---|
| `JOUR` | Day of the week (Monday–Sunday) |
| `MOIS` | Month (1–12) |
| `DATE DEPART` | Departure date |
| `N° VOL` | Flight number |
| `VILLE DE DEPART` | Departure city |
| `VILLE D'ARRIVEE` | Arrival city |
| `TIME DEPART` | Departure time |
| `TIME ARRIVEE` | Arrival time |
| `CLASS` | Flight class |
| `CODE` | Flight code |
| `PRIX TTC` | Ticket price (€) |
| `DISPONIBILITE` | Seat availability (how many seats left for the flight) |

---

## 🔧 Data Preprocessing

The raw Excel files were merged and cleaned through several steps:

1. **Column removal:** — Dropped irrelevant columns (`COMPARE PRICE`, `DIFF PRICE`, `COMPARE DISPO`, `N° VOL` and `CODE`)
2. **Filtering** — Removed rows with `DISPONIBILITE` of 0 or 1 (unavailable/single seat), and excluded Strasbourg routes (insufficient data)
3. **Outlier removal** — Removed erroneous prices of €1 and €2
4. **Handling duplicates** — Kept the last occurrence of duplicate rows
5. **Data transformation:**
   - Datetime conversion on columns `DATE DEPART`, `TIME DEPART` and `TIME ARRIVEE` to standardize their format into datetime objects
   - Changed the data type of the CLASS column to string to prepare it for encoding
6. **Feature engineering:**
   - Extracted `DAY`, `depart_hour`, `depart_minute`, `arrival_hour`, `arrival_minute` from datetime columns
   - Computed `dur_min` (flight duration in minutes)
   - Applied **One-Hot Encoding** to departure and arrival cities
   - Encoded `JOUR` (day of week) and `CLASS` using **Label Encoding**
   - Applied **Min-Max Scaling** to time-related numerical features: `depart hour`, `depart minute`, `arrival hour`, `arrival minute` and `dur min`, thereby standardizing their ranges to fall between 0 and 1.
   
---

## 🤖 Models

Three regression models were trained and evaluated:

### 1. XGBoost Regressor ⭐ (Best)
### 2. Random Forest Regressor
### 3. Extra Trees Regressor

All models used an 80/20 train-test split with `random_state=42`.

---

## 📈 Results

| Model | R² Score | MAE | RMSE |
|---|---|---|---|
| **XGBoost Regressor** | **0.9969** | **4.19** | **7.50** |
| Random Forest Regressor | 0.9954 | 4.64 | 9.03 |
| Extra Trees Regressor | 0.9943 | 4.87 | 10.09 |

**XGBoost** achieved the best performance with an R² of **0.9969**, a Mean Absolute Error of just **€4.19**, and an RMSE of **€7.50**.

---

## 🛠️ Tools Used

- **Python** (Google Colab)
- **Pandas** — data manipulation
- **NumPy** — numerical operations
- **Matplotlib / Seaborn** — data visualization
- **Scikit-learn** — preprocessing, model evaluation, Random Forest, Extra Trees
- **XGBoost** — gradient boosting regression

---

## 📄 License

This project was developed as an academic end-of-year project. Feel free to use the code for educational purposes.

---

*Made with ❤️ by Amine Chebil — 2024*