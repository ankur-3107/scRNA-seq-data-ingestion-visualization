# RNA-seq Analysis: Bulk vs. Single-Cell RNA-seq

## Overview
RNA-seq is a genomic method for detecting and analyzing messenger RNA in biological samples. Bulk RNA-seq measures average gene expression across a population, while scRNA-seq studies individual cells, uncovering rare populations and regulatory relationships.

## Requirements
- `anndata`
- `scanpy`
- `pandas`
- `scipy.io`
- `scipy.sparse`
- `seaborn`

## Methodology

### 1. Data Ingestion
- **Diseased Dataset (GSE180498)**: Contains one integrated counts CSV for 3 samples. Data was transposed and converted to AnnData, assigning barcodes as `obs_names` and genes as `var_names`.
- **Control Dataset (GSE142541)**: Features, barcodes, and matrix files were loaded. After transposing, the data was converted to AnnData, assigning gene names to `var_names` and barcodes to `obs_names`. Only the first six samples (based on barcode suffix `...-6`) were used.

### 2. Sample Labeling
- **Control Data**: Samples were identified from barcodes (`...-1` to `...-6`) and labeled based on dataset information in `sample` and `cohort` columns.
- **Diseased Data**: Samples (`R1`, `R2`, `R3`) were identified from barcode suffixes and labeled in `sample` and `cohort`.

### 3. Quality Control (QC) Metrics
- **Metrics Calculated**:
  - Total Counts (sum of RNA counts per cell)
  - Number of Genes Detected (non-zero gene expression values)
  - Percentage of Mitochondrial Genes (`mt-` prefix genes).
- **Methods**:
  - Custom code to calculate metrics.
  - `scanpy`’s `calculate_qc_metrics` function.

### 4. Visual Inspection
- **Plots Generated**:
  - Violin plots for total counts, number of genes detected, and percentage of mitochondrial genes (`sc.pl.violin`).
  - Scatter plots for QC metrics.

### 5. Data Filtration
- Thresholds were set for the total number of genes and percentage of mitochondrial genes to remove:
  - Low-quality cells.
  - Overrepresented cells.
  - Cells with high mitochondrial content.

### 6. Doublet Detection
- Doublets were identified using `sc.pp.scrublet` with `sample` as the batch key.

---
