## Park2026b-MACH-SMF

Code for *The Stellar Mass Function for Nine Massive Galaxy Clusters in the Local Universe* (Park et al. 2026, ApJ, accepted).

The notebooks here measure the galaxy stellar mass function (SMF) of the nine most massive clusters in the MACH survey (MAssive Cluster survey with Hectospec), from the spectroscopic completeness corrections to the comparison with the SDSS field SMF and with IllustrisTNG-300 clusters.

> **Data availability.** The MACH spectroscopic catalogs and the derived data products belong to the HeCS-omnibus team and are not part of this repository, so the notebooks cannot be run end to end without them. The repository documents how each number and figure in the paper was produced. Every notebook starts with a header that lists its inputs and outputs, and the paper figures are included under `FIGURE/`.

## Directory structure

`CODE/` holds the notebooks, in the order they were run. The `DATA/` folder they read from is not included.

### `CODE/MACH/DATA_ANALYSIS/`: cluster sample and spectroscopic completeness

- `00_MACH_sample_overview.ipynb`: the nine MACH clusters within the HeCS-omnibus sample, the cluster property table, and the number of DESI and NED redshifts in the MACH fields (Figure 1).
- `01_MACH_CMD.ipynb`: red-sequence fit in the colour–magnitude diagram, the linear relation used to predict Dn4000 from g − r for galaxies without a spectrum, and the member fraction above, on and below the red sequence (Figure 5).
- `02_MACH_1Dspec_completeness_analysis.ipynb`: spectroscopic completeness as a function of r magnitude for each cluster within R200 and the magnitude limit that follows from it (Figure 2). The per-cluster limits feed the SMF notebooks.
- `03_MACH_2Dspec_completeness_analysis.ipynb`: maps of the spectroscopic completeness on the sky around each cluster (Figure 3).
- `04_Rv_digaram.ipynb`: radius–velocity diagrams with the caustic envelopes that define membership (Figure 4).

### `CODE/MACH/SMF/`: cluster stellar mass functions

- `00_rawSMF_mass_completeness_limit_1dspec.ipynb`: stellar-mass completeness limit of the spectroscopic member sample, for the stacked sample and per cluster.
- `01_build_SMF_correction_parameters.ipynb`: the table of f_spec and f_mem in cells of (M_r, g − r, R_cl/R200) used to add photometric galaxies back into the SMF (Figure 9).
- `02a_SMF_total_MACH_stacked.ipynb`: completeness-corrected SMF of the stacked sample in a chosen radial range, Monte Carlo membership correction, quiescent/star-forming split, and Schechter fits with `emcee`.
- `02b_SMF_total_per_cluster.ipynb`: the same for each cluster separately. Writes Table 4 and the Schechter parameter table (Figures 10, 11).
- `03_SMF_cluster_vs_field_mass_normalized.ipynb`: cluster and field SMFs normalised by the total mass in each volume (Figure 14).
- `04_SMF_starforming_quiescent_compare.ipynb`: quiescent and star-forming SMFs in three radial bins next to the field SMFs (Figure 15).
- `05_quiescent_fraction_cluster_vs_field.ipynb`: quiescent fraction against stellar mass in the cluster radial bins and in the field (Figure 16).
- `06_SMF_MACH_vs_TNG300.ipynb`: stacked MACH SMF against massive TNG300 haloes at z ≈ 0.07 (Figure 17).
- `07_SMF_evolution.ipynb`: the MACH SMF next to the higher-redshift cluster SMFs of van der Burg et al. (2018, 2020) and the matching TNG300 snapshots.
- `99_SMF_change_check.ipynb`: one-off check made when the master catalog was rebuilt.
- `Table4_MRT.txt`: the machine-readable SMF table of the paper, produced by `02b`. The other tables the notebooks write (`MACH_1dspec_limit.csv`, `MACH_SMF_fspec_fmem_bin.csv`, `SMF_Fit_Params_Table.csv`, `SMF_results/*.npz`) are derived from the proprietary catalogs and are not included.

### `CODE/FIELD/`: field SMF from SDSS

- `00_FieldSMF_total.ipynb`: 1/V_max field SMF from the SDSS Main Galaxy Sample at 0.07 < z < 0.11, with the same CIGALE stellar masses as the clusters.
- `00b_FieldSMF_figure.ipynb`: the field completeness figure (Figure 12).
- `01_FieldSMF_starforming.ipynb`, `01b_FieldSMF_quiescent.ipynb`: the same split by Dn4000.
- `02_FieldSMF_Comparison_and_fq.ipynb`: Schechter fits to the three field SMFs and the field quiescent fraction.

The field SMF tables these notebooks write (`FieldSMF_*.csv`) are not included either.

## Requirements

Python 3.9 or later with Jupyter. The notebooks use

| Package | Version | Used for |
|---|---|---|
| `numpy` | ≥ 1.23 | arrays and binning |
| `pandas` | ≥ 1.5 | catalog tables |
| `scipy` | ≥ 1.9 | `curve_fit`, `stats`, `interp1d`, binned statistics, KDE |
| `matplotlib` | ≥ 3.6 | figures |
| `astropy` | ≥ 5.2 | cosmology (`LambdaCDM`, `Planck15`), `SkyCoord`, units, `astropy.modeling` |
| `emcee` | ≥ 3.1 | MCMC Schechter fits |
| `corner` | ≥ 2.2 | posterior plots |
| `scikit-learn` | ≥ 1.1 | linear regression in the completeness analysis |
| `tqdm` | ≥ 4.64 | progress bars |

```bash
pip install numpy pandas scipy matplotlib astropy emcee corner scikit-learn tqdm
```

or

```bash
conda install numpy pandas scipy matplotlib astropy scikit-learn tqdm
conda install -c conda-forge emcee corner
```

## Citation

If you use this code, please cite

> Park et al. (2026), *The Stellar Mass Function for Nine Massive Galaxy Clusters in the Local Universe*, ApJ, accepted.

Questions about the code or the data can go to `jubee.sohn@snu.ac.kr` or `jongin.park@snu.ac.kr`.
