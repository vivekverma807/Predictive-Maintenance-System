# Predictive Maintenance System (Vehicle Health Prediction)

> **An AI-powered dashboard that monitors industrial assets, predicts remaining useful life (RUL), detects anomalies, and helps schedule proactive maintenance.**

## 📌 About

This system focuses on **Predictive Maintenance for Vehicles**, using machine learning to analyze vehicle sensor data such as engine temperature, RPM, vibration, fuel efficiency, battery voltage, tire pressure and more. The goal is to forecast component failures, detect anomalies early and estimate Remaining Useful Life (RUL) of critical vehicle parts.

It helps improve safety, reduce breakdowns, optimize service schedules and extend vehicle lifespan.

## 🔍 Project Description

Vehicles produce continuous real-time telemetry through OBD-II sensors, CAN bus data and onboard engine monitors. This project converts that data into actionable predictions by:

* collecting engine, battery, brake, tyre and fuel system metrics
* preprocessing and extracting meaningful features for model inputs
* training ML models that detect abnormal patterns and predict failures
* estimating RUL of engine parts, battery health or brake pad wear
* providing alerts and dashboards for maintenance scheduling

## ✨ Key Features

* Data ingestion pipeline (CSV, MQTT, or simulated stream)
* Data cleaning and feature engineering modules
* RUL prediction models (e.g., Random Forest, XGBoost, LSTM/GRU) with training notebooks
* Anomaly detection (Isolation Forest / Autoencoders) for early-warning alerts
* REST API for inference and alerts
* Interactive dashboard with historical & real-time visualization, asset health summary, and alerting
* Exportable maintenance plans and scheduled tasks

## 🧭 Architecture Overview

1. **Data Sources**: CSV files, IoT device streams (MQTT), or simulated sensor streams
2. **Ingestion & Storage**: ETL scripts write to a time-series database or PostgreSQL (TimescaleDB)
3. **Processing**: Batch/stream feature engineering with Python (Pandas, NumPy)
4. **Model Training**: Jupyter notebooks for experiments; models saved as pickles or ONNX
5. **Serving**: Flask/FastAPI endpoints for inference
6. **Dashboard**: React frontend (or plain HTML/JS) hitting the API for live metrics and alerts

## 🛠 Tech Stack

* Language: Python 3.9+
* Libraries: pandas, numpy, scikit-learn, xgboost, tensorflow / torch (optional), mlflow (optional)
* API: FastAPI or Flask
* Database: PostgreSQL (TimescaleDB) or InfluxDB
* Frontend: React.js (or Vue/Vanilla) + charting (Recharts / Chart.js)
* Containerization: Docker
* Optional: Kafka / MQTT for streaming ingestion, Redis for caching

## 📁 Repository Structure

```
Predictive-Maintenance-System/
├─ data/                   # sample datasets and data schema
├─ notebooks/              # exploratory analysis & training notebooks
├─ src/
│  ├─ ingestion/           # data ingestion scripts (CSV, MQTT simulators)
│  ├─ preprocessing/       # feature engineering, scaling, pipelines
│  ├─ models/              # model training & evaluation code
│  ├─ serving/             # API (FastAPI/Flask) for inference
│  ├─ dashboard/           # frontend source (React) or static dashboard files
│  └─ utils/               # helpers: logging, metrics, serializers
├─ scripts/                # convenience scripts: run_server.sh, train.sh
├─ docker/                 # Dockerfiles and compose configurations
├─ tests/                  # unit and integration tests
├─ requirements.txt
├─ README.md
└─ LICENSE
```

## 🚀 Quick Start — Local Development

1. Clone the repo

```bash
git clone https://github.com/vivekverma807/Predictive-Maintenance-System.git
cd Predictive-Maintenance-System
```

2. Create a virtual environment and install dependencies

```bash
python -m venv venv
source venv/bin/activate   # on Windows: venv\Scripts\activate
pip install -r requirements.txt
```

3. Load sample data (provided in `data/`) or start the simulator

```bash
python src/ingestion/simulate_stream.py --dataset data/sample_sensor.csv
```

4. Run preprocessing and training (example)

```bash
python src/models/train_model.py --config configs/train_config.yaml
```

5. Start the API server

```bash
uvicorn src.serving.api:app --reload --host 0.0.0.0 --port 8000
```

6. Start the frontend dashboard (if present)

```bash
cd src/dashboard
npm install
npm start
```

## 🔬 Data & Feature Engineering

* Recommended raw signals: vibration (x/y/z), temperature, RPM, current, voltage, pressure
* Common features: rolling mean/std, spectral features (FFT), kurtosis, skewness, peak-to-peak, RMS
* Labeling approach for RUL: use time-to-failure from historical runs or synthetic degradation curves
* Suggested preprocessing: imputation for missing values, robust scaling, and window-based aggregation

## 🧠 Models & Training

* Baseline models: Linear Regression, Random Forest Regressor for RUL
* Stronger models: XGBoost, LightGBM
* Sequence models: LSTM/GRU for sequence-to-one RUL prediction
* Anomaly detection: Isolation Forest, One-Class SVM, Autoencoder

**Model artifacts** should be saved to `models/` with a manifest file describing hyperparameters and training metrics.

## 📡 API Endpoints (example)

* `POST /predict` — send recent sensor window, returns predicted RUL and confidence
* `POST /anomaly` — send sensor window, returns anomaly score and flag
* `GET /assets` — list tracked assets and current health
* `GET /assets/{id}/history` — time-series of key metrics and predictions

## ✅ Evaluation & Metrics

* RUL: use MAE, RMSE, and Timeliness-based metrics (e.g., early/late prediction penalties)
* Classification (failure/no-failure in N hours): precision, recall, F1-score
* Anomaly detection: ROC-AUC, PR-AUC, and precision@k for top anomalies
* Use cross-validation across machines / runs to avoid leakage

## 📊 Dashboard Features

* Live time-series charts for sensors
* Asset health score and RUL forecast widget
* Alert feed for anomalies and critical RULs
* Maintenance schedule generator and export (CSV/ICS)
* Export charts and reports for stakeholders

## 🔧 Deployment

* Provide a `docker-compose.yml` to bring up DB, API, and frontend
* Use MLflow or Seldon for model management in production
* Enable authentication for the dashboard and APIs (JWT)
* Monitor model drift with periodic re-evaluation

## 🧪 Testing

* Unit test data transforms and preprocessing functions
* Integration tests for API endpoints (use test clients)
* End-to-end tests with simulated streaming data

## 🤝 Contributing

Contributions are welcome. Suggested workflow:

1. Fork the repo
2. Create a branch: `git checkout -b feature/your-feature`
3. Add tests and update docs
4. Open a pull request with a clear description

Please follow the repository's code style and ensure models and large artifacts are not checked in; use the `models/` manifest to reference trained artifacts.

## 📝 Roadmap

* [ ] Add streaming ingestion via Kafka or MQTT
* [ ] Integrate MLflow for tracking experiments and models
* [ ] Add containerized deployment with Helm charts
* [ ] Multi-tenant dashboard and team management
* [ ] Auto-scheduler for retraining and model drift detection

## 📄 License

This project is released under the MIT License. See `LICENSE` for details.

## ✉️ Contact

Created by **Vivek Kumar Verma**. For issues, feature requests, or collaboration, open an issue or contact: `vivekverma807@users.noreply.github.com`.

---

If you want, I can also:

1. Add badges (build, license, demo)
2. Create example `docker-compose.yml` and Dockerfiles
3. Generate starter notebooks for data preprocessing and training
4. Produce a short `CONTRIBUTING.md` or `DEPLOY.md`

Pick an option number or tell me what to add next.
