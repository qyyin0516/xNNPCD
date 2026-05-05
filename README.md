# xNNPCD: an interpretable neural network framework for discovering regulators of programmed cell death from integrative perturbation profiles



## Overview
xNNPCD is an interpretable AI framework designed to decode the regulatory landscape of Programmed Cell Death (PCD). By embedding biological prior knowledge (GO, KEGG, Reactome) into an MLP architecture via a mask matrix, and utilizing an innovative pathway ablation mechanism to refine the mask matrix, xNNPCD dynamically discovers novel gene-pathway associations across apoptosis, autophagy, ferroptosis, necroptosis, and pyroptosis.

## Data Availability
You can download CMap L1000 (`.gctx`) from [CLUE.io](https://clue.io/data) and DepMap CRISPR data from [DepMap](https://depmap.org/portal/download/), and place them in `data/`.
