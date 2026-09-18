# Tools

This directory contains supporting Python scripts used to generate project documentation.

## Files

### `build_final_report.py`

Generates the final project report in DOCX format.

The script reads selected project outputs from the `outputs/` directory, including validation threshold summaries, fine-tuning results, Grad-CAM summaries, final test evaluation results, and project figures.

It expects the project root to have the following relevant paths:

```text
outputs/
├── analysis/
│   ├── milestone3/
│   ├── milestone5/
│   ├── milestone6/
│   └── milestone7/
└── figures/
    ├── milestone4/
    ├── milestone6/
    └── milestone7/
```

### `build_presentation_practice_guide.py`

Generates the presentation practice guide for the final project presentation.

The guide contains the slide-by-slide English script, Persian coaching notes, cue cards, suggested answers to likely questions, and a shortened five-minute version.

## Dependencies

The scripts use `python-docx` and standard Python libraries.

The main project dependencies are documented in:

```text
requirements.txt
```

## Usage

Run the scripts from the project root so that relative paths resolve correctly.

Example:

```powershell
python tools/build_final_report.py
python tools/build_presentation_practice_guide.py
```

## Note

These scripts are documentation-generation utilities. They are not required for running the trained model or reviewing the notebooks.
