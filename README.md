# Physics-Guided Reconstruction of Frequency-Dependent Electrical Characteristics

This repository hosts a single archive:

- [`CeO2_Manuscript_Complete_Reproducibility_Package_.zip`](./CeO2_Manuscript_Complete_Reproducibility_Package_.zip)

The documentation below is based on direct inspection of that ZIP file and only describes files that are actually present.

## Confirmed package structure (inside the ZIP)

After extraction, the package root is:

- `CeO2_Reproducibility_Package/`

Confirmed top-level contents:

- `CeO2_Reproducibility_Package/README.md`
- `CeO2_Reproducibility_Package/00_README/README.md`
- `CeO2_Reproducibility_Package/00_README/FILE_INVENTORY.csv`
- `CeO2_Reproducibility_Package/02_Raw_Data/`
  - `corrected_1MHz_cached_values.csv`
  - `corrected_1MHz_reference.csv`
  - `experimental_cv_gv_long.csv`
  - `experimental_nss_reference.csv`
  - `hill_coleman_nss_reference_metrics.csv`
  - `main_sheet_cached_values.csv`
- `CeO2_Reproducibility_Package/03_Python_Code/`
  - `current_reproduction/`
    - `run_all.py`
    - `run_sparse_reconstruction.py`
    - `recompute_metrics_from_predictions.py`
    - `verify_manuscript_numbers.py`
    - `regenerate_numerical_figures.py`
  - `legacy_public_code/`
    - `README.md`, `ENVIRONMENT.md`, `requirements.txt`, `pytest.ini`
    - `src/` (including `physics.py`, `data_loader.py`, `lofo.py`, `metrics.py`, `models/`)
    - `scripts/` (01/02/03/05/07/09/10/11 workflow scripts + `scripts/README.md`)
    - `tests/` (`test_data.py`, `test_physics.py`)
- `CeO2_Reproducibility_Package/04_Analysis_Data/`
  - `LOFO/`, `Sparse_Grid/`, `Derived_Rs_Gp_Nss/`, `Analytical_Baseline/`, `Nss_Sensitivity/`, `Physical_Consistency/`, `Repeated_Seeds/`
- `CeO2_Reproducibility_Package/05_Tables/`
  - `CSV/` (e.g., `Table1.csv` ... `Table6a.csv`, `Table6b.csv`, `TableS1.csv`, `TableS2.csv`)
  - `Excel/` (e.g., `Table1.xlsx` ... `Table6.xlsx`, `TableS1.xlsx`, `TableS2.xlsx`)
- `CeO2_Reproducibility_Package/06_Figures/`
  - `Images/Figure01_FINAL.png` ... `Figure11_FINAL.png`
  - `Excel_Data/` (`Figure01_Schematic_Metadata.xlsx`, `Figure02_Schematic_Metadata.xlsx`, `Figure03_Schematic_Metadata.xlsx`, `Figure06_Data.xlsx`, `Figure07_Data.xlsx`, `Figure08_Data.xlsx`, `Figure09_Data.xlsx`, `Figure10_Data.xlsx`, `Figure11_Data.xlsx`)
- `CeO2_Reproducibility_Package/07_Environment/`
  - `requirements.txt`
  - `environment_notes.txt`
- `CeO2_Reproducibility_Package/08_Checksums/SHA256SUMS.txt`

## Purpose of included materials

- **Raw measurements**: `02_Raw_Data/`
- **Python reproduction code**:
  - `03_Python_Code/current_reproduction/` (current rerun/audit scripts)
  - `03_Python_Code/legacy_public_code/` (earlier implementation with tests)
- **Processed and analysis outputs**: `04_Analysis_Data/`
- **Manuscript tables and figure assets**: `05_Tables/`, `06_Figures/`
- **Environment and integrity metadata**: `07_Environment/`, `08_Checksums/`, `00_README/`

## Prerequisites and dependencies (confirmed)

From `07_Environment/environment_notes.txt`:

- Recommended: **Python 3.11+**

From `07_Environment/requirements.txt`:

- `numpy`
- `pandas`
- `scipy`
- `scikit-learn`
- `xgboost`
- `matplotlib`
- `python-docx`
- `torch`

Additional pinned legacy environment is listed in:

- `03_Python_Code/legacy_public_code/requirements.txt`
- `03_Python_Code/legacy_public_code/ENVIRONMENT.md`

## Reproducibility

### 1) Extract the archive

From repository root:

```bash
unzip CeO2_Manuscript_Complete_Reproducibility_Package_.zip
cd CeO2_Reproducibility_Package
```

### 2) Install dependencies for current reproduction scripts

```bash
python -m pip install -r 07_Environment/requirements.txt
```

### 3) Run the current reproduction workflow

```bash
python 03_Python_Code/current_reproduction/run_all.py
```

Equivalent step-by-step commands:

```bash
python 03_Python_Code/current_reproduction/run_sparse_reconstruction.py
python 03_Python_Code/current_reproduction/recompute_metrics_from_predictions.py
python 03_Python_Code/current_reproduction/verify_manuscript_numbers.py
python 03_Python_Code/current_reproduction/regenerate_numerical_figures.py
```

### 4) Optional fast numerical audit (no retraining)

```bash
python 03_Python_Code/current_reproduction/recompute_metrics_from_predictions.py
python 03_Python_Code/current_reproduction/verify_manuscript_numbers.py
```

### 5) Optional file-integrity check

```bash
cd CeO2_Reproducibility_Package
sha256sum -c 08_Checksums/SHA256SUMS.txt
```

## Expected outputs (evident from files/scripts)

- Precomputed analysis CSV outputs already included under `04_Analysis_Data/`.
- Final manuscript figure PNGs already included under `06_Figures/Images/`.
- Table CSV/XLSX files already included under `05_Tables/`.
- Running the current reproduction scripts creates `09_Recalculated/` (generated outputs), including:
  - `rerun_sparse_primary_predictions.csv`
  - `recalculated_sparse_primary_summary.csv`
  - `recalculated_lofo_region_summary.csv`
  - `recalculated_Table5_Rs.csv`
  - `recalculated_Table5_Gp_over_omega.csv`
  - `recalculated_Nss_metrics.csv`
  - `figures/Figure8_C_R2_mean.png`, `Figure8_C_NRMSE_mean_pct.png`, `Figure8_G_R2_mean.png`, `Figure8_G_NRMSE_mean_pct.png`, `Figure11_Nss.png`

## Confirmed limitations / cannot be determined from the current ZIP

- No Jupyter notebooks (`.ipynb`) are present.
- `08_Checksums/SHA256SUMS.txt` and `00_README/FILE_INVENTORY.csv` reference files such as:
  - `01_Manuscript/Manuscript_FINAL_checked.docx`
  - `05_Tables/Word/TableS1.docx`
  - `05_Tables/Word/TableS2.docx`
  These paths are referenced by metadata files but are **not present** in the inspected ZIP contents.
- `03_Python_Code/legacy_public_code/src/config.py` points to a local `data/` layout (`data/raw`, `data/processed`) that is not present under `legacy_public_code/`, so a fully validated end-to-end legacy rerun cannot be confirmed from archive contents alone.

## Academic Citation

If you use this repository or package contents in academic work, cite both the manuscript and this repository.

### Manuscript citation (placeholder)

```text
Author(s). (Year). Physics-Guided Reconstruction of Frequency-Dependent Electrical Characteristics for Reliable Interface-State Density Extraction in CeO₂ Nanoparticle-Doped Graphene Quantum Dot Devices. Journal, volume(issue), pages. DOI.
```

### Repository citation

```text
Tuğrul Mert Orhan. (2026). Ce-GQDs2026_10_12: Physics-Guided Reconstruction of Frequency-Dependent Electrical Characteristics [Reproducibility package]. GitHub. https://github.com/PhoenixMert/Ce-GQDs2026_10_12
```

Update the placeholders with the final publication DOI and archival version when available.

## License and Usage Terms

No formal open-source license file is currently present in this repository. Until explicit licensing is added, treat contents as **all rights reserved**.

- Permitted: personal inspection and scholarly evaluation.
- Not automatically permitted: redistribution, relicensing, or commercial reuse.
- Academic reuse should include appropriate citation.

When formal license information becomes available, this section should be updated accordingly.
