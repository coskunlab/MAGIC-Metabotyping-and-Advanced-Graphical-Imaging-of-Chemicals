# MAGIC

This repository provides the analysis pipeline for the clozapine dose-response mouse brain dataset using the MAGIC framework introduced in the manuscript: **Super Resolved Single-cell Spatial Metabobarcoding and Metabotyping for Unlimited Chemical Maps**

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

- **Operating Systems:** Windows 10/11
- **Python Version:** 3.10
- **Memory:** ≥16 GB RAM
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
> • PyTorch 2.7.1 + CUDA 12.6 
> • Windows 11

### 🧰 Reproducible environments (Conda YAML)

For a fully reproducible setup, use the provided Conda environment files:

- **GPU (CUDA 12.6):** `environment.yml`
- **CPU‑only:** `environment-cpu.yml`

These pin versions for PyTorch, imaging, and the single‑cell stack. If you prefer `pip`, you can still use `requirements.txt`.

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
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126
```

---

## 🧪 3. Demo
### Interactive quickstart (Python **Shiny** app)

The Shiny app (`app.py`) demonstrates **Guided Super‑Resolution (GSR)** on a single low‑res MSI image using a high‑res guide.

**Run**
```bash
# if not already installed via requirements
pip install shiny pytorch_msssim super-image opencv-python pillow scikit-image matplotlib

# launch (either works)
python app.py
# or:
shiny run --reload --launch-browser app.py
```

**Use in the browser**
1. **Guide (high‑res structure):**
2. **Low‑res MSI:** select one test image
3. Set **Epochs** (e.g., `50`) and **SSIM weight** (e.g., `0.15`)  
4. Click **Run SR** to generate the super‑resolved output

**What you’ll see**
- Left: uploaded **Guide** image  
- Middle: **Low‑res** MSI  
- Right: **Super‑resolved** MSI (viridis) produced by the Two‑Input U‑Net (with EDSR pre‑upsampling)

**Typical runtime (per image)**
- GPU: ~20–40 s for 100 epochs

## ▶️ 4. Reproducing the results in clozapine dataset

Use the data in https://doi.org/10.6084/m9.figshare.29650292.v1 for reproducing the results in clozapine dataset.

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

- Super-resolved `.npy` MSI images  
- Single-cell `AnnData` files with phenotypes and metabolite vectors  
- Barcode visualizations (bar plots, UMAPs, subgraphs)  
- Per-cell predictions and AUC metrics

#### ⏱️ Estimated Runtime (desktop GPU)

| Step                             | Runtime (GPU) |
|----------------------------------|-----------------|
| GSR on protein markers           | ~5 hours        | 
| Cell phenotyping                 | ~15 minutes     |
| GNN on lipidomics (low-res)      | ~20 minutes     | 
| GSR on top 15 lipid channels     | ~3.5 hours      | 

> 💡 Total time: ~9 hours (GPU)

---

## 🧬 5. Usage on Your Data

To apply this pipeline to your own MSI + structural image dataset:

1. **Preprocess**
   - Align structural (fluorescence, IMC, H&E) image with MSI using ImageJ BigWarp, SIFT or equivalent.
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
- Clozapine dose-response mouse brain dataset (Figshare): https://doi.org/10.6084/m9.figshare.29650292.v
---

## 📁 Repository

- GitHub: https://github.com/coskunlab/MAGIC-Metabotyping-and-Advanced-Graphical-Imaging-of-Chemicals

---
