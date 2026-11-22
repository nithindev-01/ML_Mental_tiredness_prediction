# 🧠 Mental Tiredness Score Prediction

A machine learning web app that predicts a **mental tiredness score** from a person's daily work activity, health habits, and working environment. Enter your details, click **Predict**, and get an instant score with a plain-language tiredness level.

🔗 **Live demo:** [ml-mental-tiredness-prediction.streamlit.app](https://ml-mental-tiredness-prediction.streamlit.app/)

<img width="907" height="895" alt="image" src="https://github.com/user-attachments/assets/7dc7a252-a6ae-4a1e-80a3-87d8e58ed0fa" />


---

## Overview

Mental fatigue is shaped by many everyday factors: how much we sleep, how often we are interrupted, how long we stare at screens, and even how noisy the room is. This project trains a regression model on these factors and serves it through an interactive Streamlit interface.

The app takes 17 inputs, builds two engineered features from them, and returns a predicted score (clipped to a minimum of 0) with a color-coded interpretation.

## Features

- Interactive form with sliders, number inputs, and dropdowns, grouped into three sections
- Real-time prediction from a pre-trained scikit-learn-style model (`model.pkl`)
- Feature engineering applied at inference time, identical to training
- Color-coded result: 🟢 low, 🟡 moderate, 🔴 high tiredness
- Custom-styled UI (gradient background, frosted-glass card, styled button)
- Graceful error message if the model file is missing

## Inputs

| Category | Features |
|---|---|
| 💼 **Work activity** | Decisions made, context switches, notifications received, screen time (min), deep work (min), average task complexity, workload score, breaks taken |
| 😴 **Health & lifestyle** | Sleep hours, deep sleep %, caffeine (mg), hydration (litres), mood (Happy / Neutral / Low) |
| 🏢 **Environment** | Work type (Office / Remote / Manual / Student), work environment (Quiet / Moderate Noise / Noisy), noise level (dB), temperature (°C) |

### Engineered features

Two additional features are computed from the inputs before prediction:

- `deep_sleep_hours = sleep_hours × (deep_sleep_pct / 100)`
- `workload_intensity = workload_score × context_switch_count`

## Interpreting the score

| Score | Level | Meaning |
|---|---|---|
| < 20 | 🟢 Low | Well rested |
| 20 to 40 | 🟡 Moderate | Consider taking regular breaks |
| ≥ 40 | 🔴 High | Rest, sleep, and fewer context switches may help |

The thresholds are indicative and based on the dataset's score range (roughly 0 to 77).

## Tech stack

- **Language:** Python
- **Web app:** Streamlit
- **Data handling:** pandas
- **Model:** scikit-learn-based regression model saved with joblib/pickle
- **Deployment:** Streamlit Community Cloud

## Project structure

```
ML_Mental_tiredness_prediction/
├── app.py             # Streamlit app: UI, feature engineering, prediction
├── model.pkl          # Trained regression model
└── requirements.txt   # Python dependencies
```

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/nithindev-01/ML_Mental_tiredness_prediction.git
cd ML_Mental_tiredness_prediction
```

### 2. (Optional) Create a virtual environment

```bash
python -m venv venv
source venv/bin/activate      # On Windows: venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the app

```bash
streamlit run app.py
```

Then open the local URL shown in your terminal (usually `http://localhost:8501`).

> **Note:** The saved model was trained with a specific scikit-learn version. If you see a version warning or loading error, install the version pinned in `requirements.txt`.

## How it works

1. The user fills in the form, and the values are collected into a pandas DataFrame.
2. The two engineered features are added to match the training pipeline.
3. The loaded model predicts the tiredness score.
4. The score is clipped at 0 and mapped to a low, moderate, or high level.

The model is loaded once and cached with `st.cache_resource` so predictions stay fast.

## Model details

<!-- Fill these in from your training notebook so recruiters can see the ML work -->


## Limitations

- This is an educational project, not a medical or diagnostic tool.
- Predictions reflect patterns in the training data and may not generalize to everyone.
- Score thresholds for low, moderate, and high are indicative only.

## Future improvements

- Add feature importance or SHAP explanations to show which habits drive a score
- Include the training notebook and dataset description in the repo
- Add input validation and unit tests
- Track history so users can see their score over time

## Author

**Nithin Dev**
GitHub: [@nithindev-01](https://github.com/nithindev-01)
