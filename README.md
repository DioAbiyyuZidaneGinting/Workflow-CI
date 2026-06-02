# Workflow-CI — Telco Churn MLOps

Repositori CI/CD untuk submission Machine Learning Operations (MLOps) Dicoding.  
Workflow ini menjalankan pelatihan model secara otomatis menggunakan **MLflow** dan **GitHub Actions**.

**Nama:** Dio Abiyyu Zidane Ginting

---

## Struktur Repositori

```
Workflow-CI
├── .github/
│   └── workflows/
│       └── ci.yml                       ← GitHub Actions workflow
└── MLProject/
    ├── MLproject                        ← Konfigurasi MLflow Project
    ├── conda.yaml                       ← Environment dependencies
    ├── modelling.py                     ← Script pelatihan model (Random Forest + MLflow autolog)
    └── telco_churn_preprocessed.csv    ← Dataset preprocessed (dari repo Eksperimen)
```

## Cara Kerja Workflow CI

Setiap kali ada **push ke branch `main`/`master`** (khususnya pada folder `MLProject/`):

1. ✅ Checkout repository
2. ✅ Setup Python 3.12
3. ✅ Install dependencies (MLflow, scikit-learn, pandas, dll.)
4. ✅ Jalankan `mlflow run MLProject/` untuk melatih model
5. ✅ Upload artefak (mlruns, grafik, log) ke GitHub Actions Artifacts
6. ✅ Build Docker image
7. ✅ Push Docker image ke Docker Hub

## Fitur Modelling

- **Algoritma:** Random Forest Classifier
- **Autolog:** `mlflow.sklearn.autolog()` — params, metrics, & model ter-log otomatis
- **Artefak:** Confusion Matrix, ROC Curve, Feature Importance
- **Model Registry:** Disimpan sebagai `telco-churn-rf` di MLflow

## Secrets yang Diperlukan

| Secret | Keterangan |
|---|---|
| `DOCKERHUB_USERNAME` | Username Docker Hub |
| `DOCKERHUB_TOKEN` | Access token Docker Hub |
| `MLFLOW_TRACKING_URI` | URI MLflow tracking server (opsional) |
| `MLFLOW_TRACKING_USERNAME` | Username MLflow (opsional) |
| `MLFLOW_TRACKING_PASSWORD` | Password MLflow (opsional) |
