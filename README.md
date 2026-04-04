# Uncertainty in Quantitative DCE-MRI

<p>
  <a href="https://www.sciencedirect.com/science/article/pii/S136184152500427X"><img src="https://img.shields.io/badge/Paper-Medical%20Image%20Analysis-blue"></a>
  <a href="https://www.python.org/"><img src="https://img.shields.io/badge/Python-3.x-3776AB.svg"></a>
  <a href="https://pytorch.org/"><img src="https://img.shields.io/badge/PyTorch-2.4-EE4C2C.svg"></a>
  <a href="https://lightning.ai/docs/pytorch/stable/"><img src="https://img.shields.io/badge/PyTorch%20Lightning-2.4-792EE5.svg"></a>
</p>

Research code for **physics-informed uncertainty quantification in DCE-MRI** using mean-variance estimation, stochastic baselines, and physics-informed variants.

<p align="center">
  <img src="https://ars.els-cdn.com/content/image/1-s2.0-S136184152500427X-gr7_lrg.jpg" alt="Paper figure" width="900"/>
</p>

---

## 📄 Paper

- **Physics-Informed Uncertainty Quantification in DCE-MRI using Mean Variance Estimation**
- Link: https://www.sciencedirect.com/science/article/pii/S136184152500427X

---

## ✨ What this repository includes

- Multiple uncertainty-aware model families:
  - `snn`
  - `pinn`
  - `mve_snn`
  - `mve_pinn`
  - `pinn_ph`
- Networks:
  - `fc`, `fc_unc`
  - `dcenet`, `dcenet_unc`
- Datasets/modes:
  - `normal`, `ood`, `vivo`
- End-to-end scripts for simulation, training, evaluation, ensembling, and NLLS baselines.

---

## 📂 Repository structure

```text
.
├── configs/                 # Experiment configs (normal/ood/vivo + debug/example)
├── data/                    # Input and generated datasets
├── jobs/                    # Job scripts
├── models/                  # Model wrappers (SNN, PINN, MVE, physics-informed)
├── networks/                # Network backbones (FC, DCENet and uncertainty variants)
├── scripts/
│   ├── simulate.py
│   ├── simulate_ood.py
│   ├── train.py
│   ├── eval.py
│   ├── ensemble.py
│   └── nlls.py
├── utils/                   # Data modules, metrics, helpers
└── requirements.txt
```

---

## 🔧 Installation

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

---

## 🚀 Quick start

### 1) Optional: simulate data

```bash
python scripts/simulate.py
python scripts/simulate_ood.py
```

### 2) Run the example pipeline

```bash
python scripts/example.py
```

### 3) Train a model from config

```bash
# debug run
python scripts/train.py --config debug --seed 0 --vis True

# example config
python scripts/train.py --config example --seed 42 --vis True
```

### 4) Evaluate a trained checkpoint/output folder

```bash
python scripts/eval.py --path output/normal/mve_pinn_fc_0 --eval True --save_preds True
```

### 5) Evaluate an ensemble

```bash
python scripts/ensemble.py --config configs/normal/ensemble_snn.yaml --eval True --save_preds True
```

### 6) Run NLLS baseline

```bash
python scripts/nlls.py --mode sim --simmode normal --eval True --vis True
```

---

## ⚙️ Configuration notes

- Config files are in `configs/` (including `configs/normal`, `configs/ood`, `configs/vivo`).
- Core fields include:
  - `model`, `network`, `dataset`, `mode`
  - `epochs`, `batch_size`, `lr`, `batch_per_epoch`
  - `logger` (`wandb` or local/default)
  - `kwargs` (e.g., `burnin_epochs`, `dt_predictor`)

---

## 📊 Logging

Supported logging:
- Default PyTorch Lightning logger
- Weights & Biases (`logger: wandb` in config)

---

## 📝 Citation

If you use this codebase, please cite the paper:

```bibtex
@article{dce_mri_uq_2025,
  title   = {Physics-Informed Uncertainty Quantification in DCE-MRI using Mean Variance Estimation},
  journal = {Medical Image Analysis},
  year    = {2025},
  url     = {https://www.sciencedirect.com/science/article/pii/S136184152500427X}
}
```
