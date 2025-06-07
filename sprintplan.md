# ⚡ 1-Hour Agile Sprint Plan

**Project:** Energy Grid Load Optimizer — QNN Rapid Build
**Team:** Solo (LLM pair programming ready)

---

## 🎯 Sprint Goal:

> ✅ Fully functional backend API that:
>
> * Wraps QNN APIs for forecast, storage, grid switching
> * Stores optimization runs into Postgres (Supabase)
> * Supports vector storage for future semantic retrieval

---

## 🕐 Sprint Timebox: **60 min**

---

### 🏁 0–5 min: Repo Bootstrap

* Create new repo + local project
* Initialize FastAPI project (`fastapi`, `uvicorn`, `pydantic`, `httpx`)
* Install pgvector extension on Supabase if not done:

```sql
create extension if not exists vector;
```

* Install Python packages:

```bash
pip install fastapi uvicorn pydantic httpx psycopg2-binary pgvector sqlalchemy
```

---

### 🔗 5–10 min: Setup DB Models

* Create SQLAlchemy ORM models for:

  * `optimization_runs`
  * `optimization_embeddings`
  * (skip `anomalies` & `qnn_execution_metrics` for now)

* Use the SQL DDL we generated

---

### ⚙️ 10–20 min: Build QNN Client Service

* Build small internal Python client for calling:

  * `POST /api/v1/predictions/predict`
  * `GET /api/v1/health/simple`
* Use `httpx.AsyncClient` for non-blocking API calls
* Centralize base URL & token configs

---

### 🔌 20–40 min: Build Core API Routes

#### `/health` route (5 min)

* Pings QNN `/api/v1/health/simple`

#### `/forecast` route (7 min)

* Accepts POST payload
* Calls QNN `predict`
* Stores `optimization_run` + result JSON

#### `/storage-optimize` route (7 min)

* Same as forecast, different request\_type

#### `/grid-switch-optimize` route (7 min)

* Same pattern, different request\_type

---

### 🧠 40–50 min: Build Vectorization Logic

* Add simple OpenAI embedding call or local embedding function (mock allowed)
* Store vectors into `optimization_embeddings` for each run

```python
# Example:
embedding = embed_function(payload_json)
```

* Use pgvector `VECTOR(1536)` field

---

### 🚀 50–55 min: End-to-End Test & Local Run

* Hit all routes with mocked test data
* Verify:

  * QNN API returns valid response
  * Postgres writes properly
  * Vectors stored correctly

---

### 📦 55–60 min: Final Polish

* Quick README scaffold:

  * Setup
  * `.env` file
  * Run instructions
* Sanity check logs & error handling

---

# ✅ Deliverables at End

* Full API server live locally
* QNN integration complete
* All optimization requests logged
* Vector storage live for future RAG expansion
* Supabase schema deployed

---

# ⚠️ Constraints Reminder

* No UI
* No admin dashboard
* No training, just inference
* Minimal error handling
* Focus: **Demo-Ready API backend**

---


