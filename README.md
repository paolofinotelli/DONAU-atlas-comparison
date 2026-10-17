# DONAU: structural and functional connectome analysis across brain parcellations

Analysis code accompanying the paper:

> **No Single Atlas Fits All: Parcellation Choice Shapes Structural and Functional Connectome Analyses in Mild Cognitive Impairment**
> *(working title; authors, journal and DOI to be added)*

The code extracts nodal graph metrics from structural (SC) and functional (FC)
connectivity matrices, compares them across three parcellations (Desikan,
Schaefer, Glasser), and tests for differences between cognitively normal (CN)
participants and participants with mild cognitive impairment (MCI) in the
ADNI cohort.

## Repository structure

```
.
├── FC/    # functional connectivity pipeline  (see FC/README.md)
├── SC/    # structural connectivity pipeline  (see SC/README.md)
├── CITATION.cff
├── LICENSE
└── README.md
```

The two pipelines are independent but deliberately parallel: they use the same
nodal metrics, the same statistical procedures and the same script numbering.

| Step | FC | SC | What it does |
|---|---|---|---|
| 1 | `01a_…`, `01b_…` | `01_…` | Nodal graph metrics (strength, weighted clustering coefficient, betweenness and closeness centrality) |
| 2 | `02_compare_atlases.py` | `02_compare_atlases.py` | Metric distributions, KS tests, Friedman + post-hoc Wilcoxon (atlas comparison) |
| 3 | `03_report_boxplot_values.py` | `03_report_boxplot_values.py` | Numerical values behind the aggregate boxplots |
| 4 | `04_group_comparison_CN_vs_MCI.py` | `04_group_comparison_CN_vs_MCI.py` | Node-wise CN vs MCI comparison (Mann-Whitney U, FDR, Cohen's d) |

The analyses reported in the paper use the subjects present in **both** the SC
and FC datasets (output files suffixed `_shared_FC-SC`). Each script therefore
accepts a `--subset-dir` pointing to the other modality's data. Details and
full usage are in the README of each folder.

## Installation

Python 3.9 or later is recommended.

```bash
git clone https://github.com/<OWNER>/donau-connectivity-analysis.git
cd donau-connectivity-analysis

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r FC/requirements.txt   # FC pipeline (includes h5py for MATLAB v7.3 files)
pip install -r SC/requirements.txt   # SC pipeline
```

## Data

The analyses use data from the Alzheimer's Disease Neuroimaging Initiative
(ADNI). **ADNI data cannot be redistributed and are not included in this
repository.** To reproduce the results, request access at
https://adni.loni.usc.edu, then generate the connectivity matrices as described
in the paper. Expected folder layouts are documented in `FC/README.md` and
`SC/README.md`.

## Reproducing the paper

1. Obtain ADNI data and build the SC and FC inputs (see the paper).
2. Run the SC pipeline (`01` → `02` → `04`), then the FC pipeline, giving each
   the other's data folder as `--subset-dir`.
3. Script `03` can be run at any point after step `01` to print the values
   behind the boxplots.

The scripts are provided exactly as used for the analyses in the paper. The
version matching the paper is tagged in the GitHub releases.

## How to cite

Please cite the paper above and, for the code itself, the archived release
(DOI to be added after the first Zenodo release). GitHub's "Cite this
repository" button uses `CITATION.cff`.

## Acknowledgements

This work was supported by the French National Research Agency (ANR) under
grant ANR-24-JPWG-0002 (DONAU project).  

Data used in this work were obtained from the Alzheimer's Disease Neuroimaging
Initiative (ADNI) database (adni.loni.usc.edu). ADNI investigators contributed
to the design and implementation of ADNI and/or provided data but did not
participate in the analysis or writing of this work. Please check the current
ADNI data use agreement for the exact acknowledgement text required.

## License

Code released under the MIT License (see `LICENSE`).

## Contact

DONAU project coordinator: *Paolo Finotelli, paolo.finotelli@unicaen.fr ; paolo.finotelli@polimi.it*.
Code author: *Valentina Bordin, valentina.bordin@polimi.it*.
