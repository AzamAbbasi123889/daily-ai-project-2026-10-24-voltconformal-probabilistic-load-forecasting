# Implementation Checklist

Build the application yourself using `PROJECT_BRIEF.md`.

## Initial setup

- [ ] Read the project specification.
- [ ] Review the architecture and data model.
- [ ] Create a Python virtual environment.
- [ ] Install and pin the required dependencies.
- [ ] Configure credentials through environment variables.
- [ ] Review the data privacy and security requirements.

## Project acceptance criteria

- [ ] Inference latency under 150ms for a 96-step forward horizon (24 hours at 15-min intervals)
- [ ] Pinball loss across test holdout is at least 12% lower than a seasonal persistence baseline
- [ ] Empirical quantile calibration within 2.5% deviation from nominal quantiles (e.g., P90 captures between 87.5% and 92.5% of observations)
- [ ] User can specify error rate alpha between 0.05 and 0.20 via API parameter
- [ ] Maintains empirical prediction interval coverage >= 1 - alpha on non-stationary test windows
- [ ] Outputs adaptive prediction band widths that naturally widen during cloud transient periods and narrow at night
- [ ] Reconciles bottom-up meter forecasts to aggregate transformer forecasts with zero summation residual
- [ ] Mean Absolute Scaled Error (MASE) of reconciled forecasts improves or stays within 1% of independent transformer-level forecasts
- [ ] BESS State of Charge (SoC) remains strictly bounded between 15% and 95% at all time steps
- [ ] Generates feasible schedule in less than 300ms using PuLP/CBC solver
- [ ] Demonstrates documented electric bill cost savings exceeding 18% compared to unmanaged heuristic charging in backtests
- [ ] Curate open microgrid dataset (e.g., OpenEI or Pecan Street open sample) downsampled to uniform 15-minute intervals.
- [ ] Implement temporal feature engineering pipeline (time-of-day, day-of-week, solar angles, 24h/168h lags, rolling standard deviations).
- [ ] Train multi-quantile LightGBM models for P10, P50, and P90 net-load.
- [ ] Implement split conformal prediction layer to generate statistically valid prediction bands at user-chosen alpha.
- [ ] Verify empirical coverage on held-out test windows.
- [ ] Implement hierarchical reconciliation matrix operations to ensure sub-meter coherence.
- [ ] Construct PuLP-based linear programming optimizer enforcing BESS limits, C-rates, and degradation penalties.
- [ ] Build FastAPI endpoints exposing ingestion, forecast, reconcile, and dispatch functionalities with Pydantic validation.
- [ ] Write backtesting benchmarking script comparing VoltConformal against deterministic point-forecast heuristic dispatch.
- [ ] Containerize application using Docker and create reproducible sample execution CLI.
- [ ] Unit tests for solar position calculations and time-lag feature extraction under missing timestamp scenarios using pytest.
- [ ] Property-based testing with Hypothesis ensuring conformal lower bounds are strictly less than or equal to upper bounds for all timesteps.
- [ ] Constraint validation tests for the PuLP dispatch optimizer verifying battery SoC never exceeds specified physical thresholds (e.g., [15%, 95%]).
- [ ] API integration tests using FastAPI TestClient asserting correct HTTP status codes, error handling for corrupted time-series schemas, and valid JSON schemas.
- [ ] Stress test generating forecasts and dispatch schedules for 50 concurrent microgrid nodes within 2 seconds.
- [ ] Multi-stage Dockerfile packaging FastAPI, LightGBM, and PuLP with minimal Debian slim base.
- [ ] Docker Compose environment pre-configured with local DuckDB volume and optional Redis cache for fast feature lookups.
- [ ] GitHub Actions pipeline running flake8/black linting, pytest suite, and automated backtest regression test on PRs.
- [ ] Deployable to free-tier cloud containers (Render, Railway, or Hugging Face Spaces) with zero proprietary vendor dependencies.

## Before completion

- [ ] Implement the planned MVP features.
- [ ] Add unit and integration tests.
- [ ] Run the test suite.
- [ ] Measure the evaluation metrics in the brief.
- [ ] Record actual results and known limitations.
- [ ] Document setup and deployment.
- [ ] Update the README to reflect the implemented features.
- [ ] Add only verified outcomes to your resume.
