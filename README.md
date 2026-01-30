# BiTE-Design
AI Co-Scientist Challenge Korea 2026

# Comparative Evaluation of AI-Guided vs. Human-Constrained Linker Design for BiTEs

This repository contains the source code, analysis pipelines, and structural models for the paper submitted to the **2026 AI Co-Scientist Challenge Korea**.

## 📂 Repository Contents

### 1. Generation & Analysis Pipelines (Jupyter Notebooks)

* **`Inpainting_RFdiffusion.ipynb`**
  - **Method A (Inpainting):** Script for generating linkers using RFdiffusion with "Inpainting" mode, allowing the AI to optimize geometry between scFv domains.

* **`PADD_RFdiffusion.ipynb`**
  - **Method B (PADD):** Script for generating linkers using the "Fixed Backbone" strategy, where human-defined helical phase constraints are enforced.

* **`BiTE_Rigid_Linker_Analysis_Pipeline.ipynb`**
  - **Bulk Analysis:** The main automated pipeline for analyzing thousands of generated models.
  - Calculates RMSD, Inter-domain Fluctuation (Stiffness), and NMA metrics.

* **`Final_Candidate_Analysis.ipynb`**
  - **Validation:** The final stress-test analysis script used to verify the Top 3 candidates after AlphaFold2 resampling (12 recycles).

### 2. Structural Models (Top Candidates)

We present the top three linker designs selected from over 2,048 generated models. The selection was based on strict criteria: **(1) Proximity to 130Å target distance**, **(2) Structural Rigidity (Low Fluctuation)**, and **(3) AlphaFold Confidence (pLDDT)**.

#### 🏆 Rank 1: Lead Candidate (Method B: PADD)
* **Filename:** `Fixed_backbone85.pdb`
* **Strategy:** Phase-Aligned De Novo Design (Human-Constrained Geometry)
* **Selection Reason:** - The **Global Best** model demonstrating the highest thermodynamic stability (pLDDT > 90) and lowest inter-domain fluctuation.
  - Validates that explicitly correcting the "Helical Phase" (100° rotation) is critical for rigid linker design.
  - Achieves the target geometry with a robust, textbook-quality alpha-helical structure that AI alone failed to generate consistently.

#### 🥈 Rank 2: Runner-up Candidate (Method B: PADD)
* **Filename:** `Fixed_backbone54.pdb`
* **Strategy:** Phase-Aligned De Novo Design
* **Selection Reason:**
  - Selected to demonstrate the **reproducibility** of the PADD method.
  - Like Candidate 85, it maintains high rigidity and structural confidence, proving that the PADD framework reliably produces developable candidates.
  - Serves as an excellent alternative scaffold with slightly different surface properties.

#### 🥉 Rank 3: Comparative Candidate (Method A: Inpainting)
* **Filename:** `Inpainting5.pdb`
* **Strategy:** Geometry-Guided Inpainting (AI-Driven Geometry)
* **Selection Reason:**
  - The best model found by the Inpainting method, included for **comparative analysis**.
  - While it successfully found a unique "Rigid Bend" geometry to bridge the gap, its thermodynamic stability scores (pLDDT) and structural definition were slightly lower than the PADD candidates.
  - Highlights the trade-off between geometric novelty (Inpainting) and biophysical stability (PADD).
### 3. Input Templates & Reference Files

This section contains the starting structures used to initialize the RFdiffusion process (Inputs) and the benchmarks used for analysis.

#### 🧬 Input Templates (Before Generation)
* **`Inpainting_template.pdb`**
  - **Used for:** Method A (Geometry-Guided Inpainting)
  - **Description:** The input structure defining the two scFv domains with a "mask" between them. The AI was tasked to generate a linker connecting these specific endpoints.
* **`PADD_template.pdb`**
  - **Used for:** Method B (Phase-Aligned De Novo Design)
  - **Description:** The "Fixed Backbone" template with pre-calculated helical phase constraints. This structure forced the AI to optimize the sequence for a specific, rigid geometry.

#### 📏 Validation References
* **`reference.pdb`**: The baseline backbone structure used as the "Ground Truth" for RMSD alignment and calculations.
* **`Include_antigen_with_perfect_distance.pdb`**: The full Antigen-BiTE complex structure. Used to measure the inter-membrane distance and verify if the generated linkers successfully span the ~130Å gap.

---
## 🛠️ Usage
These notebooks are designed to run on **Google Colab (Pro/Pro+)** environments with GPU acceleration.
1. Download the `.ipynb` files.
2. Upload the necessary `.pdb` files to your Colab session.
3. Run the cells sequentially to reproduce the analysis.

**Note:** To demonstrate the efficiency of our high-throughput screening pipeline, the PDB files provided here are **unrelaxed** structures (Top Candidates, direct AlphaFold2 outputs without AMBER energy minimization). This highlights that our design strategy yields geometrically valid and rigid structures even before expensive refinement steps.
