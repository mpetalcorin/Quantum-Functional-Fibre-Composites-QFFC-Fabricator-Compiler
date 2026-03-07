# Data Sheet QFFC Synthetic Dataset (Recipe  Defects  Quantum Metrics)

## Motivation
This dataset exists to:
- Prototype an end-to-end manufacturing QC workflow for QFFCs.
- Stress-test a closed-loop optimisation pipeline before experimental data exists.
- Provide a reproducible baseline for figure/table generation in manuscripts and proposals.

It is **not** intended as a physically accurate dataset.

## Composition
Each row represents one simulated manufacturing run (recipe) with:
1) controllable setpoints (inputs),
2) latent drivers and host outputs (defects, roughness/scattering proxies),
3) simulated quantum readouts (NV ODMR proxies, g(0), Er memory proxy, EO/loss proxies),
4) a composite score (`qffc_score`),
5) an explicit QC label (`quantum_ready`) derived from a threshold gate.

## Data generation process
Generated entirely within `universal_fabricators_qffc_v4.ipynb` using:
- fixed random seeds,
- declared numeric priors for baseline quantum regimes,
- smooth nonlinear transforms (e.g., sigmoid/log) to create regime transitions,
- clamping to keep values in plausible ranges.

No external files are required.

## Data fields

### A) Controllable recipe setpoints
- `pH`
- `ionic_mM`
- `temp_C`
- `silica_precursor_mM`
- `residence_s`
- `draw_speed_m_per_min`
- `tension_proxy`
- `mixing_quality`
- `scaffold_robustness`

### B) Latent drivers
- `ss_proxy` (supersaturation proxy)
- `shear_proxy`
- `collapse_risk`

### C) Host outputs and QC proxies
- `lumen_um`
- `wall_um`
- `geom_cv_pct`
- `pressure_kPa` (fouling/clogging proxy)
- `scattering_au` (bulk precipitation/roughness proxy)
- `defects_per_m` (events/m)
- `roughness_nm` (proxy)

### D) Quantum metrics (simulated)
- `nv_odmr_contrast`
- `nv_odmr_linewidth_mhz`
- `g2_0`
- `er_storage_us`
- `tfln_vpiL_vcm`
- `insert_loss_db_per_cm`

### E) Composite score and QC gate
- `qffc_score` (weighted composite)
- `quantum_ready` (0/1 derived from threshold gate)

## Preprocessing / cleaning
None beyond:
- clamping outputs to plausible numeric ranges,
- deterministic generation from a fixed seed.

## Uses
### Appropriate uses
- Demonstrating QC gating, defect taxonomies, and recipe screening logic.
- Training toy surrogates to explore process leverage.
- Generating figures/tables for proposals and manuscripts describing the platform concept.

### Inappropriate uses
- Predicting real quantum device performance.
- Comparing directly to experimental data without calibration.
- Any engineering decision-making without experimental validation.

## Distribution and maintenance
- Dataset is generated on-demand by running the notebook.
- Version changes should be tracked by:
  - notebook version tag (e.g., v4),
  - seed values,
  - declared priors,
  - and any modifications to mapping functions.

## Known limitations
- Mechanistic relationships are synthetic and simplified.
- Quantum readiness is heuristic and should be recalibrated for any real system.
- Domain shift from simulation to experiment is not modelled.

## Recommended experimental mapping (future)
When experimental data exists, replace proxies as follows:
- `roughness_nm`  AFM roughness (nm)
- `defects_per_m`  counted defects per metre from imaging/in-line event logs
- `scattering_au`, `pressure_kPa`  real inline optical scattering/pressure
- `nv_odmr_*`  ODMR spectral fits
- `g2_0`  photon correlation measurement
- `er_storage_us`  memory protocol outcome
- `tfln_vpiL_vcm`, `insert_loss_db_per_cm`  EO + propagation loss measurements
