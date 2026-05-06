# xNNPCD: an interpretable neural network framework for discovering regulators of programmed cell death from integrative perturbation profiles



## Overview
xNNPCD is an interpretable AI framework designed to decode the regulatory landscape of Programmed Cell Death (PCD). By embedding biological prior knowledge (GO, KEGG, Reactome) into an MLP architecture via a mask matrix, and utilizing an innovative pathway ablation mechanism to refine the mask matrix, xNNPCD dynamically discovers novel gene-pathway associations across apoptosis, autophagy, ferroptosis, necroptosis, and pyroptosis.

## Repository Structure
```text
xNNPCD/
├── notebook/
│   └── main_github.ipynb    # Main pipeline
├── data/                    # Local directory for datasets
├── models/                  # Storage for trained .pth weights
└── results/                 # Storage for obtained mask matrices and queires from ontological databases
```

## Data Availability & Reproducibility

To ensurereproducibility and account for the high-volume nature of the datasets, we categorize the data into three levels:

### 1. Frozen Prior Knowledge (2024 Snapshot)
Public databases (GO, KEGG, Reactome) are subject to frequent updates. To exactly reproduce the results in our paper, we provide the `gene_pcd.csv` in the `data/` directory. The `main_github.ipynb` is configured to use the frozen file directly.

### 2. Processed Datasets (Banquet Format)
Due to the large file size (~GB scale), the pre-processed Banquet datasets are hosted on **Zenodo** to ensure long-term availability and stable access. The `main_github.ipynb` is also configured to use the frozen file directly.
* **Link**: [Download from Zenodo (DOI: 10.5281/zenodo.XXXXX)](#) 
* **Placement**: Download and place the files into the `data/` folder.

### 3. Raw Multi-Omics Data
For users wishing to run the full preprocessing pipeline from scratch:
* **CMap L1000 (Level 5)**: Obtain `*.gctx` and `siginfo` files from the [CLUE.io Data Portal](https://clue.io/data).
* **CRISPR DepMap**: Obtain `CRISPRGeneEffect.csv` and `Model.csv` from the [DepMap Public Release](https://depmap.org/portal/download/).
* **Placement**: All raw files should be stored in `data/raw_data/`.
