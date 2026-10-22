# Diabetes Prediction API

A simple machine learning web API that predicts whether a person is likely to have diabetes. A trained Logistic Regression model (scikit-learn) is served with FastAPI.

> **Disclaimer:** This project is for learning and lab purposes only. It is not a medical tool and must not be used for diagnosis.

## Features

- `POST /predict` returns a predicted label, a text result, and a probability
- `GET /health` checks that the server is running
- Interactive documentation at `/docs` (Swagger UI)

## Project Structure

```
diabetes-prediction-api/
├── main.py            # FastAPI application
├── Mymdoel.pkl        # Trained model
├── requirements.txt   # Python dependencies
├── .gitignore
└── README.md
```

## Setup

1. Clone the repository:
   ```
   git clone https://github.com/<your-username>/diabetes-prediction-api.git
   cd diabetes-prediction-api
   ```

2. (Optional) Create a virtual environment:
   ```
   python -m venv venv
   venv\Scripts\activate
   ```

3. Install dependencies:
   ```
   python -m pip install -r requirements.txt
   ```

## Run the Server

```
python -m uvicorn main:app --reload --port 8000
```

When you see `Application startup complete.`, the server is ready. Open:

```
http://127.0.0.1:8000/docs
```

## Example Request

`POST /predict`

```json
{
  "Glucose": 148,
  "BloodPressure": 72,
  "Insulin": 0,
  "BMI": 33.6,
  "DiabetesPedigreeFunction": 0.627,
  "Age": 50
}
```

Example response (exact values depend on the model):

```json
{
  "predicted_label": 1,
  "prediction": "Diabetic",
  "probability": 0.78
}
```

**How to read it:** `predicted_label` is `1` for diabetic and `0` for not diabetic. `probability` is the model's confidence that the person is diabetic (0.78 means about 78%).

## Input Features

| Feature | Description |
|---|---|
| Glucose | Plasma glucose concentration |
| BloodPressure | Diastolic blood pressure (mm Hg) |
| Insulin | Serum insulin (mu U/ml) |
| BMI | Body mass index |
| DiabetesPedigreeFunction | Family history score |
| Age | Age in years |

## Tech Stack

- Python
- FastAPI and Uvicorn
- scikit-learn and pandas

## Note on the Model File

The `.pkl` file was saved with scikit-learn 1.9.0, so `requirements.txt` pins that version to avoid version warnings. Only load pickle files you trust, because they can run code when loaded.
