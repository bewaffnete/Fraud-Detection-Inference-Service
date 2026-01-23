# Fraud Detection Inference Service

Real-time fraud detection inference service.  
Built with **Celery** + **RabbitMQ** as message broker, results and transaction data stored in **PostgreSQL**.  
Uses **XGBoost** model with strong class imbalance handling via **SMOTE**.  
Hyperparameters were optimized using **Optuna**.
<p align="center">
  <img src="static/new_data_conf_matrix.png" alt="confusion matrix" width="60%" />
  <img src="static/feature_importance_2.png" alt="feature importance" width="60%" />
</p>
<!-- ![new_data_conf_matrix.png](static/new_data_conf_matrix.png) -->
<!-- <p align="center"> -->
  <!-- <img src="static/feature_importance_2.png" alt="feature importance" width="60%" /> -->
<!-- </p> -->
<!-- ![feature_importance_2.png](static/feature_importance_2.png) -->

## Architecture

- **Backend**: Celery workers  
- **Message Broker**: RabbitMQ  
- **Database**: PostgreSQL  
- **ML Model**: XGBoost (trained with SMOTE + Optuna tuning)  
- **Deployment**: Docker + Docker Compose  

## Main Components

- `app/app.py` — Celery configuration and task registration  
- `worker/tasks.py` — main task `run_fraud_inference(**data_dict)` for model inference  
- `models/` — serialized XGBoost model (`xgb_final.joblib`) + preprocessing pipeline  
- `docker-compose.yml` — launches RabbitMQ, PostgreSQL and Celery workers  
## Quick Start (Local)

### Requirements
- Docker  
- Docker Compose  

### Run

```bash
docker-compose up --build
```
```
Flower localhost:5555
