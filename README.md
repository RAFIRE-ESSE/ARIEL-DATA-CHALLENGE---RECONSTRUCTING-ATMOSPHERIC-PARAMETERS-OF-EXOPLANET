# ARIEL 2025 Final Submission – Project Architecture

This repository contains the final machine learning pipeline for the **ARIEL 2025** competition.  
The workflow is implemented inside the notebook **`ariel-2025-final-submission.ipynb`**, organized into clearly defined architectural layers for clarity, maintainability, and reproducibility.

---

## Architecture Overview

This project implements a complete **end-to-end ML pipeline** for ARIEL telescope data.  
It ingests raw observations, extracts features, trains models, generates predictions, applies physics-informed corrections, and finally produces a competition-ready submission.

---

## High-Level Pipeline

flowchart TD
    A[Data Loading] --> B[Feature Engineering]
    B --> C[Model Training]
    C --> D[Prediction Generation]
    D --> E[Post-processing & Noise Correction]
    E --> F[Submission File Builder]

# Architecture Components

## 1. **Data Loading Layer**

Reads and structures all raw ARIEL telescope datasets.

**Capabilities:**
- Loads flux, sigma, and metadata files  
- Merges and cleans raw observational data  
- Produces standardized DataFrame outputs  

**Purpose:**  
Provide a stable and consistent data foundation for all downstream processes.

---

## 2. **Feature Engineering Layer**

Transforms raw telescope time-series into model-ready features.

**Key operations include:**
- Rolling window statistical calculations  
- Gradient, slope, and variability features  
- Flux dip detection  
- Symmetry and event-shape features  
- Outlier and noise handling  
- Injection-based anomaly analysis  
- Highly optimized vectorized computations  

**Purpose:**  
Extract meaningful physical patterns from ARIEL flux data to boost model accuracy.

---

## 3. **Modeling Layer**

Constructs and trains machine learning models for flux prediction.

**Features:**
- CatBoost model implementation  
- Multiple configuration profiles  
- Predefined hyperparameters  
- Fully deterministic model training  

**Purpose:**  
Train models optimized for ARIEL challenge performance and reproducibility.

---

## 4. **Prediction & Ensembling Layer**

Generates predictions from trained models.

**Capabilities:**
- Computes raw model outputs  
- Supports multiple prediction variants  
- Optional lightweight ensembling  
- Optimized batch inference  

**Purpose:**  
Produce stable, high-quality predictions for the ARIEL competition dataset.

---

## 5. **Post-processing & Noise Correction Layer**

Applies astrophysics-informed corrections to the model outputs.

**Includes:**
- Flux dip detection and evaluation  
- Symmetry scoring  
- Sigma-based noise correction formulas  
- Gaussian smoothing  
- Physically guided prediction adjustments  

**Purpose:**  
Reduce noise, correct anomalies, and ensure physical realism in predictions.

---

## 6. **Submission Builder**

Produces the official ARIEL competition submission.

**Responsibilities:**
- Integrates corrected predictions  
- Converts outputs into competition format  
- Builds final `id → value` mapping  
- Provides a preview before saving  

**Purpose:**  
Automate and validate generation of the final submission CSV file.
