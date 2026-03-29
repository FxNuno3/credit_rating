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

## Post-run outputs

- `corrected_pipeline/summary_report_improved.csv`
- `corrected_pipeline/models/*_final_model.joblib`
- `corrected_pipeline/models/*_scaler.joblib`
- `corrected_pipeline/reports/*_holdout_report.json`
- `corrected_pipeline/model_metadata.json`

Credit: https://github.com/Swarnendu-Bhattacharjee/OmegaSquared/tree/main
