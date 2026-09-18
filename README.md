# Industrial Surface Defect Detection Using Deep Learning and Explainable AI

This project develops a supervised binary image classifier for the **Tile** category of MVTec AD. The operational classes are **Good** and **Defective**. The workflow includes leakage-safe data splitting, exploratory analysis, a custom CNN baseline, MobileNetV2 transfer learning, controlled fine-tuning, validation-only threshold calibration, Grad-CAM explanations, a confidence-based human-review policy, and one locked final test evaluation.

## Final result

The selected model is a fine-tuned MobileNetV2. The last 20 backbone layers were made eligible for training while BatchNormalization layers remained frozen. Fine-tuning used Adam with a learning rate of `1e-5`, training-only augmentation, class weights, checkpointing, early stopping, and learning-rate reduction.

The operating thresholds were fixed on the validation split before the test set was evaluated:

- Binary defective threshold: `0.152666`
- Automatic Good: probability below `0.152666`
- Needs Human Review: probability from `0.152666` to below `0.439`
- Automatic Defective: probability at or above `0.439`

Final locked test results on 51 images:

| Metric | Value |
|---|---:|
| Accuracy | 94.12% |
| Defective precision | 90.91% |
| Defective recall | 83.33% |
| F1-score | 86.96% |
| ROC-AUC | 97.44% |
| PR-AUC | 94.44% |
| True negatives / False positives | 38 / 1 |
| False negatives / True positives | 2 / 10 |

The locked human-review policy referred one image for review. Two defects (`gray_stroke` and `rough`) were automatically classified as Good. This limitation is reported without adjusting thresholds after test evaluation.

## Scientific scope and caveat

MVTec AD was originally designed for unsupervised anomaly detection. This project deliberately reformulates the Tile category as supervised binary classification. Original images were assigned to train, validation, and test manifests with fixed seeds and duplicate/group leakage checks. Augmentation occurs only in the training pipeline. Hyperparameters and thresholds are selected only with validation data.

The dataset is not included in this repository. Preserve the original MVTec AD directory structure under:

```text
data/raw/mvtec_ad/tile/
```

## Project Structure

```text
Industrial-surface-defect-detection/
├── README.md
├── .gitignore
├── requirements.txt
│
├── notebooks/
│   ├── 01_MVTec_Tile_Data_Validation_and_Splitting.ipynb
│   ├── 02_MVTec_Tile_Baseline_and_Transfer_Learning.ipynb
│   ├── 02_MVTec_Tile_Baseline_and_Transfer_Learning_working.ipynb
│   ├── 03_MVTec_Tile_Standard_Training.ipynb
│   ├── 04_MVTec_Tile_Validation_Analysis_and_Threshold_Selection.ipynb
│   ├── 05_MVTec_Tile_Controlled_Fine_Tuning.ipynb
│   ├── 06_MVTec_Tile_Fine_Tuned_Threshold_Recalibration.ipynb
│   ├── 07_MVTec_Tile_GradCAM_Explainability.ipynb
│   ├── 08_MVTec_Tile_Final_Test_Evaluation.ipynb
│   └── 09_MVTec_Tile_Final_Project_Summary.ipynb
│
├── tools/
│   ├── build_final_report.py
│   ├── build_presentation_practice_guide.py
│   └── README.md
│
├── data/
│   └── README.md
│
├── outputs/
│   └── README.md
│
└── docs/
    ├── Industrial_Surface_Defect_Detection_Final_Report.pdf
    └── Industrial_Surface_Defect_Detection_Presentation_Practice_Guide.docx



## Notebook workflow

Run or review the notebooks in numerical order:

1. `01_MVTec_Tile_Data_Validation_and_Splitting.ipynb` - dataset audit, EDA, leakage checks, and manifests.
2. `02_MVTec_Tile_Baseline_and_Transfer_Learning.ipynb` - original model-development notebook.
3. `02_MVTec_Tile_Baseline_and_Transfer_Learning_working.ipynb` - protected working copy and smoke-test development.
4. `03_MVTec_Tile_Standard_Training.ipynb` - executed baseline CNN and frozen-backbone MobileNetV2 training.
5. `04_MVTec_Tile_Validation_Analysis_and_Threshold_Selection.ipynb` - frozen-model validation analysis.
6. `05_MVTec_Tile_Controlled_Fine_Tuning.ipynb` - smoke test and controlled fine-tuning.
7. `06_MVTec_Tile_Fine_Tuned_Threshold_Recalibration.ipynb` - validation-only threshold calibration.
8. `07_MVTec_Tile_GradCAM_Explainability.ipynb` - Grad-CAM analysis for correct, false-positive, and low-confidence validation examples.
9. `08_MVTec_Tile_Final_Test_Evaluation.ipynb` - locked, one-time final test evaluation.
10. `09_MVTec_Tile_Final_Project_Summary.ipynb` - presentation-ready synthesis of the executed project.


## Reproducibility

The executed environment used Python 3.10, TensorFlow 2.21.0, NumPy 2.2.6, pandas 2.3.3, scikit-learn 1.7.2, Matplotlib 3.10.9, Pillow 12.3.0, and nbformat 5.10.4. A fixed seed of `42` is used throughout.

Create and activate a virtual environment on Windows:

```powershell
py -3.10 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
jupyter notebook
```

ImageNet weights may be downloaded automatically by Keras if they are not already present in the configured Keras cache. Native Windows TensorFlow 2.21 executes this project on CPU; GPU use generally requires WSL2 or another supported environment.

## Interpretation limitations

- The validation and test sets contain few defective examples, so subgroup recall estimates are uncertain.
- The supervised reformulation differs from the original anomaly-detection purpose of MVTec AD.
- The final test contained two false negatives, showing that validation-based safety behavior did not fully generalize.
- Grad-CAM provides coarse gradient-based spatial sensitivity, not a causal explanation.
- The current work is an experimental prototype, not a production inspection system.

## Data source

MVTec AD: P. Bergmann et al., *MVTec AD - A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection*, CVPR 2019.
