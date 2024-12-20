# scRNA-seq Dataset Ingestion and Quality Control Pipeline

## Problem 1: Ingesting and Labeling Public scRNA-seq Datasets

### Task 1: Download and Ingest Datasets
1. **Diseased mice dataset** from GSE180498, including samples with the following IDs:
   - `GSM5463957`
   - `GSM5463958`
   - `GSM5463959`

2. **Control mice dataset** from GSE142541, including samples with the following IDs:
   - `GSM4231663`
   - `GSM4231664`
   - `GSM4231665`
   - `GSM4231666`
   - `GSM4231667`
   - `GSM4231668`

3. **Steps to Ingest**:
   - Use `scanpy` to load the datasets into `AnnData` format.

### Task 2: Add Sample Labels and Cohort Information
- Add two columns to `adata.obs`:
  1. `sample`: Assign unique labels to each sample (e.g., `NODAIRE_1`, `NODAIRE_2`, `NODCTRL_1`, etc.).
  2. `cohort`: Indicate the group of each sample (`NODAIRE`, `SC`, or `NODICAM`).

---

## Problem 2: Visual Inspection and Quality Control (QC) of scRNA-seq Data

### Task 1: Calculate QC Metrics
For each cell in the dataset, compute the following metrics:
- **Total Counts**: Sum of all counts (RNA content) per cell.
- **Number of Genes Detected**: Count of unique genes with non-zero expression per cell.
- **Percentage of Mitochondrial Genes**: Percentage of mitochondrial counts relative to total counts.

### Task 2: Visual Inspection
Create the following visualizations:
- **Distribution of Total Counts per Cell**: Visualize the RNA content distribution.
- **Number of Genes Detected per Cell**: Assess cell complexity.
- **Percentage of Mitochondrial Genes per Cell**: Identify cells with high mitochondrial content.

### Visualization Guidelines
Use the generated plots to:
- Select thresholds for filtering low-quality cells.
- Exclude overrepresented cells.
- Remove cells with high mitochondrial content.

---

