# MAGIC

This repository provides the analysis pipeline for the **clozapine dose-response** mouse brain dataset using the MAGIC framework introduced in the manuscript: **Super Resolved Single-cell Spatial Metabobarcoding and Metabotyping for Unlimited Chemical Maps**

---

## 📁 Contents

| File                               | Description                                                     |
|------------------------------------|-----------------------------------------------------------------|
| `maldi_ihc_gsr.ipynb`              | Super-resolves MALDI-IHC protein marker channels               |
| `cell_phenotyping.ipynb`           | Segments cells and assigns phenotypes using super-resolved data |
| `lowres_metabolic_barcoding.ipynb` | Learns metabolic barcodes from low-resolution lipid features    |
| `lipid_gsr.ipynb`                  | Applies GSR to key lipidomic MSI channels                       |
| `superres_metabolic_barcoding.ipynb` | Refines metabolic barcodes using GSR-enhanced features        |

---

## 🖥️ 1. System Requirements

- **Operating Systems:** Windows 10/11, Ubuntu 20.04/22.04 (macOS not tested)
- **Python Version:** 3.8 to 3.11
- **Memory:** ≥16 GB RAM (≥32 GB recommended for large runs)
- **GPU (optional):** CUDA-compatible GPU recommended for faster GSR training/inference

### 📦 Required Dependencies

Install dependencies with:

```bash
pip install -r requirements.txt
```

**Core packages include:**

- `torch`, `torchvision`, `torch_geometric`
- `scanpy`, `anndata`, `scikit-learn`, `umap-learn`
- `matplotlib`, `seaborn`, `pandas`, `numpy`
- `opencv-python`, `tifffile`

> ✅ Tested on:  
> • Python 3.10  
> • PyTorch 2.0.1 + CUDA 11.7  
> • Windows 11 and Ubuntu 22.04

---

## ⚙️ 2. Installation Guide

1. **Clone the repository:**

```bash
git clone https://github.com/coskunlab/MAGIC-Metabotyping-and-Advanced-Graphical-Imaging-of-Chemicals.git
cd MAGIC-Metabotyping-and-Advanced-Graphical-Imaging-of-Chemicals
```

2. **(Optional) Create a new virtual environment:**

```bash
conda create -n magic python=3.10
conda activate magic
```

3. **Install Python dependencies:**

```bash
pip install -r requirements.txt
```

4. **(Optional GPU Support):** Install PyTorch with CUDA:

```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu117
```

---

## 🧪 3. Demo

### ▶️ Demo on small simulated dataset

Use the `demo_data_clozapine/` directory (not included here) or subset your own data for testing.

#### Step-by-Step

1. **Super-resolve MALDI-IHC channels**  
   Run `maldi_ihc_gsr.ipynb` → outputs GSR-enhanced protein marker images.

2. **Cell segmentation and phenotype assignment**  
   Run `cell_phenotyping.ipynb` → generates phenotype-labeled cell masks.

3. **Train metabolic GNN on low-res lipidomic data**  
   Run `lowres_metabolic_barcoding.ipynb` → outputs top lipid features and initial barcodes.

4. **Super-resolve lipid features**  
   Run `lipid_gsr.ipynb` → generates GSR versions of key lipids.

5. **Barcode correction and classification**  
   Run `superres_metabolic_barcoding.ipynb` → final phenotype predictions and pseudotime analysis.

#### Expected Output

- Super-resolved `.npy` or `.tiff` MSI images  
- Single-cell `AnnData` files with phenotypes and metabolite vectors  
- Barcode visualizations (bar plots, UMAPs, subgraphs)  
- Per-cell predictions and AUC metrics

#### ⏱️ Estimated Runtime (desktop CPU or GPU)

| Step                              | Runtime (CPU)   | Runtime (GPU) |
|----------------------------------|-----------------|---------------|
| GSR on protein markers           | ~5 minutes      | ~2 minutes    |
| Cell phenotyping                 | ~2 minutes      | ~1 minute     |
| GNN on lipidomics (low-res)      | ~8 minutes      | ~3 minutes    |
| GSR on top 15 lipid channels     | ~6 minutes      | ~3 minutes    |
| RF classifier on barcodes        | ~4 minutes      | ~2 minutes    |

> 💡 Total time: ~25 minutes (CPU), ~10 minutes (GPU)

---

## 🧬 4. Usage on Your Data

To apply this pipeline to your own MSI + structural image dataset:

1. **Preprocess**
   - Align structural (fluorescence, IMC, H&E) image with MSI using BigWarp or equivalent.
   - Normalize MSI to [0,1] and convert to `.npy` or `.tiff`.

2. **Run GSR**
   - Use `maldi_ihc_gsr.ipynb` or `lipid_gsr.ipynb` for protein/lipid MSI channels.

3. **Cell segmentation + phenotyping**
   - Segment nuclei using Mesmer (or provide masks).
   - Annotate cell types based on marker expression with `cell_phenotyping.ipynb`.

4. **Metabolic Barcoding**
   - Run `lowres_metabolic_barcoding.ipynb` to generate barcodes using a GNN.
   - Refine using GSR-enhanced MSI features with `superres_metabolic_barcoding.ipynb`.

> To reproduce manuscript results, follow the notebooks in order and set dataset paths accordingly.

---

## 📄 Citation

If you use this software, please cite:

**Ozturk et al. (2025)**  
_Super Resolved Single-cell Spatial Metabobarcoding and Metabotyping for Unlimited Chemical Maps_  
DOI: (pending)

---

## 🔐 License

This project is released for academic and non-commercial use only.

---

## 📦 Data Availability

- Super-resolved MSI (Figshare): https://doi.org/10.6084/m9.figshare.29522213  
- Single-cell `AnnData` (Figshare): https://doi.org/10.6084/m9.figshare.29524625

---

## 📁 Repository

- GitHub: https://github.com/coskunlab/MAGIC-Metabotyping-and-Advanced-Graphical-Imaging-of-Chemicals

---
