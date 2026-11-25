# Taxi Demand Forecasting

Forecasts hourly taxi demand for every New York City taxi zone and serves the forecasts through an API.

## Problem

<Write 2–3 sentences in your own words: who needs this forecast and why.>

## Data

- Source: NYC Taxi & Limousine Commission (TLC) trip records, published monthly as Parquet files.
- Taxi zone lookup table that maps zone IDs to boroughs and zone names.
- Raw data lives in `data/raw/` and is never committed to Git.

## Planned architecture

1. **Ingestion:** PySpark loads monthly trip files into Parquet.
2. **Features:** hourly demand per zone, plus time and calendar features.
3. **Model:** scikit-learn models with time-series cross-validation, tracked in MLflow.
4. **Serving:** a FastAPI prediction service in Docker.
5. **Monitoring:** data drift and model performance reports.

## Status

- [x] Project setup: uv, ruff, pytest, pre-commit, GitHub Actions CI
- [ ] Data ingestion pipeline
- [ ] Feature engineering
- [ ] Model training and tracking
- [ ] Prediction API
- [ ] Monitoring and deployment

## Development

### Prerequisites

- [uv](https://docs.astral.sh/uv/)
- Git

### Setup

```bash
git clone https://github.com/<your-username>/taxi-demand.git
cd taxi-demand
uv sync
uv run pre-commit install
```

### Common commands

| Command | What it does |
| --- | --- |
| `uv sync` | Creates `.venv` and installs the exact versions from `uv.lock` |
| `uv add <package>` | Adds a dependency to `pyproject.toml` and `uv.lock` |
| `uv add --dev <package>` | Adds a development-only tool |
| `uv run pytest -q` | Runs the tests |
| `uv run ruff check .` | Finds code problems |
| `uv run ruff format .` | Formats the code |
| `uv run pre-commit run --all-files` | Runs every pre-commit check on all files |

### Project structure

```text
src/taxi_demand/    application code
tests/              tests
notebooks/          exploration notebooks
data/raw/           raw data (not in Git)
docs/adr/           architecture decision records
.github/workflows/  CI pipeline
```
