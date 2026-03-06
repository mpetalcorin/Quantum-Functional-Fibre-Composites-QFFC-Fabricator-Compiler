# Quantum-Functional-Fibre-Composites-QFFC-Fabricator-Compiler
Reproducible digital twin for protein-programmed quantum material fibres, linking manufacturing recipes to defect statistics and quantum-readiness metrics with QC gating, surrogate models, and closed-loop recipe screening.
# Protein-Programmed Quantum Functional Fibre Composites (QFFC)

A reproducible, proof-of-concept “digital twin” for manufacturing **Quantum Functional Fibre Composites (QFFCs)**. The workflow links **recipe setpoints** to **host-fibre defect statistics** (events/m, roughness/scattering proxies) and then to **quantum-relevant readouts** (NV ODMR proxies, single-photon g²(0), erbium memory proxy, lithium niobate EO/loss proxies). It includes QC gating (“quantum-ready”) and surrogate-guided recipe screening to mimic closed-loop optimisation.

This repository is designed for **platform thinking**: replace simulated outputs with experimental metrology later while keeping the same QC and optimisation logic.

## What’s in this repo

### Core notebooks
- `universal_fabricators_qffc_v4.ipynb`  
  End-to-end simulation + analysis for QFFC manufacturing, includes:
  - literature-benchmarked priors (referenced in notebook)
  - simulated recipe → host outputs → quantum outputs
  - distribution plots, correlation heatmap
  - random-forest surrogates with MAE/R²
  - feature importance
  - explicit QC gate for “quantum-ready”
  - surrogate-guided candidate recipe shortlist

### Extension notebooks 
- `universal_fabricators_poc_v3_image_qc.ipynb`  
  Synthetic cross-section microscopy generator + automated image QC loop.

## Installation

### Recommended
- Python 3.10–3.12

## Install dependencies:

```bash
pip install numpy pandas matplotlib scikit-learn
```
## Open:
	•	universal_fabricators_qffc_v4.ipynb

## Execute all cells from top to bottom. The notebook will:
	1.	simulate a QFFC dataset,
	2.	visualise host and quantum metric distributions,
	3.	compute correlation maps,
	4.	train surrogate models,
	5.	define a “quantum-ready” QC gate,
	6.	output top candidate recipes by predicted score.

## Outputs 
The notebook produces:
	•	Figures (in-notebook):
	•	host manufacturing envelope histograms
	•	quantum metrics histograms
	•	correlation heatmap
	•	surrogate feature importance
	•	quantum-ready corridor comparisons
	•	Tables (in-notebook):
	•	priors table
	•	summary statistics table
	•	surrogate model performance table
	•	QC gate definition
	•	top recipe shortlist

## How to adapt this to real experiments
This repo is structured so you can swap simulated values for real measurements:
Replace:
	•	roughness_nm → AFM roughness (nm)
	•	defects_per_m → measured defect events per metre
	•	scattering_au / pressure_kPa → inline metrology streams
	•	nv_odmr_contrast, nv_odmr_linewidth_mhz → ODMR analysis results
	•	g2_0 → measured g²(0)
	•	er_storage_us → memory protocol readout
	•	tfln_vpiL_vcm, insert_loss_db_per_cm → EO + loss measurements

## Keep:
	•	QC gate logic (update thresholds as you learn)
	•	model training and recipe screening pipeline
	•	figure/table reporting structure for manuscripts and proposals

## Reproducibility
	•	The notebooks set fixed random seeds.
	•	All outputs are generated from declared priors and code cells.
	•	No external data downloads are required for the simulation runs.

## Citation
**Petalcorin, M.I.R.** (2026). Protein-Programmed Manufacturing of Quantum Functional Fibre Composites, A Reproducible Quality-Control and Optimisation Framework that Links Recipe Settings to Defect Statistics and Quantum Performance at Scale. https://github.com/mpetalcorin/Quantum-Functional-Fibre-Composites-QFFC-Fabricator-Compiler

## License
MIT
