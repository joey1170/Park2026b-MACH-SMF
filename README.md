## Park2026b-MACH-SMF

**The Stellar Mass Function for Nine Massive Galaxy Clusters in the Local Universe**

This repository provides the **full analysis codebase** used to measure the galaxy stellar mass function (SMF) of the nine most massive galaxy clusters in the local universe, using the MACH (MAssive Cluster survey with Hectospec) spectroscopic dataset. The code covers the complete analysis pipeline: from spectroscopic completeness corrections and SMF construction, to comparisons with the field SMF (SDSS) and IllustrisTNG-300 simulations.

> **Note on data availability:** The underlying MACH spectroscopic catalogs and derived data products are **proprietary to HeCS-omnibus team** and are not publicly released in this repository. As a result, the notebooks cannot be run end-to-end without access to the original data. This repository is shared in the spirit of **methodological transparency** — to document exactly how the analysis was performed, support reproducibility of the logic and approach, and serve as a resource for researchers undertaking similar studies of galaxy stellar mass functions in dense environments.

---

## Purpose of This Repository

- **Paper transparency & credibility**: Every step of the analysis — from completeness estimation to Schechter function fitting — is documented in self-contained notebooks, providing a clear audit trail for the results presented in Park et al. (2026).
- **Resource for the community**: Researchers working on cluster or field SMFs can adapt the methodology, correction schemes, and comparison frameworks to their own datasets.
- **Analysis portfolio**: The notebooks illustrate the full workflow of a spectroscopy-based SMF analysis in a dense cluster environment, including handling of spectroscopic incompleteness, stellar mass completeness limits, and environment-dependent quenching comparisons.

---

## Directory Structure

- **`CODE/`** – Jupyter notebooks and derived numerical products for the full analysis pipeline

  - **`MACH/DATA_ANALYSIS/`** – Cluster sample characterization and spectroscopic completeness
    - `00_MACH_sample_overview.ipynb`: Summary of the nine MACH clusters, their physical properties, and the overall sample selection.
    - `01_MACH_CMD.ipynb`: Color–magnitude diagram (CMD) construction and color cuts used to separate cluster members from field interlopers.
    - `02_MACH_1Dspec_completeness_analysis.ipynb`: 1D spectroscopic completeness analysis — targeting strategy, magnitude dependence, and correction functions.
    - `03_MACH_2Dspec_completeness_analysis.ipynb`: 2D (spatial) spectroscopic completeness maps and corrections across the cluster field.
    - `04_Rv_digaram.ipynb`: Radius–velocity (R–v) phase-space diagrams for visualizing cluster dynamics and confirming membership boundaries.

  - **`MACH/SMF/`** – Cluster stellar mass function construction and analysis
    - `00_rawSMF_mass_completeness_limit_1dspec.ipynb`: Determination of stellar mass completeness limits from the 1D spectroscopy and construction of the raw (uncorrected) SMFs.
    - `01_build_SMF_correction_parameters.ipynb`: Derivation of all correction parameters (spectroscopic completeness, membership completeness, volume normalization) applied to the final SMFs.
    - `02a_SMF_total_MACH_stacked.ipynb`: Construction of the **stacked cluster SMF** across all nine MACH clusters, including normalization and uncertainty estimation.
    - `02b_SMF_total_per_cluster.ipynb`: Individual cluster SMFs and analysis of cluster-to-cluster variation.
    - `03_SMF_cluster_vs_field_mass_normalized.ipynb`: Mass-normalized quantitative comparison between the cluster and field (SDSS) SMFs.
    - `04_SMF_starforming_quiescent_compare.ipynb`: Decomposition of the SMF into star-forming and quiescent components and their dependence on cluster-centric radius.
    - `05_quiescent_fraction_cluster_vs_field.ipynb`: Quiescent galaxy fractions as a function of stellar mass and environment (cluster vs. field).
    - `06_SMF_MACH_vs_TNG300.ipynb`: Direct comparison of the observed MACH cluster SMFs with IllustrisTNG-300 simulated cluster SMFs.
    - `07_SMF_evolution.ipynb`: Supporting analyses for the discussion of SMF evolution across redshift and environments.
    - **Derived data files**: `SMF_Fit_Params_Table.csv`, `MACH_SMF_fspec_fmem_bin.csv`, `MACH_1dspec_limit.csv`, `Table4_MRT.txt` — numerical results (Schechter fit parameters, completeness values, mass limits) used directly in the paper tables and figures.

  - **`FIELD/`** – Field SMF from SDSS for environmental comparison
    - `00_FieldSMF_total.ipynb`: Total field SMF construction from SDSS spectroscopy over the same redshift range as the MACH clusters.
    - `00b_FieldSMF_figure.ipynb`: Publication-quality figures for the field SMF.
    - `01_FieldSMF_starforming.ipynb`, `01b_FieldSMF_quiescent.ipynb`: Field SMFs separated by star-forming and quiescent classifications.
    - `02_FieldSMF_Comparison_and_fq.ipynb`: Quantitative cluster–field SMF comparison and quiescent fraction analysis.
    - **Derived data files**: `FieldSMF_total.csv`, `FieldSMF_starforming.csv`, `FieldSMF_quiescent.csv`, `FieldSMF_fq_Dn4000.csv` — tabulated field SMFs and quiescent fractions.

---

## Computational Environment

- **Python**: 3.x (a recent 3.9+ release recommended)
- **Environment**: Jupyter Notebook / JupyterLab

### Python Package Dependencies

The following third-party packages are required. All are available via `pip` or `conda`.

| Package | Version guidance | Role in this analysis |
|---|---|---|
| `numpy` | ≥ 1.23 | Array operations, binning, numerical computations throughout |
| `pandas` | ≥ 1.5 | Loading and manipulating catalog tables and derived data products |
| `scipy` | ≥ 1.9 | Curve fitting (`curve_fit`), statistical tests (`stats`), interpolation (`interp1d`), 2D binned statistics, KDE estimation |
| `matplotlib` | ≥ 3.6 | All publication-quality figures |
| `astropy` | ≥ 5.2 | Cosmological calculations (`LambdaCDM`, `Planck15`), sky coordinates (`SkyCoord`), unit handling, model fitting (`astropy.modeling`), and table I/O |
| `emcee` | ≥ 3.1 | MCMC ensemble sampler for Schechter function parameter estimation and posterior sampling |
| `corner` | ≥ 2.2 | Corner plots for visualizing MCMC posterior distributions |
| `scikit-learn` | ≥ 1.1 | Linear regression utilities used in completeness and correction analyses |
| `tqdm` | ≥ 4.64 | Progress bars for iterative computations |

Install all dependencies at once:

```bash
pip install numpy pandas scipy matplotlib astropy emcee corner scikit-learn tqdm
```

or with conda:

```bash
conda install numpy pandas scipy matplotlib astropy scikit-learn tqdm
conda install -c conda-forge emcee corner
```

---

## Citation

If this repository or the methods documented here are useful for your work, please cite:

> **Park et al. (2026)**, *"The Stellar Mass Function for Nine Massive Galaxy Clusters in the Local Universe"*, ApJ, accepted.

For questions, methodological discussions, or collaboration inquiries, please contact the corresponding authors at `jubee.sohn@snu.ac.kr` and `jongin.park@snu.ac.kr`.
