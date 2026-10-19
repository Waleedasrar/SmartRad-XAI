# SmartRad-XAI 🩻🤖
### Deep Learning-Based Chest X-ray Classification with Clinical Evaluation at IDC

SmartRad-XAI is a final-year Computer Engineering project that explores how deep learning can classify chest X-ray images into selected disease categories and present model predictions through a mobile-oriented application workflow. The project combines model experimentation, classification evaluation, prediction reporting, and clinical case comparison with Islamabad Diagnostic Centre (IDC).

> **Important medical disclaimer:** SmartRad-XAI is an academic/research prototype, not a certified medical device. It is not intended to diagnose patients, replace radiologists, or guide treatment decisions. Predictions must be reviewed by qualified healthcare professionals.

## Table of Contents
- [Project Overview](#project-overview)
- [Problem and Motivation](#problem-and-motivation)
- [Project Objectives](#project-objectives)
- [Supported Classes](#supported-classes)
- [Dataset](#dataset)
- [Methodology and Workflow](#methodology-and-workflow)
- [Models Compared](#models-compared)
- [Reported Results](#reported-results)
- [Application Features](#application-features)
- [IDC Clinical Evaluation](#idc-clinical-evaluation)
- [Technology Stack](#technology-stack)
- [Repository Contents](#repository-contents)
- [Run the Notebook](#run-the-notebook)
- [Training Configuration](#training-configuration)
- [Limitations and Future Work](#limitations-and-future-work)
- [Team and Acknowledgements](#team-and-acknowledgements)
- [Disclaimer and Data Privacy](#disclaimer-and-data-privacy)

## Project Overview

Chest X-rays are widely used to examine conditions affecting the lungs and chest. Interpreting them requires clinical expertise, and AI-based image classification may help researchers explore ways to support medical-image review.

SmartRad-XAI was developed to:
- Train and compare multiple pretrained deep-learning architectures for five-class chest X-ray classification.
- Select a model based on the experimental comparison.
- Produce a predicted class and confidence score for an input image.
- Explore a mobile application workflow for image upload/capture and viewing prediction reports.
- Compare model predictions on selected real clinical cases with reports from IDC as part of project-level clinical evaluation.

The final presentation identifies **YOLOv8s classification** as the selected model.

## Problem and Motivation

The project investigates whether a practical AI-assisted workflow can classify selected chest X-ray categories while making the output easier to review. The goal is to explore a research prototype that can support preliminary image review—not to automate or replace a clinician's diagnosis.

## Project Objectives

1. Build a deep-learning pipeline for five-class chest X-ray classification.
2. Prepare a subset of the NIH ChestX-ray14 data using image resizing, standardization, and augmentation.
3. Compare ResNet18, ResNet50, Vision Transformer (ViT), and YOLOv8 classification models.
4. Evaluate model performance using classification metrics and confusion-matrix analysis.
5. Integrate prediction output into a mobile application workflow with result/report presentation.
6. Compare selected predictions against IDC clinical reports during project evaluation.

## Supported Classes

The project uses five image classes:

| Class | Meaning |
|---|---|
| `Cardiomegaly` | Enlarged cardiac silhouette label in the dataset |
| `Effusion` | Pleural effusion label |
| `Pneumonia` | Pneumonia label |
| `Pneumothorax` | Pneumothorax label |
| `No Finding` | No finding label in the dataset |

These are dataset labels, not definitive diagnoses for an individual patient.

## Dataset

- **Source:** NIH ChestX-ray14 subset
- **Imaging modality:** Grayscale chest X-rays
- **Project-reported subset size:** 2,465 images across five classes
- **Dataset class folders:** One folder per selected class
- **Preparation:** Resizing, standardization, dataset organization, and augmentation were part of the project methodology.

The NIH dataset contains medical images and associated labels. Use the original source and its terms when obtaining the data:

- [NIH ChestX-ray14 dataset information / download page](https://www.kaggle.com/datasets/nih-chest-xrays/data)

**Dataset note:** Training and validation counts can differ between notebook runs because dataset splitting and saved folders changed during experimentation. For a reproducible result, document the exact split used for the final run and keep patient-level leakage in mind when constructing medical-image splits.

Do not upload the full dataset or any identifiable clinical images to a public repository unless you have confirmed that redistribution is permitted and that all privacy requirements are met.

## Methodology and Workflow

1. **Data preparation** — organize the selected images into class-wise folders and apply the chosen preprocessing.
2. **Transfer learning** — start from pretrained model weights and fine-tune the models for the five target classes.
3. **Training** — train the models in a GPU-enabled environment.
4. **Evaluation** — compare classification accuracy, confusion matrices, and other available metrics.
5. **Model selection** — select YOLOv8s classification based on the results reported in the final project presentation.
6. **Inference** — load trained weights, provide a chest X-ray image, and return the predicted class with a confidence score.
7. **Localization experiment** — the notebook also contains an experiment that matches NIH bounding-box annotations to a subset of images and visualizes available boxes. This is annotation-based visualization; it should not be interpreted as proof that the classifier itself reliably localizes disease.
8. **Application and clinical evaluation** — connect prediction output to the SmartRad-XAI application workflow and compare selected outputs with IDC reports.

## Models Compared

| Model | Role in the project | Accuracy reported in the final presentation |
|---|---|---:|
| ResNet18 | Lightweight residual CNN baseline | 54.3% |
| Vision Transformer (ViT) | Transformer-based image model | 56.3% |
| ResNet50 | Deeper residual CNN | 57.7% |
| YOLOv8s Classification | Selected final classification model | **92.6%** |

**How to read these results:** The percentages above are transcribed from the project's final presentation. They are reported experimental results, not a guarantee of performance on new hospitals, devices, populations, or image distributions. Re-run evaluation on the exact final split before using these numbers for formal benchmarking. A notebook run also records a separate validation output, so results should always be associated with the corresponding checkpoint and dataset split.

The notebook's final metric-calculation cell also reports:
- Precision: **0.7646**
- Recall: **0.7612**
- F1 score: **0.7625**

These metrics are kept separate from the presentation's 92.6% accuracy because the notebook run/split and metric calculation should be verified before treating them as a single consolidated evaluation.

## Application Features

The project presentation describes a mobile application workflow with:
- User login interface and terms/privacy screens.
- Image input from camera or gallery.
- Display of the predicted class and confidence score.
- Prediction report generation.
- Prediction history interface.

The exact availability of these features depends on which mobile application source files are included in this GitHub repository.

## IDC Clinical Evaluation

As documented in the final project presentation and thesis, SmartRad-XAI was evaluated using selected real clinical chest X-ray cases associated with **Islamabad Diagnostic Centre (IDC)**. The project team compared AI-generated predictions with interpretations in IDC radiology reports and documented example cases, including Cardiomegaly, Effusion, and Pneumothorax.

This is described here as **project-level clinical evaluation / comparison**, not as regulatory approval, product certification, or proof of clinical safety. The available project material describes high agreement qualitatively but does not provide a complete, independently reproducible clinical-study protocol or a comprehensive statistical agreement analysis. Therefore, no unsupported clinical-validation percentage is claimed in this README.

Only share clinical images, reports, or related records publicly if IDC and the relevant data owners have explicitly authorized release and all patient privacy requirements are satisfied. Prefer de-identified, approved examples or synthetic placeholders in a public repository.

## Technology Stack

Technologies documented in the project materials include:

- **Language:** Python
- **Deep learning:** PyTorch, Ultralytics YOLOv8
- **Model architectures:** ResNet18, ResNet50, Vision Transformer, YOLOv8s classification
- **Data / image processing:** OpenCV, Pandas, NumPy
- **Visualization and evaluation:** Matplotlib, scikit-learn
- **Training environment:** Google Colab with GPU
- **Dataset preparation:** Roboflow is referenced in the project methodology
- **Application/backend:** Mobile application and a FastAPI backend are part of the broader project workflow; include their source and exact setup only if those files are part of this repository.

## Repository Contents

A recommended public-repository structure is:

```text
SmartRad-XAI/
├── README.md
├── SmartRadXAI.ipynb
├── requirements.txt
├── backend/              # if backend source is included
├── mobile-app/           # if mobile source is included
├── screenshots/          # approved, non-sensitive screenshots only
├── results/              # metrics/plots that may be shared
└── .gitignore
```

This is a suggested layout. Keep only folders and files that actually exist in your project. Do not commit large datasets, private clinical records, credentials, local machine paths, or unnecessary generated files.

## Run the Notebook

The supplied notebook was written for Google Colab and expects files in Google Drive. Its original absolute paths will need to be updated to match your own folder structure.

1. Open the notebook in Google Colab.
2. Set the runtime to use a GPU if one is available.
3. Install the required packages:

   ```bash
   pip install ultralytics opencv-python pandas matplotlib scikit-learn
   ```

4. Obtain the NIH ChestX-ray14 data through its official/source page and organize only the five selected classes into class-wise directories.
5. Update dataset and model paths in the notebook. Replace paths such as `/content/drive/MyDrive/Disease classes` and the saved `best.pt` path with your own paths.
6. Run preprocessing, training, validation, and inference cells in order.

### Example YOLOv8s classification training command

The notebook includes this training configuration:

```bash
yolo task=classify mode=train \
  model=yolov8s-cls.pt \
  data="/path/to/Disease classes" \
  epochs=45 \
  imgsz=128 \
  batch=128 \
  patience=20 \
  device=0
```

Replace `/path/to/Disease classes` with your dataset directory. The directory must follow the class-folder structure expected by Ultralytics. Training from scratch may require a compatible GPU and significant memory; reduce batch size if your GPU runs out of memory.

### Inference example

```python
from ultralytics import YOLO

model = YOLO("path/to/best.pt")
results = model.predict(
    source="path/to/chest_xray.png",
    imgsz=128
)

result = results[0]
class_index = int(result.probs.top1)
predicted_class = result.names[class_index]
confidence = float(result.probs.top1conf)

print("Predicted class:", predicted_class)
print(f"Confidence: {confidence:.2%}")
```

Use the same preprocessing and input-size conventions as the trained model. A confidence score is the model's score for a class; it is not the probability that a patient truly has a disease.

## Training Configuration

The YOLOv8s notebook training command uses:

| Parameter | Value |
|---|---|
| Task | Classification |
| Model | `yolov8s-cls.pt` |
| Epochs | 45 |
| Image size | 128 |
| Batch size | 128 |
| Early stopping patience | 20 |
| Device | GPU (`device=0`) |

Other architectures were trained through separate workflows, so their training configurations are not identical.

## Limitations and Future Work

Known challenges and future improvements include:

- Similar radiographic patterns can lead to confusion among Pneumonia, Effusion, and Pneumothorax.
- Class imbalance can affect performance across categories.
- The project uses a subset of a public dataset; external generalization is not established by the reported accuracy alone.
- Dataset splitting, checkpoint selection, and metric calculation should be standardized and documented for reproducibility.
- Bounding-box annotations are available for only a subset of NIH images; localization visualizations should not be interpreted as validated lesion localization.
- Clinical evaluation should be expanded with a predefined protocol, appropriate permissions, larger independent cohorts, class-wise metrics, and expert review.
- Explainability methods and report generation should be documented with their exact implementation and limitations.
- Future work could include stronger calibration, external validation, robust input-quality checks, model monitoring, and a reproducible deployment pipeline.

## Team and Acknowledgements

**Project:** SmartRad-XAI  
**Department:** Computer Engineering, Bahria University Islamabad  
**Supervisor:** Dr. Amna Waheed

**Project team**
- Muhammad Waleed Asrar
- Abdullah Aamir
- Hameed Junior

The project materials acknowledge support from Islamabad Diagnostic Centre (IDC) during clinical case access, application testing, and comparison with radiology reports. Any public acknowledgement of individual staff members or use of IDC branding should follow the relevant permissions.

## Disclaimer and Data Privacy

This repository documents an academic AI/ML project. It is not a medical device and must not be used as the sole basis for clinical decisions. The model may produce incorrect predictions, and its confidence scores are not a substitute for professional interpretation.

Before making this repository public:
- Remove API keys, access tokens, passwords, private URLs, and personal credentials.
- Do not publish patient-identifiable images, reports, or clinical records.
- Confirm permissions and licensing for datasets, screenshots, application assets, and model weights.
- Keep large trained weights outside Git if necessary; link to them only where redistribution is permitted.
- Review all notebook outputs for private data and machine-specific paths.

---

If you use or build on this work, please cite the NIH ChestX-ray14 dataset and follow its applicable terms. This project was developed for academic learning and research.
