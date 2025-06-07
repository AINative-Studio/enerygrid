# 📄 Revised PRD: **Energy Grid Load Optimizer — QNN Rapid Prototype**

---

## 1️⃣ Executive Summary

We will build a **QNN-powered Energy Grid Load Optimizer** that:

* Forecasts energy demand
* Optimizes battery storage schedules
* Simulates grid switching configurations
* Uses the QNN API capabilities directly (no custom model training for this prototype)
* Fully serverless / backend API-first, built in under 1 hour

---

## 2️⃣ QNN API Endpoints to Leverage

Here’s how we will directly reuse the existing QNN API:

| Functional Need                      | QNN API Used                         | Notes                                                                                                              |
| ------------------------------------ | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| **Health Check**                     | `/api/v1/health/simple`              | Verify API is online                                                                                               |
| **Prediction / Forecasting**         | `/api/v1/predictions/predict`        | We will repurpose the generic `predict` endpoint to forecast loads by encoding load profile data into "code" input |
| **Optimization Logic**               | `/api/v1/predictions/predict`        | Also used for optimizing storage & grid switching by embedding optimization objectives into input payload          |
| **Anomaly Detection (Stretch Goal)** | `/api/v1/monitoring/anomalies/`      | Can later monitor for load forecasting anomalies                                                                   |
| **Cost & Execution Monitoring**      | `/api/v1/monitoring/quantum/metrics` | Monitor API usage & quantum resource utilization                                                                   |

We are essentially **prompting the QNN Predict endpoint** with encoded load data to simulate optimization problems.

---

## 3️⃣ API Design for Wrapper (Our App)

We’ll build a simple **FastAPI Backend** that wraps calls to QNN.

### Our API:

#### POST `/forecast`

* ✅ Calls QNN `/api/v1/predictions/predict` with encoded historical load data.

#### POST `/storage-optimize`

* ✅ Calls QNN `/api/v1/predictions/predict` with encoded storage utilization profiles.

#### POST `/grid-switch-optimize`

* ✅ Calls QNN `/api/v1/predictions/predict` with encoded grid switching state.

#### GET `/health`

* ✅ Pings QNN `/api/v1/health/simple`.

---

## 4️⃣ Input Example (Encoding Forecast into QNN)

```json
{
  "code": "Region=California; Date=2025-06-07; PastLoads=[200,210,220,230,225,215]; ForecastGoal=Next24Hours",
  "model_id": "PRETRAINED_QNN_GRID_MODEL",
  "mode": "quantum",
  "optimization_level": 1
}
```

> ✅ This approach allows us to simulate forecasting using generic QNN inference without training a domain-specific model.

---

## 5️⃣ Database Model (Supabase)

```sql
Table: optimization_runs
- id UUID PK
- request_type (ENUM: forecast, storage, grid_switch)
- input_payload JSONB
- result_payload JSONB
- created_at TIMESTAMP DEFAULT now()
- status TEXT
```

---

## 6️⃣ Stack

| Layer     | Technology                        |
| --------- | --------------------------------- |
| Backend   | FastAPI (Python 3.11)             |
| Data      | Supabase (Postgres)               |
| Model API | QNN API                           |
| Hosting   | Localhost or Docker for Hackathon |

---

## 7️⃣ Agile 1-Hour Sprint Plan

| Task                                          | Time Alloc |
| --------------------------------------------- | ---------- |
| Setup FastAPI project                         | 10 min     |
| Build health check                            | 5 min      |
| Build QNN wrapper for `/forecast`             | 10 min     |
| Build QNN wrapper for `/storage-optimize`     | 10 min     |
| Build QNN wrapper for `/grid-switch-optimize` | 10 min     |
| Build Supabase insert logic                   | 5 min      |
| Build simple CLI test client                  | 5 min      |
| Buffer / Debug / Polish                       | 5 min      |

---

## 8️⃣ Success Criteria

* ✅ All endpoints working
* ✅ Stored responses into DB
* ✅ Live demo with mocked data through QNN inference
* ✅ No custom ML model training required

---

## ⚠️ NOTE:

By using the **Prediction endpoint** creatively and encoding the grid optimization problem as structured input, you're massively accelerating development without needing full domain-specific models trained.

This is **exactly how to pitch it to the VC as well.**

---


