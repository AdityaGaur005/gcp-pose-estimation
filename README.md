# 🛰️ Aerial GCP Keypoint Detection & Shape Classification

This project focuses on detecting **Ground Control Points (GCPs)** from aerial imagery and predicting:

* 📍 **Precise keypoint location** `(x, y)`
* 🔷 **Shape classification** of the marker

The model processes aerial images and outputs predictions in the exact JSON format required for evaluation.

---

# 📌 Project Overview

Ground Control Points (GCPs) are visible markers placed on the ground to help align aerial imagery with geographic coordinates.

The goal of this project is to build a deep learning model that:

1. Detects the **center location of the GCP marker**
2. Classifies the **shape of the marker**

The predictions are evaluated using:

* **Percentage of Correct Keypoints (PCK)** for localization accuracy
* **Macro F1-score** for shape classification

---

# 🧠 Model Architecture

The model is designed as a **multi-task neural network** that performs both:

* **Keypoint regression**
* **Shape classification**

### Architecture Components

| Component           | Purpose                                     |
| ------------------- | ------------------------------------------- |
| CNN Backbone        | Extract spatial features from aerial images |
| Regression Head     | Predict `(x, y)` coordinates of the marker  |
| Classification Head | Predict marker shape                        |

The model outputs:

* **Keypoint coordinates:** `(x, y)`
* **Shape class:** `Circle`, `Square`, or `Triangle`

This design allows the model to learn both **spatial localization** and **object classification simultaneously**.

---

# ⚙️ Training Strategy

The training pipeline includes several techniques to improve model performance and robustness.

### 📊 Data Processing

* Images resized to a consistent resolution
* Normalization applied for stable training
* Custom dataset loader for image + annotation handling

### 🔄 Data Augmentation

To improve generalization the following augmentations were applied:

* Horizontal flips
* Random rotations
* Color jittering
* Scaling transformations

These augmentations help the model become robust to **orientation and lighting variations** present in aerial imagery.

### 🎯 Loss Functions

Since the task is multi-objective:

| Task                  | Loss Function            |
| --------------------- | ------------------------ |
| Keypoint localization | Mean Squared Error (MSE) |
| Shape classification  | Cross Entropy Loss       |

The final loss is a combination of both objectives.

---

# 📈 Evaluation Metrics

The model is evaluated using two key metrics.

### 1️⃣ Localization Accuracy (PCK)

Percentage of Correct Keypoints measures whether predicted coordinates fall within a threshold distance of the ground truth.

Thresholds used:

* **10 pixels**
* **25 pixels**
* **50 pixels**

### 2️⃣ Classification Accuracy

Measured using **Macro F1 Score** across the three classes:

* Circle
* Square
* Triangle

---

# 🚧 Challenges Encountered

### 1️⃣ Small Object Size

GCP markers occupy a very small region of the aerial image, making localization difficult.

**Solution**

High resolution images and careful feature extraction were used to preserve spatial details.

---

### 2️⃣ Shape Similarity

Some shapes appear visually similar at high altitude.

**Solution**

The classification head was trained jointly with localization to allow shared spatial features to improve discrimination.

---

### 3️⃣ Dataset Variability

Different lighting conditions and camera angles introduced variability.

**Solution**

Data augmentation techniques were applied to improve generalization.

---

# 📂 Repository Structure

```
gcp-keypoint-detection/
│
├── data/
│
├── models/
│
├── src/
│   └── pose_estimation.ipynb
│
├── outputs/
│   └── predictions.json
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## 📂 Dataset

The dataset used in this project was provided as part of the assignment.

Download it from:

https://drive.google.com/drive/folders/1RDNiAO1EynKrRDomcVNXQW1-ct5zzvE5?usp=drive_link

After downloading, place the dataset in the following directory structure:

data/
   train_dataset/
   test_dataset/

   
# 📦 Model Weights

The trained model weights are provided separately due to file size limitations.

Download them from the link below:

👉 **Model Download Link**

https://drive.google.com/drive/folders/1QNptSo8IkHIebVF84vOpNIAEa-cw9I5g?usp=drive_link


After downloading, extract the zip file and place the model inside the project directory as follows:

```
models/best_model.pth
```

---

# 🧪 Running Inference

To reproduce the predictions:

### Step 1 — Install dependencies

```
pip install -r requirements.txt
```

---

### Step 2 — Download the model weights

Download the model from the link above and place it in:

```
models/best_model.pth
```

---

### Step 3 — Run inference

Run the notebook:

```
src/pose_estimation.ipynb
```

This notebook will:

1. Load the trained model
2. Run inference on the **test dataset**
3. Generate the prediction file

---

### Step 4 — Output

The final predictions file will be generated as:

```
outputs/predictions.json
```

This file follows the same format as the training annotations.

Example:

```json
{
 "image_name.jpg": {
    "mark": {
        "x": 3276.21,
        "y": 1537.19
    },
    "verified_shape": "Square"
 }
}
```

---

# 🧰 Requirements

Dependencies used in the project include:

```
torch
torchvision
numpy
opencv-python
matplotlib
tqdm
pandas
```

Install them using:

```
pip install -r requirements.txt
```

---

# 📊 Final Output

The submission includes:

✅ Codebase
✅ Trained model weights (via download link)
✅ Generated `predictions.json` file
✅ Documentation explaining the approach

---

# ✨ Future Improvements

Potential improvements include:

* Using **advanced backbones (ResNet / EfficientNet)**
* Applying **heatmap-based keypoint detection**
* Incorporating **attention mechanisms**
* Training with **larger augmented datasets**

---

# 👨‍💻 Author

**Aditya Gaur**

B.Tech Student
Cloud & AI Enthusiast
