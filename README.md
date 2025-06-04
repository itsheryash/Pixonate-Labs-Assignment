# 🛠️ Bearing Defect Detection using YOLOv8 & CNN

This repository contains code and workflows for detecting and classifying defects in bearing images using both **YOLOv8 (for object detection)** and **CNN (for classification)**.

The dataset contains **high-resolution images** of bearings — some with **visible defects (e.g., dents, notches, scratches)** and some **normal**. The goal is to identify whether an image contains a defect and classify it accordingly.

---

## 📂 Project Structure

├── Yolo_to_Csv.py # Converts YOLOv8 annotation format (from Roboflow) to CSV for CNN usage
├── labels.csv # Output file from Yolo_to_Csv: contains filename and label columns
├── labels/ # Folder containing image filenames and their class labels (Normal or Defect)
├── Yolo_train.py # YOLOv8 training script for defect detection
├── CNN_Training.py # CNN training script from scratch for binary classification

---

## 🚀 Workflow Overview

### 1. **Image Annotation using Roboflow**
- Images were uploaded and annotated in [Roboflow](https://roboflow.com/).
- Annotations were exported in YOLOv8 format (`.txt` for each image).

---

### 2. **Annotation Conversion for CNN**
- The script `Yolo_to_Csv.py` parses YOLO-format annotations.
- For each image:
  - If any annotation exists → `label = defect`
  - If no annotation exists → `label = normal`
- Result: `labels.csv` with two columns:
  - `filename` – image filename
  - `label` – `"defect"` or `"normal"`

---

### 3. **Object Detection with YOLOv8**
- `Yolo_train.py` trains a YOLOv8 model using the annotated dataset.
- Purpose: detect bounding boxes around defect areas in bearings.

---

### 4. **Classification using CNN**
- `CNN_Training.py` builds and trains a **CNN from scratch** using TensorFlow/Keras.
- It uses the `labels.csv` file for supervised binary classification:
  - **Input**: bearing image
  - **Output**: `"defect"` or `"normal"`

---

## 🧠 Models Compared

| Model        | Task              | Strengths                            |
|--------------|-------------------|---------------------------------------|
| YOLOv8       | Object Detection  | Localizes and identifies defect areas |
| CNN (Scratch)| Classification    | Lightweight, classifies entire image  |

---

## 📊 Example Entry from `labels.csv`

| filename       | label   |
|----------------|---------|
| bearing_001.jpg| defect  |
| bearing_002.jpg| normal  |


## Dependencies include:

1. ultralytics (for YOLOv8)
2. tensorflow
3. pandas
4. opencv-python
