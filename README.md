# Chihuahua vs Muffin Classification using 3LC

## Overview

This repository contains the solution developed for the Kaggle competition **“The 3LC HACK[AI]THON”**. The objective of the competition is to build a binary image classifier that distinguishes between Chihuahua images and Muffin images using a data-centric AI workflow powered by 3LC.

Unlike traditional machine learning competitions that focus on improving model architectures, this competition emphasizes improving dataset quality through iterative labeling, embeddings analysis, and sample weighting.

The model architecture is fixed to ResNet-18 and must be trained from scratch without pretrained weights.

---

# Competition Objective

Build a binary image classifier where:

| Label | Class |
|------|------|
| 0 | Chihuahua |
| 1 | Muffin |

The primary goal is to improve model accuracy through better data curation and active learning strategies using the 3LC platform.

---

# Project Structure

```bash
.
├── data/
│   ├── train/
│   ├── val/
│   └── test/
│
├── register_tables.py
├── train.py
├── predict.py
├── config.yaml
├── best_model.pth
├── submission.csv
├── requirements.txt
└── README.md
```

---

# Dataset Information

| Dataset Split | Description |
|------|------|
| Train | 100 labeled images + 3579 unlabeled images |
| Validation | 1000 balanced validation images |
| Test | 1184 hidden test images |

---

# Technologies Used

- Python 3.9+
- PyTorch
- Torchvision
- 3LC
- UMAP
- Kaggle

---

# Environment Setup

## Step 1: Create Virtual Environment

### Windows

```bash
python -m venv 3lc-env
3lc-env\Scripts\activate
```

### Linux / macOS

```bash
python -m venv 3lc-env
source 3lc-env/bin/activate
```

---

# Install Dependencies

## CPU Installation

```bash
pip install 3lc joblib pytz umap-learn torch torchvision
```

## GPU Installation (CUDA Example)

### CUDA 11.8

```bash
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118
pip install 3lc joblib pytz umap-learn
```

---

# 3LC Setup

## Create 3LC Account

Create an account at:

```text
https://account.3lc.ai
```

Generate an API key from:

```text
https://account.3lc.ai/api-key
```

---

# Login to 3LC

```bash
3lc login YOUR_API_KEY
```

---

# Start 3LC Service

```bash
3lc service
```

Open the dashboard in your browser:

```text
https://dashboard.3lc.ai
```

---

# Workflow

## Step 1: Register Tables

Run the following command to create train and validation tables inside 3LC:

```bash
python register_tables.py
```

---

# Step 2: Initial Training

Train the ResNet-18 model on the currently labeled data:

```bash
python train.py
```

This step will:

- Train the model
- Generate embeddings
- Track experiments in 3LC
- Save model checkpoints
- Store metrics and predictions

The best model is saved as:

```text
best_model.pth
```

---

# Step 3: Analyze Embeddings in 3LC Dashboard

Inside the 3LC Dashboard:

1. Open the latest run
2. Visualize embeddings in 3D
3. Filter unlabeled samples
4. Inspect confidence scores
5. Label useful samples
6. Set sample weight to `1`
7. Save a new table revision

This creates an improved dataset revision for retraining.

---

# Step 4: Retrain Model

Retrain the model using the updated dataset:

```bash
python train.py
```

The script automatically loads the latest table revision from 3LC.

Repeat the following cycle as needed:

```text
Train → Analyze → Label → Retrain
```

---

# Step 5: Generate Predictions

Run inference on the hidden test set:

```bash
python predict.py
```

This generates:

```text
submission.csv
```

---

# Submission Format

The generated CSV file must follow this structure:

```csv
image_id,prediction,confidence
test_00001,0,0.92
test_00002,1,0.88
```

| Column | Description |
|------|------|
| image_id | Unique image identifier |
| prediction | Predicted class (0 or 1) |
| confidence | Model confidence score |

---

# Data-Centric AI Workflow

This project follows a data-centric AI approach where model performance is improved by improving the quality of training data instead of modifying model architecture.

The workflow includes:

1. Training with limited labeled data
2. Generating embeddings and predictions
3. Identifying useful unlabeled samples
4. Strategically labeling samples
5. Retraining with improved data
6. Repeating the process iteratively

---

# 3LC Features Used

- Tables
- Dataset Revisions
- Experiment Runs
- Embeddings Visualization
- Sample Weights
- Dashboard Analytics

---

# Training Constraints

The following competition rules were strictly followed:

- ResNet-18 architecture only
- No pretrained weights
- No external datasets
- Training from scratch
- 3LC workflow mandatory

---

# Results

| Metric | Score |
|------|------|
| Validation Accuracy | XX% |
| Public Leaderboard Score | XX |
| Private Leaderboard Score | XX |

---

# Screenshots

Add screenshots in this section:

- Embeddings visualization
- Accuracy graphs
- Dashboard analytics
- Confusion matrix

Example:

```markdown
![Embeddings](screenshots/embeddings.png)
```

---

# Resources

## 3LC Documentation

```text
https://docs.3lc.ai
```

## Kaggle Competition

```text
https://www.kaggle.com
```

## PyTorch Documentation

```text
https://pytorch.org
```

---

# Team Information

| Name | Role |
|------|------|
| Your Name | Developer / Researcher |

---

# License

This project was developed for educational and hackathon purposes.

---

# Acknowledgments

Special thanks to:

- 3LC
- Sphere Hive
- JOY Startup Incubators Lab
- Kaggle

for organizing and supporting this competition.
