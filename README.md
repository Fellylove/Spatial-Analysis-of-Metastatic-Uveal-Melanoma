# Spatial Transcriptomics Analysis of Metastatic Uveal Melanoma

## Overview
This repository contains the analysis pipeline and code for spatial transcriptomic profiling of liver metastatic uveal melanoma (UM) and primary retinoblastoma using 10x Visium HD.

## Abstract
Uveal melanoma (UM) metastasizes to the liver in 50% of patients with poor prognosis, yet cellular mechanisms driving liver colonization remain unclear. We performed spatial transcriptomics on liver metastatic UM and primary retinoblastoma to define cell organization and signaling networks. Our analysis reveals EMT-reprogrammed endothelial cells as dominant drivers of immunosuppressive microenvironment, with M2-polarized macrophages and extensive cell-cell communication networks.

## Key Findings
- **M2-dominant macrophage polarization** in metastatic UM (3.6-fold higher vs retinoblastoma, p < 0.001)
- **EMT-reprogrammed endothelial cells** drive immunosuppressive signaling via TGF-β (5.3-fold enrichment)
- **Retinal origin** of endothelial cells confirmed by retinal-specific gene signatures (2.4-fold enrichment)
- **Endothelial-dominated cell-cell communication** via collagen-CD44 and SPP1-CD44 pathways
- **Premetastatic niche establishment** driven by retinal endothelial cells

## Repository Structure
```
.
├── data/                          # Raw and processed data
│   ├── raw/                      # Raw Visium HD data
│   ├── processed/                # Processed Seurat objects
│   └── metadata/                 # Sample metadata
├── scripts/                       # Analysis scripts
│   ├── 01_preprocessing.R        # Quality control and normalization
│   ├── 02_clustering.R           # Cell type identification
│   ├── 03_module_scoring.R       # M1/M2, EMT, retinal scoring
│   ├── 04_differential_expression.R
│   ├── 05_cellchat_analysis.R    # Ligand-receptor interactions
│   └── 06_visualization.R        # Plots and figures
├── results/                       # Output files
│   ├── figures/                  # Publication-quality figures
│   ├── tables/                   # Summary statistics and tables
│   └── cellchat/                 # Cell-cell communication results
├── markers/                       # Gene marker lists
│   ├── macrophage_markers.csv
│   ├── endothelial_markers.csv
│   ├── retinal_markers.csv
│   └── emt_markers.csv
├── environment.yml               # Conda environment
├── requirements.txt              # Python dependencies (if applicable)
└── README.md                     # This file
```

## Methods

### Spatial Transcriptomics
- **Platform**: 10x Genomics Visium HD
- **Pipeline**: SpaceRanger v2.0
- **Samples**: 
  - Liver metastatic uveal melanoma (UM)
  - Primary retinoblastoma (control)

### Computational Analysis
- **Clustering**: Cell-type/state panel approach using Seurat
- **Module Scoring**: 
  - M1/M2 polarization signatures
  - EMT gene signatures (BAP1-deficient UM)
  - Retinal endothelial gene panel
- **Cell-Cell Communication**: CellChat for ligand-receptor interaction analysis
- **Statistical Testing**: Wilcoxon rank-sum test for comparisons

### Identified Cell Populations
- **Cluster 0-2, 4, 5, 6**: Tumor cells
- **Cluster 3**: Macrophages
- **Cluster 7**: Endothelial/Microglia-like cells (retinal origin)
- **Cluster 8**: Monocytes

## Installation

### Requirements
- R >= 4.2.0
- Python >= 3.8 (optional, for additional analyses)

### R Packages
```r
# Core packages
install.packages(c("Seurat", "dplyr", "ggplot2", "tidyverse"))

# Spatial transcriptomics
install.packages("hdf5r")

# Cell-cell communication
devtools::install_github("sqjin/CellChat")

# Additional packages
install.packages(c("pheatmap", "viridis", "patchwork", "RColorBrewer"))
```

### Creating Conda Environment
```bash
conda env create -f environment.yml
conda activate spatial_um
```

## Usage

### 1. Preprocessing and Quality Control
```r
source("scripts/01_preprocessing.R")
```

### 2. Cell Type Identification
```r
source("scripts/02_clustering.R")
```

### 3. Module Score Analysis
```r
# Calculate M1/M2 polarization scores
source("scripts/03_module_scoring.R")
```

### 4. Cell-Cell Communication Analysis
```r
# Run CellChat analysis
source("scripts/05_cellchat_analysis.R")
```

### 5. Generate Figures
```r
source("scripts/06_visualization.R")
```

## Key Results

### M2 Polarization
- All UM clusters showed M2-dominant phenotype
- Mean M2/M1 ratio: 598 (UM) vs 164 (retinoblastoma), p = 0.002

### TGF-β Expression
- Cluster 7 (endothelial) showed highest TGF-β expression (5.3-fold, p < 0.001)
- Drives immunosuppressive microenvironment

### Cell-Cell Communication
- **Dominant pathways**:
  - Endothelial → Tumor/Macrophages: Collagen-CD44 (31 interactions)
  - Macrophages → All cells: SPP1-CD44 (7 interactions)
- CD44 universally expressed as receptor hub

### Retinal Endothelial Origin
- Retinal gene panel enrichment: 2.4-fold (p < 0.001)
- General endothelial panel: 1.3-fold (p < 0.001)
- Suggests retinal endothelial cells migrate and establish premetastatic niche

## Data Availability
- Raw sequencing data: [GEO/SRA accession] (to be submitted)
- Processed Seurat objects: Available upon request
- Cell-cell communication data: `results/cellchat/`

## Citation
If you use this code or data, please cite:
```
[Your name et al.] (2025). Spatial Transcriptomics of Metastatic Uveal Melanoma 
Reveals EMT-Reprogrammed Endothelial Cells Driving an Immunosuppressive 
Microenvironment. [Journal], [Volume]([Issue]), [Pages].
```

## Contributing
This is an ongoing research project. Additional analyses are being added.

## Contact
- **Principal Investigator**: Dr. Gurdeep Singh 
- **Analyst**: Sylvia Burris, Esteban Abeyta
- **Email**: [your.email@institution.edu]
- **Institution**: University of New Mexico

## License
MIT

## Acknowledgments
- 10x Genomics for Visium HD platform
- [Funding sources]
- [Collaborators: Esteban Abeyta, Sylvia Burris, Dr. Gurdeep Singh]

## Changelog
- **2025-01-XX**: Initial analysis pipeline
- **2025-XX-XX**: Added CellChat analysis
- **2025-XX-XX**: Retinal endothelial origin analysis
- [More to come as you add analyses]

---
*Last updated: [Date]*
