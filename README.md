# ARIEL 2025 Final Submission – Project Architecture

This repository contains the final machine learning pipeline for the ARIEL 2025 competition.  
The workflow is implemented inside the notebook `ariel-2025-final-submission.ipynb`, organized into a set of well-defined architectural layers to ensure clarity, maintainability, and reproducibility.

---

# Architecture Overview

This project is built as a complete end-to-end pipeline. It takes raw ARIEL observation data, performs feature extraction, trains machine learning models, generates predictions, applies physics-informed corrections, and builds a competition-ready submission file.

---

## High-Level Pipeline

```mermaid
flowchart TD
    A[Data Loading] --> B[Feature Engineering]
    B --> C[Model Training]
    C --> D[Prediction Generation]
    D --> E[Post-processing and Noise Correction]
    E --> F[Submission File Builder]
Architecture Components
1. Data Loading Layer

The data loading component reads and structures all raw ARIEL telescope datasets.

Loads flux, sigma, and metadata files

Merges and cleans raw observational data

Prepares standardized DataFrame outputs

Purpose: Provide a stable and consistent data foundation for all downstream processes.

2. Feature Engineering Layer

This layer converts raw telescope time-series into model-ready features.

Key operations include:

Rolling window statistical calculations

Gradient, slope, and variability features

Flux dip detection

Symmetry and event-shape features

Outlier and noise handling

Injection-based anomaly analysis

Vectorized computations for performance

Purpose: Extract meaningful physical patterns from the flux time series to improve model accuracy.

3. Modeling Layer

This layer builds and trains the machine learning models used for prediction.

Uses the CatBoost algorithm

Supports multiple model configurations

Contains hyperparameter definitions

Ensures deterministic training

Purpose: Train ML models optimized for ARIEL flux prediction and competition scoring.

4. Prediction and Ensembling Layer

Responsible for generating predictions from trained models.

Computes raw model outputs

Supports multiple prediction variants

Optional simple ensembling

Optimized batch inference

Purpose: Produce stable, high-quality predictions for the ARIEL challenge dataset.

5. Post-processing and Noise Correction Layer

Applies astrophysics-aware corrections to improve prediction realism.

Includes:

Flux dip detection and analysis

Symmetry scoring

Sigma noise correction formulas

Gaussian smoothing

Physically consistent prediction adjustments

Purpose: Reduce noise, correct anomalies, and align predictions with expected telescope behavior.

6. Submission Builder

This final component constructs the official ARIEL competition submission file.

Combines corrected predictions

Converts outputs to the required format

Creates the final id → value mapping

Previews the submission file before saving

Purpose: Automate and validate the generation of the final competition submission CSV file.

Conceptual Project Structure

Although the project lives inside a single notebook, it is logically structured as follows:

ariel-2025-final-submission.ipynb
│
├── Configuration and Parameters
├── Utility Functions
├── Data Loading
├── Feature Engineering
├── Model Training
├── Prediction Pipeline
├── Post-processing
└── Submission Builder
