# Outputs

This directory contains selected generated artifacts from the project experiments.

## Organization

The project outputs are organized by function and milestone:

```text
outputs/
├── analysis/
│   ├── milestone3/
│   ├── milestone5/
│   ├── milestone6/
│   └── milestone7/
│
├── figures/
│   ├── milestone4/
│   ├── milestone6/
│   └── milestone7/
│
├── models/
│   └── histories/
└── README.md
```

## Important Analysis Files

The final report workflow uses analysis summaries including:

```text
outputs/analysis/milestone3/validation_threshold_selection_summary.json
outputs/analysis/milestone5/fine_tuned_threshold_selection_summary.json
outputs/analysis/milestone6/gradcam_summary.json
outputs/analysis/milestone7/final_test_evaluation_summary.json
```

Selected supporting CSV files are also retained in the milestone folders for validation, threshold, Grad-CAM, and final-test analysis.

## Important Figures

```text
outputs/figures/milestone4/mobilenetv2_finetuned_standard_learning_curves.png
outputs/figures/milestone6/fine_tuned_validation_gradcam_panel.png
outputs/figures/milestone7/final_test_metrics.png
outputs/figures/milestone7/final_test_error_examples.png
```

## What Should Be Uploaded?

Upload **small, meaningful final figures and analysis summaries** that help a reviewer understand the results.

Do not upload:

- the raw MVTec AD dataset
- large or unnecessary model checkpoints
- temporary training files
- Python cache directories
- virtual environments
- large intermediate artifacts unless they are specifically needed to reproduce or understand the project

## GitHub Portfolio Principle

The repository should prioritize:

1. Reproducible notebooks
2. Clear documentation
3. Final evaluation evidence
4. Selected explainability figures
5. Clean supporting scripts

Large generated artifacts should remain local unless they add clear value to the repository.
