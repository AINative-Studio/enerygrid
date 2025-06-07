# 📊 Energy Grid Load Optimizer — Backlog (Hackathon Build)

---

## 🚀 Epic 1: Project Bootstrap & Environment

**Goal:** Set up repo, framework, dependencies, and environment.

| Story ID | User Story                                                                                                                                                          | SSC Score |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| E1-S1    | As a developer, I need to initialize a FastAPI project structure so that I have a clean starting point for backend code.                                            | 1         |
| E1-S2    | As a developer, I need to configure package dependencies (`fastapi`, `uvicorn`, `httpx`, `sqlalchemy`, `pgvector`, etc.) so that my code can use external services. | 1         |
| E1-S3    | As a developer, I need to connect Supabase Postgres and verify vector extension (`pgvector`) is enabled.                                                            | 1         |

---

## 🚀 Epic 2: Database Schema & Models

**Goal:** Implement Supabase-compatible Postgres schema and ORM models.

| Story ID | User Story                                                                                                                              | SSC Score |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| E2-S1    | As a developer, I need to define SQL DDL to create `optimization_runs` table to store optimization request and result data.             | 1         |
| E2-S2    | As a developer, I need to define SQL DDL to create `optimization_embeddings` table to store vector embeddings of optimization requests. | 1         |
| E2-S3    | As a developer, I need to implement SQLAlchemy ORM models for these tables so that I can write/read records easily from Python code.    | 1         |

---

## 🚀 Epic 3: QNN API Client Integration

**Goal:** Build reusable Python client to connect to the QNN API.

| Story ID | User Story                                                                                                                                     | SSC Score |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| E3-S1    | As a developer, I need to build a QNN API client using `httpx` to call `/api/v1/predictions/predict` so that I can send optimization requests. | 2         |
| E3-S2    | As a developer, I need to build a QNN health check client to call `/api/v1/health/simple` to verify API availability.                          | 1         |

---

## 🚀 Epic 4: Core Forecast API Endpoints

**Goal:** Build API routes for load forecast and optimization.

| Story ID | User Story                                                                                                                    | SSC Score |
| -------- | ----------------------------------------------------------------------------------------------------------------------------- | --------- |
| E4-S1    | As an operator, I need a `POST /forecast` route to submit load forecast requests and store results.                           | 2         |
| E4-S2    | As an operator, I need a `POST /storage-optimize` route to submit storage optimization requests and store results.            | 2         |
| E4-S3    | As an operator, I need a `POST /grid-switch-optimize` route to submit grid switching optimization requests and store results. | 2         |
| E4-S4    | As a developer, I need a `GET /health` route that calls QNN `/health/simple` to verify external API status.                   | 1         |

---

## 🚀 Epic 5: Embedding Generation

**Goal:** Add embedding generation for future RAG and vector search.

| Story ID | User Story                                                                                                                   | SSC Score |
| -------- | ---------------------------------------------------------------------------------------------------------------------------- | --------- |
| E5-S1    | As a developer, I need to compute embeddings for each optimization request and store vectors into `optimization_embeddings`. | 3         |
| E5-S2    | As a developer, I need to integrate an embedding function (OpenAI or local) for encoding optimization input payloads.        | 2         |

---

## 🚀 Epic 6: Testing & Validation

**Goal:** Verify end-to-end functionality before demo.

| Story ID | User Story                                                                                                          | SSC Score |
| -------- | ------------------------------------------------------------------------------------------------------------------- | --------- |
| E6-S1    | As a developer, I need to write simple test payloads for forecast, storage, and grid switching to verify API logic. | 1         |
| E6-S2    | As a developer, I need to manually test the full pipeline from API request to QNN call to DB storage.               | 1         |
| E6-S3    | As a developer, I need to validate vector inserts for embedding table to ensure correctness.                        | 1         |

---

## 🚀 Epic 7: Deployment & Demo Readiness

**Goal:** Prepare for live hackathon demo.

| Story ID | User Story                                                                                                | SSC Score |
| -------- | --------------------------------------------------------------------------------------------------------- | --------- |
| E7-S1    | As a developer, I need to create a simple README with instructions to run, test, and demo the API.        | 1         |
| E7-S2    | As a developer, I need to containerize or configure local environment to ensure portable demo experience. | 1         |

---

# 🏷️ Total Backlog Summary

* Total stories: **20**
* All stories score **SSC ≤ 3** — very hackathon-ready
* Prioritized for **incremental value every 10-15 mins**

---

# 🔥 Optional Stretch Epic: Anomaly Monitoring (Future)

If you want to expand later using QNN anomaly endpoints:

* `/api/v1/monitoring/anomalies/`
* `/api/v1/monitoring/models/{model_id}/logs`
* `/api/v1/monitoring/anomalies/{anomaly_id}/resolve`

---

✅ **This backlog aligns 100% with your 1-hour sprint plan and PRD.**

---


