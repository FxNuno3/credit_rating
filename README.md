# Improved Omega² Temporal XGBoost Pipeline

## Issues Fixed

| Issue | Original | Fixed |
|-------|----------|-------|
| **1. Missing values** | `dropna()` destroys data | Median/KNN imputation per methodology |
| **2. Temporal grouping** | Sequential fallback | Proper date parsing from 'Rating Date' |
| **3. Data leakage** | 'Binary Rating' as feature | Excluded from features |
| **4. Preprocessing** | None | Winsorization, log transform, scaling |
| **5. Train leakage** | Univers scaling | Fit scaler on train only |
| **6. Reproducibility** | Not logged | All steps logged |

## Expected Results

- **Original**: 51.1% accuracy (random baseline)
- **Expected (per Omega² paper)**: AUC > 0.93, Accuracy >> 50%

## Usage

```bash
python corrected_pipeline/run_improved_xgb.py
```

## Post-run outputs

- `corrected_pipeline/summary_report_improved.csv`
- `corrected_pipeline/models/*_final_model.joblib`
- `corrected_pipeline/models/*_scaler.joblib`
- `corrected_pipeline/reports/*_holdout_report.json`
- `corrected_pipeline/model_metadata.json`

## API endpoint (FastAPI)

1. Install runtime dependencies:

```bash
pip install fastapi uvicorn
```

2. Start server:

```bash
cd corrected_pipeline
uvicorn api_server:app --reload --port 8000
```

3. Validate benchmark:

- GET `http://localhost:8000/benchmark`

4. Predict on a single sample:

- POST `http://localhost:8000/predict`

JSON body:

```json
{
  "features": {
    "Current Ratio": 1.1,
    "Debt/Equity Ratio": 0.3,
    ...
  }
}
```

Return includes predicted label and `benchmark_holdout_acc`.

Credit: https://github.com/Swarnendu-Bhattacharjee/OmegaSquared/tree/main
