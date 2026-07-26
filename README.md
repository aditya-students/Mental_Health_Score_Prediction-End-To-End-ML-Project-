# 🧠 Mental Health Score Prediction — End-To-End ML Project

A full-stack machine learning application that predicts a student's **mental health score (0–10)** based on their daily habits, social media usage, academic profile, and stress levels. Built with a **Random Forest Regressor** on the backend and a sleek, modern web interface on the frontend.

> ⚠️ **Disclaimer:** This tool is built for informational and educational purposes only — it is **not** a clinical assessment. If you're struggling, please talk to someone you trust.

---

## 📸 Overview

The application collects student lifestyle data through an interactive form and sends it to a FastAPI backend, which runs the input through a pre-trained scikit-learn pipeline to return a predicted mental health score displayed on an animated gauge.

---

## 🚀 Features

- **End-to-end ML pipeline** — from raw data to deployed prediction API
- **Random Forest Regressor** with preprocessing (scaling, encoding, log transforms)
- **FastAPI** backend serving predictions via a REST API
- **Modern, responsive UI** with SVG gauge animation, glassmorphism, and micro-interactions
- **Client-side validation** mirroring the Pydantic model on the server
- **CORS-enabled** API for seamless frontend–backend communication

---

## 🛠️ Tech Stack

| Layer        | Technology                                                  |
| ------------ | ----------------------------------------------------------- |
| **ML Model** | scikit-learn (RandomForestRegressor, Pipeline)               |
| **Backend**  | Python, FastAPI, Uvicorn, Pydantic                           |
| **Frontend** | HTML5, CSS3 (vanilla), JavaScript (vanilla)                  |
| **Data**     | pandas, NumPy                                                |
| **Fonts**    | Google Fonts (Inter, Fraunces, JetBrains Mono)               |

---

## 📂 Project Structure

```
├── Mental_Health_Score.ipynb                        # Jupyter notebook — EDA, training, evaluation
├── Student Social Media And Mental Health Impact.csv # Raw dataset
├── Mental_Health_Model.pkl                          # Trained scikit-learn pipeline (serialised)
├── main.py                                          # FastAPI application with /predict endpoint
├── requirements.txt                                 # Python dependencies
├── index.html                                       # Frontend — form & result panel
├── script.js                                        # Frontend logic — validation, API calls, gauge
├── style.css                                        # Styling — dark theme, animations, layout
├── .gitignore                                       # Ignores venv/, __pycache__/, etc.
└── README.md                                        # You are here
```

---

## 📊 ML Pipeline Details

The model is a **scikit-learn `Pipeline`** with two stages:

### 1. Preprocessing (`ColumnTransformer`)

| Transformer       | Columns                                                                                       | Steps                          |
| ------------------ | --------------------------------------------------------------------------------------------- | ------------------------------ |
| **Skewed Pipeline** | `Study_Hours`                                                                                 | `log1p` → `StandardScaler`    |
| **Plain Numeric**  | `Age`, `Avg_Daily_Usage_Hours`, `Daily_Unlocks`, `Physical_Activity_Hours`, `Sleep_Hours_Per_Night` | `StandardScaler`               |
| **Ordinal**        | `Stress_Level`                                                                                | `OrdinalEncoder` (Low → Very High) |
| **Nominal**        | `Gender`, `Academic_Level`, `Most_Used_Platform`, `Purpose_Of_Use`, `Grouped_country`         | `OneHotEncoder`                |

### 2. Model

- **Algorithm:** `RandomForestRegressor(random_state=42)`
- **Target:** `Mental_Health_Score` (continuous, 0–10)

---

## ⚙️ Setup & Installation

### Prerequisites

- Python 3.9+
- pip

### 1. Clone the repository

```bash
git clone https://github.com/aditya-students/Mental_Health_Score_Prediction-End-To-End-ML-Project-.git
cd Mental_Health_Score_Prediction-End-To-End-ML-Project-
```

### 2. Create a virtual environment

```bash
python -m venv venv

# Windows
.\venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the backend (FastAPI)

```bash
uvicorn main:app --port 2200 --reload
```

The API will be available at **http://127.0.0.1:2200** and the interactive docs at **http://127.0.0.1:2200/docs**.

### 5. Serve the frontend

```bash
python -m http.server 8000
```

Open **http://localhost:8000** in your browser.

---

## 🔌 API Reference

### `POST /predict`

Accepts student data and returns a predicted mental health score.

**Request Body (JSON):**

```json
{
  "age": 21,
  "gender": "Male",
  "country": "India",
  "academic_level": "Undergraduate",
  "most_used_platform": "Instagram",
  "purpose_of_use": "Entertainment",
  "avg_daily_usage_hours": 4.5,
  "daily_unlocks": 60,
  "study_hours": 3.0,
  "physical_activity_hours": 1.0,
  "sleep_hours_per_night": 7.0,
  "stress_level": "Medium"
}
```

**Response (JSON):**

```json
{
  "predicted_mental_health_score": 6.42
}
```

---

## 📈 Dataset

- **Source:** `Student Social Media And Mental Health Impact.csv`
- **Records:** ~1,000+ student responses
- **Features:** Age, Gender, Country, Academic Level, Social Media Platform & Usage, Study Hours, Physical Activity, Sleep, Stress Level
- **Target:** Mental Health Score (0–10)

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to open an issue or submit a pull request.

---

## 📄 License

This project is open source and available for educational purposes.
