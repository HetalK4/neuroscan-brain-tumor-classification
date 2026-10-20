# NeuroScan — Brain Tumor MRI Classification

> **This is a personal portfolio copy of a group capstone project**, uploaded to showcase my
> individual contribution. It is **not the canonical team repository**, please see the
> **Team & Credit** section below before assuming any part of this is solely my work.

## Project Overview

NeuroScan is a deep learning pipeline for classifying brain tumors from MRI scans into four
categories — `glioma`, `meningioma`, `notumor`, and `pituitary`. The project benchmarks a
custom Convolutional Neural Network (trained from scratch) against two transfer-learning
architectures, ResNet-50 and DenseNet-121, and deploys the best-performing model as an
interactive web application.

## My Contribution

This capstone was split into four defined roles across the team. **I was responsible for:**

- **Role 2 — Model Development:** Built PyTorch `DataLoader` pipelines with medical-grade
  data augmentation, and trained/tuned all three architectures (Custom CNN, ResNet-50,
  DenseNet-121).
- **Role 3 — Evaluation & Metrics:** Built the full evaluation suite, classification
  reports, multi-class confusion matrices, ROC-AUC curves, and applied Grad-CAM
  explainability to verify that predictions were driven by actual tumor regions rather than
  background artifacts.

Data collection/preprocessing (Role 1) and final deployment packaging (Role 4) were handled
by other teammates (see credits below).

## Team & Credit

This was a **group capstone project of four members**, not individual work:

- **Majesty:** maintains the canonical team repository:
  [NeuroScan-Tumor-Classification-Using-Traditional-CNN-ResNet-50-DenseNet-121](https://github.com/Majesty0/NeuroScan-Tumor-Classification-Using-Traditional-CNN-ResNet-50-DenseNet-121)
- **Bradley**
- **Mitchelle**
- **Hetal Kumbharana (me):** Model Development (Role 2) and
  Evaluation & Metrics (Role 3)

Data collection and deployment were handled by other members of the team.
If you're reviewing this for an application, the canonical repository above
reflects the complete team submission.

## Dataset

7,200 MRI images, split into:
- 4,760 training samples
- 840 validation samples
- 1,600 unseen test samples

Images varied in size and color mode (L, P, RGB, RGBA) and were resized to 224×224 and
converted to 3-channel RGB before being fed to the models. Classes were balanced across all
four categories.

## Models & Results

Three architectures were trained and evaluated on the held-out 1,600-sample test set:

| Model | Type | Test Accuracy | Macro F1 | Weighted F1 | Best Val Loss |
|---|---|---|---|---|---|
| Custom CNN | Trained from scratch | 75.94% | 0.7493 | 0.7493 | 0.3731 |
| ResNet-50 | Transfer learning | 94.37% | 0.9428 | 0.9428 | 0.0651 |
| **DenseNet-121** | **Transfer learning** | **95.31%** | **0.9521** | **0.9521** | **0.0297** |

DenseNet-121 was selected as the final model, with 100% recall on the `notumor` class and
strong performance across all four categories.

## Explainability

Grad-CAM heatmaps were generated for the final model to confirm that predictions were based
on clinically relevant tumor regions rather than spurious background features (an important
sanity check before treating any output as remotely trustworthy in a medical-imaging context).

## Deployment

The final DenseNet-121 model was deployed as an interactive **Streamlit** web app, allowing a
user to upload an MRI image and receive:
- A predicted tumor class
- Per-class confidence scores
- An optional Grad-CAM heatmap overlay

## Tech Stack

`Python` · `PyTorch` · `torchvision` · `scikit-learn` · `OpenCV` · `Streamlit` · `pandas` ·
`NumPy` · `Matplotlib`

## Repository Contents

- `NeuroScan_Data_Preprocessing_ModelDevelopment_Evaluation.ipynb` — full notebook covering
  data pipeline, model training, and evaluation (see role breakdown above for what's mine)
- `requirements.txt` — Python dependencies
- `LICENSE` — MIT License

## Running This Project

```bash
pip install -r requirements.txt
# Run the notebook top to bottom in Jupyter or Google Colab
# (the first cell will fetch the dataset from Kaggle automatically)
```

## License

This project is licensed under the MIT License (see the `LICENSE` file for details).
