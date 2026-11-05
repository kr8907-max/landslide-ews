# SIH 2026 — Landslide Early Warning System

AI-driven landslide risk monitoring and early warning for Northeast India, combining terrain susceptibility, rainfall, weather forecasts, historical events, and infrastructure exposure.

## Project layout

- `backend/` — FastAPI service, state-specific prediction services, model/data artifacts, processing scripts, and Python tests.
- `frontend/` — React, TypeScript, and Vite application.
- `docs/` — project audit and East Sikkim reproduction notes.

## Current status

This is a research prototype, not a fully provisioned production deployment. Model and training artifacts are included, but the terrain rasters listed in `backend/pilot_manifest.json` (24 artifacts, about 3.45 GB) are not in this checkout. Without those rasters, prediction endpoints that require terrain return `DATA_UNAVAILABLE`; this was verified locally. Configure `SIH_PILOT_ARTIFACT_BASE_URL` to enable the optional artifact download path, or prepare the required terrain data before expecting live predictions.

## Run locally

### Backend

From `backend/`, create and activate a virtual environment, install dependencies, and start the API:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m uvicorn app.main:app --reload
```

Run the backend tests with `python -m pytest -q tests`. On Windows, tests that require filesystem symlinks need symlink privileges (for example, Windows Developer Mode).

### Frontend

From `frontend/`:

```powershell
npm ci
npm run dev
npm test
npm run build
npm run lint
```

The frontend tests use Node's built-in test runner and TypeScript stripping.

## Development priorities

- Scientific validity and accurate data
- Spatial and temporal validation
- Explainable predictions and honest unavailable-data responses
- Reproducibility and real-world deployment feasibility