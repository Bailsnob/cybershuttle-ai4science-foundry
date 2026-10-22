# Darcy Inference — Reproducible SLURM Workflow

This project demonstrates a fully reproducible inference workflow for the Fourier Neural Operator (FNO) on the Darcy flow dataset using the NeuralOperator library.  
The repository includes:

- a standalone inference script (`darcy_inference.py`)
- a SLURM batch script (`run_darcy_inference.slurm`)
- environment specification (`environment.yml`)
- execution logs
- validation, troubleshooting, and provenance documentation

The goal is to provide a clean, minimal, and fully reproducible example of running scientific ML inference on PACE.

---

## Environment Setup

Load Anaconda and create the environment:

```bash
module load anaconda3
conda env create -f environment.yml
conda activate neuralop
```

Install NeuralOperator from your local clone:

```bash
pip install -e .
```

---

## Local Testing

Before running on SLURM, you can test the model locally:

```bash
python tests/darcy_inference.py
```

These tests confirm that the environment, dataset, and model load correctly.

---

## Running on SLURM (CPU)

Submit the reproducible inference job:

```bash
sbatch run_darcy_inference.slurm
```

This uses your `coc` account and the default CPU partition automatically selected by SLURM.

When the job finishes, SLURM will produce an output file:

```
darcy_inference_<jobid>.out
```

Move this file into the `logs/` directory:

```bash
mv darcy_inference_<jobid>.out logs/
```

The inference script prints:

- dataset path  
- input and target shapes  
- output shape  
- numerical statistics (min, max, mean)  
- device used (CPU)  
- node name  
- job metadata  

This output is used for reproducibility and validation.

---

## Repository Structure

```
vip/
├── darcy_inference.py
├── run_darcy_inference.slurm
├── environment.yml
├── README.md
├── validation.md
├── troubleshooting.md
├── sources.md
├── logs/
│   └── darcy_inference_<jobid>.out
```

---

## Reproducibility Summary

This repository provides:

- a deterministic inference script with shape checks and numerical sanity checks  
- a SLURM batch script that runs cleanly on PACE using the `coc` account  
- complete execution logs stored in `logs/`  
- validation of output correctness (`validation.md`)  
- documentation of SLURM issues and fixes (`troubleshooting.md`)  
- dataset and model provenance (`sources.md`)  

Together, these components ensure that another user can reproduce the inference results on PACE with minimal setup.
