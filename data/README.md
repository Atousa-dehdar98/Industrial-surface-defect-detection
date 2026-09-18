# Dataset

This project uses the **Tile** category of the MVTec AD (MVTec Anomaly Detection) dataset.

## Local Dataset Structure

The expected local structure is:

```text
data/
└── raw/
    └── mvtec_ad/
        └── tile/
```

The raw dataset is intentionally **not committed to GitHub**.

Obtain the dataset from the official MVTec source and place the Tile data in the directory above.

Official dataset page:

https://www.mvtec.com/research-teaching/datasets/mvtec-ad

## Project Formulation

MVTec AD was originally designed for unsupervised anomaly detection. In this project, the Tile category was intentionally reformulated as a **supervised binary classification** task.

The two operational classes are:

- **Good** — non-defective tile
- **Defective** — tile containing a surface defect

## Dataset Split

| Split | Total | Good | Defective |
|---|---:|---:|---:|
| Train | 242 | 184 | 58 |
| Validation | 54 | 40 | 14 |
| Test | 51 | 39 | 12 |

The split was created at the original-image level using seed `42`.

## Leakage Prevention

The project checks group identifiers and SHA-256 hashes to reduce the risk of identical images appearing in multiple splits.

Data augmentation is applied only to the training pipeline. Validation and test images are not augmented.

## Reproducibility

For the complete preparation and splitting workflow, see:

`notebooks/01_MVTec_Tile_Data_Validation_and_Splitting.ipynb`

## Important

Do **not** upload the raw MVTec AD dataset to this repository. The repository should contain this documentation rather than the full image dataset.
