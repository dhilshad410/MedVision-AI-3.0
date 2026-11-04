# MedVision AI 3.0

**Brain MRI binary classification: TUMOR vs NO TUMOR**

MedVision AI 3.0 is a convolutional neural network (CNN) built with TensorFlow/Keras that looks at a brain MRI slice and predicts whether it shows a tumor or not. The project also ships with a Gradio web app, so anyone can upload an MRI image and see the model's prediction scores.

> **Disclaimer:** This is an educational deep-learning project. It cannot diagnose or rule out a brain tumor. Real MRI scans must always be assessed by a qualified radiologist.

---

## Table of contents

- [Overview](#overview)
- [Results](#results)
- [Dataset](#dataset)
- [Model architecture](#model-architecture)
- [Training setup](#training-setup)
- [Project structure](#project-structure)
- [Getting started](#getting-started)
- [Using the web app](#using-the-web-app)
- [Limitations](#limitations)
- [Future work](#future-work)
- [Author](#author)

---

## Overview

The original Brain Tumor MRI dataset has four classes: `glioma`, `meningioma`, `pituitary` and `notumor`. This project turns it into a two-class problem:

| Original class | Binary label |
|---|---|
| glioma | 1 (TUMOR) |
| meningioma | 1 (TUMOR) |
| pituitary | 1 (TUMOR) |
| notumor | 0 (NO TUMOR) |

Pipeline in one line: **load images, relabel to binary, rescale and augment, train CNN with class weights, evaluate on the held-out test set, serve with Gradio.**

---

## Results

Evaluated on the dataset's `Testing` folder (1,600 images), which is never used during training or validation.

| Metric | Value |
|---|---|
| Accuracy | 93.8% (1,500 of 1,600 correct) |
| TUMOR precision | 99.6% |
| TUMOR recall | 92.1% |
| NO TUMOR recall | 98.8% |
| False alarms (NO TUMOR predicted as TUMOR) | 5 |
| Missed tumors (TUMOR predicted as NO TUMOR) | 95 |

### Confusion matrix

![Confusion matrix](assets/confusion_matrix.png)

### Training curves

![Training and validation accuracy and loss](assets/training_graph.png)

Training and validation curves converge at roughly 0.97 to 0.98 accuracy, with no sign of heavy overfitting.

**Key takeaway:** the model rarely raises false alarms, but it misses about 8% of tumor images. Improving TUMOR recall is the main goal for future versions.

---

## Dataset

- **Name:** Brain Tumor MRI Dataset (four-class version, with `Training` and `Testing` folders)
- **Classes:** glioma, meningioma, notumor, pituitary
- **Split used here:** 80% of `Training` for training, 20% of `Training` for validation, and the whole `Testing` folder for the final evaluation
- **Image size:** resized to 180 x 180 RGB

Expected folder layout:

```
Brain Tumor MRI Dataset/
├── Training/
│   ├── glioma/
│   ├── meningioma/
│   ├── notumor/
│   └── pituitary/
└── Testing/
    ├── glioma/
    ├── meningioma/
    ├── notumor/
    └── pituitary/
```

The dataset is **not** included in this repository. Download it yourself and point the script to it (see [Getting started](#getting-started)).

---

## Model architecture

A compact four-block CNN with a single sigmoid output.

| Stage | Layers |
|---|---|
| Input | 180 x 180 x 3 |
| Preprocessing | Rescaling (1/255) |
| Augmentation | RandomRotation (0.04), RandomZoom (0.08), RandomContrast (0.08) |
| Block 1 | Conv2D 32 (3x3, ReLU) + BatchNorm + MaxPool |
| Block 2 | Conv2D 64 (3x3, ReLU) + BatchNorm + MaxPool |
| Block 3 | Conv2D 128 (3x3, ReLU) + BatchNorm + MaxPool |
| Block 4 | Conv2D 256 (3x3, ReLU) + BatchNorm + MaxPool |
| Head | GlobalAveragePooling2D, Dense 128 (ReLU), Dropout 0.45 |
| Output | Dense 1 (sigmoid): close to 0 = NO TUMOR, close to 1 = TUMOR |

---

## Training setup

| Setting | Value |
|---|---|
| Optimizer | Adam, learning rate 0.0001 |
| Loss | Binary cross-entropy |
| Max epochs | 20 |
| Batch size | 32 |
| Random seed | 42 |
| Class balancing | Class weights = total images / (2 x images in that class) |
| Callbacks | ModelCheckpoint (best `val_loss`), EarlyStopping (patience 5, restore best weights), ReduceLROnPlateau (factor 0.5, patience 2) |

---

## Project structure

```
MedVision-AI-3.0/
├── medvision_ai.py          # full pipeline: data, model, training, evaluation, Gradio app
├── assets/
│   ├── confusion_matrix.png
│   └── training_graph.png
├── MedVision_AI_3.0/        # created when you run the script
│   ├── medvision_binary.keras   # best saved model
│   ├── class_names.json
│   ├── training_graph.png
│   └── confusion_matrix.png
└── README.md
```

---

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/MedVision-AI-3.0.git
cd MedVision-AI-3.0
```

### 2. Create a virtual environment (recommended)

```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install tensorflow numpy matplotlib seaborn scikit-learn gradio
```

### 4. Set the dataset path

Open `medvision_ai.py` and change this line to the folder where you saved the dataset:

```python
DATASET_DIR = Path(r"C:\Users\YourName\Downloads\Brain Tumor MRI Dataset")
```

### 5. Run

```bash
python medvision_ai.py
```

The script will:

1. Check that all dataset folders exist and print image counts
2. Convert the four classes into two
3. Train the CNN and save the best model to `MedVision_AI_3.0/medvision_binary.keras`
4. Save the training graph and confusion matrix
5. Print test accuracy and a classification report
6. Launch the Gradio web app

---

## Using the web app

When training finishes, Gradio starts a local server and prints a link (usually `http://127.0.0.1:7860`).

1. Open the link in your browser
2. Upload a brain MRI image
3. Click **Analyze MRI**
4. Read the TUMOR and NO TUMOR scores and the result message

The app resizes the image to 180 x 180, runs the saved model, and shows both probabilities. A tumor score of 0.5 or higher is reported as "TUMOR PREDICTED".

---

## Limitations

- Trained and tested on a single public dataset, so results may not carry over to scans from other scanners or hospitals
- Works on single 2D slices, not full 3D MRI volumes
- Misses some tumors (recall 92.1%), so it must not be used to rule out a tumor
- Binary output only: it does not say which tumor type is present
- Educational project, not a medical device

---

## Future work

- Transfer learning with pretrained models (for example ResNet or EfficientNet)
- Grad-CAM heatmaps to show which image regions drive each prediction
- Threshold tuning to raise TUMOR recall
- Validation on external MRI data
- Return to the four-class problem (glioma, meningioma, pituitary, no tumor)

---

## Author

**Muhammed Dhilshad P**
Data Science, Batch B1, Trycod

Guided by **Faizel** and **Fathima**.

---

## License

Add a license of your choice (for example MIT) before publishing. Remember that the dataset has its own license and terms, so check them before redistributing any images.
