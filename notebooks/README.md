# Notebooks

The notebooks document the complete development workflow for the Industrial Surface Defect Detection project.

## Recommended Order

| # | Notebook | Purpose |
|---|---|---|
| 01 | `01_MVTec_Tile_Data_Validation_and_Splitting.ipynb` | Dataset validation, EDA, leakage checks, and split manifests |
| 02 | `02_MVTec_Tile_Baseline_and_Transfer_Learning.ipynb` | Baseline CNN and MobileNetV2 development/smoke tests |
| 02W | `02_MVTec_Tile_Baseline_and_Transfer_Learning_working.ipynb` | Protected working version used during development |
| 03 | `03_MVTec_Tile_Standard_Training.ipynb` | Standard training experiments |
| 04 | `04_MVTec_Tile_Validation_Analysis_and_Threshold_Selection.ipynb` | Validation metrics and threshold analysis |
| 05 | `05_MVTec_Tile_Controlled_Fine_Tuning.ipynb` | Controlled MobileNetV2 fine-tuning |
| 06 | `06_MVTec_Tile_Fine_Tuned_Threshold_Recalibration.ipynb` | Validation-only threshold recalibration |
| 07 | `07_MVTec_Tile_GradCAM_Explainability.ipynb` | Grad-CAM explainability analysis |
| 08 | `08_MVTec_Tile_Final_Test_Evaluation.ipynb` | Locked one-time final test evaluation |
| 09 | `09_MVTec_Tile_Final_Project_Summary.ipynb` | Final synthesis and project summary |

## Important Evaluation Rule

The test set was reserved for the final evaluation. Model and threshold decisions were made using training and validation information before the locked test evaluation.

## Expected Data Location

The notebooks expect the dataset under:

```text
data/raw/mvtec_ad/tile/
```

See `data/README.md` for the dataset documentation.
