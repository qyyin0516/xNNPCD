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

To ensure reproducibility and account for the high-volume nature of the datasets, we categorize the data into three levels:

### 1. Frozen Prior Knowledge 
Public databases (GO, KEGG, Reactome) are subject to frequent updates. To exactly reproduce the results in our paper, we provide the `gene_pcd.csv` in the `data/` directory (a frozen 2024 snapshot). The `main_github.ipynb` is configured to use this frozen file directly.

### 2. Processed Datasets (Banquet Format)
Due to the large file size (~GB scale), the pre-processed Banquet datasets and corresponding sample information (for both CRISPR-Cas9 knockout and drug response) are hosted on Zenodo to ensure long-term availability and stable access. The `main_github.ipynb` is explicitly designed to load these processed files, bypassing heavy memory requirements.
* **Link**: Download from [Zenodo](https://doi.org/10.5281/zenodo.7829597).
* **Placement**: Download and place all extracted files (the Banquet matrices and the metadata) directly into the `data/` folder.

### 3. Raw Data Provenance
For simplicity and rapid execution, the heavy raw data preprocessing (which requires extensive metadata matching and large-scale matrix manipulation) has been omitted from this streamlined repository. For full academic transparency, our processed Banquet datasets were originally derived from:
* **CMap L1000 (LINCS 2020 Release)**: Sourced from the [CLUE.io Data Portal](https://clue.io/data/CMap2020#LINCS2020). This includes the core `.gctx` matrices (`level5_beta_trt_xpr_n142901x12328.gctx` for CRISPR, `level5_beta_trt_cp_n720216x12328.gctx` for drug response), along with their corresponding metadata annotations (e.g., `siginfo`, `cellinfo`).
* **CRISPR DepMap**: Sourced from the [DepMap Public 24Q2 Release](https://depmap.org/portal/download/). This includes the cell fitness dependency scores (`CRISPRGeneEffect.csv`) and cell line metadata (`Model.csv`).

## Environment Setup & Quick Start

To guarantee exact reproducibility, we have locked the package versions to our verified development environment. 

**Tested Environment:**
* **Python**: 3.11.9
* **OS**: Cross-platform compatible (Tested on Linux/macOS)


**Installation Steps:**
We highly recommend using a virtual environment (e.g., `conda` or `venv`) to avoid conflicts with your local packages.

```bash
# 1. Clone the repository
git clone [https://github.com/qyyin0516/xNNPCD.git](https://github.com/qyyin0516/xNNPCD.git)
cd xNNPCD

# 2. Create and activate a virtual environment (Conda example)
conda create -n xnnpcd_env python=3.11.9 -y
conda activate xnnpcd_env

# 3. Install the exact dependencies
pip install numpy==1.26.4 pandas==2.2.3 requests==2.32.3 mygene==3.2.2 \
            biomart==0.9.2 biopython==1.84 cmapPy==4.0.1 \
            matplotlib==3.10.0 seaborn==0.13.2 scipy==1.11.2 \
            scikit-learn==1.6.1 torch==2.6.0+cpu
```
Note: If you are running this on a machine with a CUDA-enabled GPU, you may omit the +cpu tag for PyTorch to enable hardware acceleration.

## Execution Flow

This repository is designed as a streamlined, "click-and-play" Jupyter Notebook. Once the data is placed in the `data/` folder and the environment is set up, simply run `notebook/main_github.ipynb` sequentially. 

The notebook executes the following pipeline:

1. **Initialization**: Loads the frozen prior knowledge (`gene_pcd.csv`) and processed Banquet matrices. It also sets up the device (CPU/GPU) and random seeds for reproducibility.
2. **Model Instantiation**: Builds the `MaskedMLP_Regression` network architecture. The first layer is automatically constrained by the mask matrix derived from the biological priors.
3. **Training & Ablation**: Iteratively trains the network using pre-determined optimal hyperparameters and then applies the pathway ablation mechanism to uncover novel gene-pathway associations.
4. **Comprehensive Analysis**: Conducts a comprehensive analysis to rigorously validate the xNNPCD framework.
