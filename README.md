# Comparative Analysis of Data Mining Algorithms for Student Academic Performance Prediction

> **Third-Year Computer Engineering — Data Warehousing & Data Mining (DWDM) Mini-Project**

An academic analytics dashboard and machine learning platform comparing **Decision Tree (CART)**, **Random Forest**, **k-Nearest Neighbors (k-NN)**, and **Naive Bayes** for early prediction of student academic outcomes based on learning, behavioral, demographic, and social factors.

---

## Project Structure

```
├── backend/
│   ├── app.py                # Flask REST API server (/api/health, /api/metrics, /api/dataset, /api/predict)
│   ├── train_models.py       # Scikit-learn training & evaluation pipeline
│   ├── requirements.txt      # Python dependencies (flask, scikit-learn, pandas, numpy, joblib)
│   ├── data/                 # Benchmark student performance dataset
│   └── models/               # Saved trained model artifacts and metric evaluations (.joblib, .json)
├── src/
│   ├── components/           # Reusable UI components (Sidebar, Header, MetricsCard, ConfusionMatrix, etc.)
│   ├── views/                # Application pages (Dashboard, Predict, Model Comparison, Dataset, About)
│   ├── services/api.ts       # Centralized API service with configurable base URL (default http://127.0.0.1:5000)
│   ├── types/                # TypeScript interface definitions
│   └── utils/                # Pure logic, validation, and evaluation functions
├── README.md                 # Complete local setup and run instructions
└── package.json              # React, Vite, Tailwind CSS, Lucide icons, Recharts
```

---

## Getting Started Locally in VS Code

### Step 1: Clone or Open in VS Code
Open the project directory in VS Code:
```bash
code .
```

---

### Step 2: Set Up and Run the Python Flask Backend

1. Open a new terminal in VS Code (`Terminal -> New Terminal`):
```bash
cd backend
```

2. Create and activate a Python virtual environment:
- **macOS / Linux**:
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```
- **Windows (PowerShell / Command Prompt)**:
  ```powershell
  python -m venv venv
  venv\Scripts\activate
  ```

3. Install required packages:
```bash
pip install -r requirements.txt
```

4. Train the 4 Data Mining Models:
```bash
python train_models.py
```
*This prepares the UCI Student Performance benchmark dataset, fits Decision Tree, Random Forest, k-NN, and Naive Bayes classifiers, computes evaluation metrics (Accuracy, Precision, Recall, Macro F1, Confusion Matrices), and serializes models to `backend/models/`.*

5. Start the Flask API server:
```bash
python app.py
```
*The Flask backend will start on **`http://127.0.0.1:5000`** with CORS enabled.*

---

### Step 3: Run the React Frontend

1. Open a second terminal tab in VS Code:
```bash
npm install
npm run dev
```

2. Open your browser and navigate to:
```
http://localhost:3000   (or http://localhost:5173)
```

The frontend will automatically connect to your Flask backend at `http://127.0.0.1:5000`. You can also configure the backend URL via the status badge in the header.

---

## Machine Learning Algorithms Evaluated

| Algorithm | Type | Strengths in DWDM Context | Key Parameters |
|---|---|---|---|
| **Decision Tree (CART)** | Rule-based Non-parametric | Clear decision paths, high interpretability for educators | `criterion='gini'`, `max_depth=5` |
| **Random Forest** | Ensemble Bagging | Resists overfitting, captures non-linear feature interactions | `n_estimators=100`, `max_depth=6` |
| **k-Nearest Neighbors (k-NN)** | Instance-based | No assumptions on underlying data distribution | `k=5`, Euclidean metric, scaled features |
| **Naive Bayes (Gaussian)** | Probabilistic | Rapid inference, effective baseline on conditional independence | Gaussian likelihood, var smoothing |

---

## REST API Endpoints

- **`GET /api/health`**: Verifies backend connection and whether models are trained.
- **`GET /api/metrics`**: Returns accuracy, precision, recall, macro F1-score, training time, and confusion matrices for all 4 models.
- **`GET /api/dataset`**: Returns dataset feature definitions, sample records, and class distribution.
- **`POST /api/predict`**: Accepts student feature JSON and chosen algorithm; outputs predicted category, confidence, estimated score, and feature impact analysis.

---

## Academic Disclaimer
This software is developed as an academic engineering prototype for educational and research purposes under the Data Warehousing & Data Mining curriculum. It is intended to assist academic counselors in early intervention and is not a definitive psychological or cognitive assessment.
