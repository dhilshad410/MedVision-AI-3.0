🧠 MedVision AI 3.0

Binary Brain MRI Classification – TUMOR vs NO TUMOR

"Python" (https://img.shields.io/badge/Python-3.10+-blue?logo=python)
"TensorFlow" (https://img.shields.io/badge/TensorFlow-Deep%20Learning-orange?logo=tensorflow)
"Gradio" (https://img.shields.io/badge/Gradio-UI-yellow?logo=gradio)
"Status" (https://img.shields.io/badge/Project-Academic%20Project-success)

📌 Project Overview

MedVision AI 3.0 is a Deep Learning-based Brain MRI Classification project that uses a Convolutional Neural Network (CNN) to classify brain MRI images into two categories:

- TUMOR – MRI images belonging to tumor categories.
- NO TUMOR – MRI images without tumors.

The project converts a four-class brain MRI dataset into a binary classification problem using TensorFlow and CNN.

It also provides a modern Gradio web interface where users can upload MRI images and view model predictions.

🎯 Project Objectives

- Develop a CNN-based brain MRI classification model.
- Classify MRI images into Tumor and No Tumor.
- Apply image preprocessing and data augmentation.
- Improve training using class weights.
- Evaluate model performance using classification metrics.
- Build an interactive Gradio interface.

📂 Dataset

Dataset Name: Brain Tumor MRI Dataset

Dataset Source: Kaggle

https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset

Original dataset contains four categories:

1. Glioma
2. Meningioma
3. No Tumor
4. Pituitary

These four categories are converted into two binary classes:

Original Category| Binary Category
Glioma| TUMOR
Meningioma| TUMOR
Pituitary| TUMOR
No Tumor| NO TUMOR

🏗️ Project Structure

MedVision_AI_3.0/
│
├── Training/
│   ├── glioma/
│   ├── meningioma/
│   ├── notumor/
│   └── pituitary/
│
├── Testing/
│   ├── glioma/
│   ├── meningioma/
│   ├── notumor/
│   └── pituitary/
│
├── MedVision_AI_3.0/
│   ├── medvision_binary.keras
│   ├── class_names.json
│   ├── training_graph.png
│   └── confusion_matrix.png
│
├── README.md
└── requirements.txt

⚙️ Technologies Used

Technology| Purpose
Python| Programming Language
TensorFlow| Deep Learning
Keras| CNN Model Development
NumPy| Numerical Operations
Matplotlib| Data Visualization
Seaborn| Confusion Matrix
Scikit-learn| Model Evaluation
Pillow| Image Processing
Gradio| Web Interface

🧠 CNN Architecture

The project uses a custom Convolutional Neural Network.

Model Architecture:

1. Input Layer – 180 × 180 × 3
2. Rescaling Layer
3. Data Augmentation
4. Convolutional Layer – 32 Filters
5. Batch Normalization
6. Max Pooling
7. Convolutional Layer – 64 Filters
8. Batch Normalization
9. Max Pooling
10. Convolutional Layer – 128 Filters
11. Batch Normalization
12. Max Pooling
13. Convolutional Layer – 256 Filters
14. Batch Normalization
15. Max Pooling
16. Global Average Pooling
17. Dense Layer – 128 Neurons
18. Dropout – 0.45
19. Output Layer – Sigmoid Activation

🔧 Model Configuration

Parameter| Value
Image Size| 180 × 180
Batch Size| 32
Epochs| 20
Optimizer| Adam
Learning Rate| 0.0001
Loss Function| Binary Crossentropy
Activation Function| ReLU, Sigmoid
Output Classes| 2
Random Seed| 42

✨ Key Features

- Binary Brain MRI Classification
- Custom CNN Architecture
- Automatic Dataset Folder Detection
- Image Preprocessing
- Data Augmentation
- Class Weight Balancing
- Training and Validation
- Accuracy and Loss Graphs
- Confusion Matrix
- Classification Report
- Interactive Gradio Interface
- 50 Sample MRI Images

📊 Model Evaluation

The model is evaluated using:

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix

Training graphs and confusion matrix are saved in the output directory.

Actual performance values should be added after completing model training and testing.

🚀 Installation and Setup

1. Clone the Repository

git clone https://github.com/YOUR-USERNAME/MedVision-AI-3.0.git

2. Open Project Folder

cd MedVision-AI-3.0

3. Install Dependencies

pip install tensorflow gradio scikit-learn matplotlib seaborn pillow numpy

4. Download Dataset

Download the Brain Tumor MRI Dataset from Kaggle:

https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset

Extract the dataset and make sure the "Training" and "Testing" folders are available.

5. Run the Project

Open the Python notebook in Google Colab or Jupyter Notebook and execute the cells after configuring the dataset path.

Important: Complete the model training step before running evaluation and Gradio prediction. The training code should define the "history" variable and save the trained model.

🖥️ Gradio Interface

The project includes an interactive web interface.

Users can:

1. Upload a Brain MRI image.
2. Click the Analyze MRI button.
3. View the predicted category.
4. Check the prediction score.
5. Try sample MRI images.

📸 Screenshots

Add your actual project screenshots here after running the application.

![MedVision AI Interface](screenshots/interface.png)

![Training Accuracy](screenshots/training_graph.png)

![Confusion Matrix](screenshots/confusion_matrix.png)

⚠️ Disclaimer

MedVision AI 3.0 is an educational and academic Deep Learning project.

It is not a clinically validated medical diagnostic system. Its predictions should not be used to make medical decisions. Actual MRI scans must be interpreted by qualified medical professionals.

🔮 Future Improvements

- Improve classification performance.
- Experiment with transfer learning models such as VGG16 and ResNet50.
- Add explainable AI using Grad-CAM.
- Improve the user interface.
- Evaluate the model on independent MRI datasets.

👨‍💻 Project Information

Project Name: MedVision AI 3.0

Project Domain: Deep Learning / Medical Image Classification

Project Type: Academic Project

Student: Muhammed Dhilshad

Course: Data Science – B1

Institution: TRYCOD Tech School, Perinthalmanna

Guide/Mentor: Faizal

---

⭐ If you find this project interesting, consider giving this repository a star!

Developed as part of a Data Science and Deep Learning academic project.
