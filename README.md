# mPAWs

mPAWs — Masked Pre-training for Aquatic Wildlife Systems

A multi-task underwater vision framework using self-supervised pre-training on unlabelled data,
fine-tuned for classification, segmentation, and coordinate regression.


📌 Overview
mPAWs is a semi-supervised deep learning system for underwater image understanding. It leverages masked image modeling to pre-train a CNN backbone on large amounts of unlabelled underwater data — learning rich visual representations without human annotation.
The pre-trained backbone is then fine-tuned for three distinct perception tasks, each using a different form of supervision:
TaskSupervision TypeLabel Format🐠 ClassificationClass labelsCategory IDs🎭 SegmentationPixel-wise masksMasked label images📍 RegressionSpatial coordinates(x, y) coordinate labels
This design demonstrates how a single self-supervised backbone can transfer to diverse downstream tasks with minimal labelled data.

🧠 Architecture
Unlabelled Underwater Data
        │
        ▼
┌─────────────────────────┐
│  Masked Image Modeling  │  ← Self-supervised pre-training
│  (CNN Backbone)         │    Random patches masked & reconstructed
└────────────┬────────────┘
             │  Shared Representations
     ┌───────┼───────┐
     ▼       ▼       ▼
┌─────────┐ ┌──────────────┐ ┌────────────────┐
│ Classif-│ │ Segmentation │ │   Regression   │
│ ication │ │    Head      │ │     Head       │
│  Head   │ │(masked labels│ │ (coordinates)  │
└─────────┘ └──────────────┘ └────────────────┘

🔬 Methodology
1. Self-Supervised Pre-training

Data: Large unlabelled underwater image dataset
Technique: Masked Image Modeling — random image patches are masked; the model learns to reconstruct them
Goal: Build a strong visual backbone that understands underwater textures, lighting, and structures without any labels

2. Fine-tuning — Classification

Standard supervised fine-tuning on labelled samples
Demonstrates sample efficiency: strong performance with few labelled examples
Metric: Top-1 / Top-5 accuracy

3. Fine-tuning — Segmentation

Uses masked label images as pixel-level supervision
The model learns to delineate object boundaries in underwater scenes
Metric: Mean IoU (Intersection over Union)

4. Fine-tuning — Regression

Uses image coordinates as label data
Predicts spatial positions of objects/keypoints within underwater frames
Metric: Mean Absolute Error (MAE) on coordinate predictions


🗂️ Repository Structure
mPAWs/
│
├── pretrain/
│   ├── masking.py           # Patch masking strategy
│   ├── pretrain_model.py    # CNN backbone + reconstruction head
│   └── pretrain_train.py    # Pre-training loop
│
├── finetune/
│   ├── classification/
│   │   ├── model.py
│   │   └── train.py
│   ├── segmentation/
│   │   ├── model.py
│   │   └── train.py
│   └── regression/
│       ├── model.py
│       └── train.py
│
├── data/
│   ├── unlabelled/          # Raw underwater images
│   ├── labelled/            # Classification labels
│   ├── masks/               # Segmentation mask images
│   └── coordinates/         # Regression coordinate labels
│
├── notebooks/
│   └── demo.ipynb           # End-to-end pipeline walkthrough
│
├── results/
│   ├── classification/      # Accuracy curves, confusion matrices
│   ├── segmentation/        # IoU plots, visual predictions
│   └── regression/          # MAE plots, coordinate overlays
│
└── README.md

📊 Results

(To be updated with final benchmarks)

TaskMetricScoreClassificationTop-1 Accuracy—SegmentationMean IoU—RegressionMean Abs. Error—

🛠️ Tech Stack

Framework: PyTorch / TensorFlow (update as applicable)
Architecture: CNN with task-specific heads
Training: Self-supervised pre-training → supervised fine-tuning
Domain: Underwater / Aquatic imagery


📄 Research
A research paper documenting the methodology, experiments, and findings is currently in preparation.
Paper status: In writing — will be linked here upon publication.

🚀 Getting Started
bash# Clone the repository
git clone https://github.com/your-username/mPAWs.git
cd mPAWs

# Install dependencies
pip install -r requirements.txt

# Run self-supervised pre-training
python pretrain/pretrain_train.py --config configs/pretrain.yaml

# Fine-tune for classification
python finetune/classification/train.py --config configs/classify.yaml

📬 Contact
Ayushi Shekhar
ushishekhar@gmail.com
