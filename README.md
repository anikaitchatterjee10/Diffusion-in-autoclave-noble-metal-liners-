# PyLiner — Diffusion in Autoclave Noble-Metal Liners
[![Python](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)
[![Panel](https://img.shields.io/badge/built%20with-Panel-0072B2.svg)](https://panel.holoviz.org/)
[![Bokeh](https://img.shields.io/badge/Bokeh-3.x-EA5C2C.svg)](https://bokeh.org/)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/anikaitchatterjee10/Diffusion-in-autoclave-noble-metal-liners-/main?urlpath=lab)
[![Data: XLSX](https://img.shields.io/badge/data-Diffusion%20Coefficients.xlsx-green.svg)](data/Diffusion%20Coefficients.xlsx)

Semi-empirical methodology for **predicting transition-metal diffusion through silver barriers** under ammonothermal crystal-growth conditions (> 300 °C, 100–400 MPa).


---

## Overview

Silver (Ag) barriers (liners, capsules, and coatings) are widely used in ammonothermal crystal growth of nitride semiconductors (such as GaN) to mitigate corrosion and suppress impurity transport from high-temperature, high-pressure autoclave alloys. This repository provides tools to estimate missing Arrhenius diffusion parameters $(Q, D_0)$ in Ag, propagate parameter uncertainties, and evaluate diffusion-limited breakthrough times ($t_{\text{BT}}$) across ammonothermal reactor configurations.

---

## Methodology in Brief

1. **Literature Compilation & Outlier Screening**:
   - Compiled 43 literature Arrhenius parameter sets for impurity diffusion in Ag and screened outliers at $600\,^\circ\text{C}$ using Z-scores ($|Z| > 2.5$.
   - Excluded 3 statistical outliers (Fe, Co, and Ni from a single reference) and fitted a **Meyer–Neldel Rule (MNR)** relation via **Total Least Squares (TLS)** across the remaining 40 datasets ($\text{SEE} = 0.963$ in $\ln D_0$, corresponding to a factor of $\approx 2.6$ in $D_0$)[cite: 1].
2. **Arrhenius Parameter Estimation**:
   - Estimated activation energies $Q$ using published data-driven models (ANN and linear regression by Zeng et al., and Ag-specific multiple regression by Onodera et al.)[cite: 1].
   - Estimated $D_0$ via the MNR correlation, then computed representative parameters using the **arithmetic mean of $Q$** and **geometric mean of $D_0$** (providing complete pairs for data-deficient elements such as B, C, P, Sc, Y, Zr, Hf, and others)[cite: 1].
3. **1D Bulk Diffusion & Breakthrough Time ($t_{\text{BT}}$)**:
   - Modeled vacancy-mediated 1D bulk diffusion (Fick's second law) across a barrier of thickness $L$ from a constant alloy source concentration $C_i$ to a semi-infinite boundary, neglecting the minor $p\Delta V$ pressure term ($\lesssim 3.8\text{ kJ mol}^{-1}$ at $\le 400\text{ MPa}$)[cite: 1].
   - Defined $t_{\text{BT}}$ as the time for concentration at $x = L$ to reach a conservative threshold of $5 \times 10^{14}\text{ cm}^{-3}$ (lowest reported SIMS detection limit for relevant impurities in GaN) and propagated parameter uncertainties into $t_{\text{BT}}$[cite: 1].
4. **Autoclave & Head-Assembly Case Studies**:
   - Evaluated **René® 41** ($400\text{–}850\,^\circ\text{C}$, up to $1000\,\mu\text{m}$ liner; and $20\text{–}850\,^\circ\text{C}$, up to $500\,\mu\text{m}$ tube coating) and **stainless steel 1.4571** ($20\text{–}200\,^\circ\text{C}$, up to $500\,\mu\text{m}$ head-assembly coating) for **Fe, Ni, Cr, and Mn**[cite: 1].

---

## Plots & Figures

*Update the image paths below to match your repository's figure directory.*

### 1. Meyer–Neldel Screening & Regression
- **Z-Score Outlier Screening ($\ln D$ at $600\,^\circ\text{C}$ vs. $Q$) & MNR TLS Fit ($\ln D_0$ vs. $Q$)**: Identifies the 3 excluded outliers and shows the TLS regression line with $\pm 1\text{ SEE}$ band[cite: 1].  
  `![Meyer-Neldel Analysis](figures/fig_mnr_tls.png)`

### 2. Estimated Arrhenius Parameters & Plausibility Domain
- **Activation Energy $Q$ Comparison Across Elements & Methods**: Compares Method 1 (ANN), Method 2 (linear regression), and Method 3 (MRA) across solutes sorted by atomic number[cite: 1].  
  `![Activation Energy Comparison](figures/fig_q_comparison.png)`
- **Pre-Exponential Factor $D_0$ Comparison Across Elements & Methods**: Compares MNR-derived $D_0$ values across estimation methods on a log scale[cite: 1].  
  `![Pre-Exponential Factor Comparison](figures/fig_d0_comparison.png)`
- **Mehrer's Plausibility Domain ($D$ at $600\,^\circ\text{C}$ vs. $Q$)**: Benchmarks estimated solute diffusivities and activation energies against FCC substitutional plausibility bounds and Ag self-diffusion[cite: 1].  
  `![Mehrer Plausibility Domain](figures/fig_mehrer_domain.png)`

### 3. Breakthrough Time vs. Temperature (with Uncertainty Bounds)
- **95% Confidence Intervals ($1\text{ mm}$ vs. $200\,\mu\text{m}$, $50\text{–}850\,^\circ\text{C}$)**:
  - **Fe and Ni**[cite: 1]: `![Breakthrough Time Fe and Ni](figures/fig_bt_ci_fe_ni.png)`
  - **Cr and Mn (Appendix D)**[cite: 1]: `![Breakthrough Time Cr and Mn](figures/fig_bt_ci_cr_mn.png)`

### 4. Temperature–Thickness Breakthrough Time Maps
- **René® 41 Liner ($400\text{–}850\,^\circ\text{C}$, $0\text{–}1000\,\mu\text{m}$)**:
  - **Fe and Ni**[cite: 1]: `![Rene 41 Liner Fe and Ni](figures/fig_map_rene41_fe_ni.png)`
  - **Cr and Mn (Appendix D)**[cite: 1]: `![Rene 41 Liner Cr and Mn](figures/fig_map_rene41_cr_mn.png)`
- **René® 41 Tube / Head-Assembly Coating ($20\text{–}850\,^\circ\text{C}$, $0\text{–}500\,\mu\text{m}$)**:
  - **Fe and Ni**[cite: 1]: `![Rene 41 Coating Fe and Ni](figures/fig_map_coating_rene41_fe_ni.png)`
- **Stainless Steel 1.4571 Head-Assembly Coating ($20\text{–}200\,^\circ\text{C}$, $0\text{–}500\,\mu\text{m}$)**:
  - **Fe and Ni**[cite: 1]: `![SS 1.4571 Coating Fe and Ni](figures/fig_map_ss14571_fe_ni.png)`
  - **Cr and Mn (Appendix D)**[cite: 1]: `![SS 1.4571 Coating Cr and Mn](figures/fig_map_ss14571_cr_mn.png)`

### 5. Literature GaN Impurity Benchmark
- **Reported Impurity Concentrations in Ammonothermal GaN**: Compares literature concentrations for Cr, Mn, Fe, and Ni across mineralizers and barrier configurations[cite: 1].  
  `![Literature GaN Impurity Concentrations](figures/fig_gan_impurities.png)`

---

## Citation & Funding

If you use this code or dataset, please cite the accompanying manuscript[cite: 1]. Supported by the **Deutsche Forschungsgemeinschaft (DFG)** (Project No. 512083685) and the **Emerging Talents Initiative (ETI) of FAU Erlangen-Nürnberg**[cite: 1].
---

## 📜 Citation

If you use this repository or methodology, please cite:

> (Cite)[cite: 1]
