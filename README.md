# 🚨 Automated CCTV Violation Detection

## Project Overview

This project is an **AI-powered video analytics system** designed to automatically detect **violent behavior** in CCTV surveillance footage. It analyzes short video clips and classifies them as **Violent** or **Non-Violent** using a deep learning model that captures both **spatial** and **temporal** patterns in video data.

The system is intended for **smart city surveillance**, **public safety monitoring**, and **security analytics**, where early detection of violent activity can support faster human intervention.

---

## Key Objectives

* Detect violent activities from CCTV video clips
* Learn **motion patterns over time**, not just single-frame appearance
* Handle real-world video issues (short clips, missing frames, noisy data)
* Provide clear and interpretable prediction confidence

---

## System Architecture

### 1. Video Input

* Accepts short CCTV clips (MP4 / AVI)
* Each video is converted into a fixed-length sequence of frames

### 2. Preprocessing Pipeline

* Frame extraction using OpenCV
* Resize frames to **64 × 64**
* Convert BGR → RGB
* Normalize pixel values to range **[0, 1]**
* Pad or truncate clips to **16 frames**

Final input shape:

```
(1, 16, 64, 64, 3)
```

---

### 3. Deep Learning Model

The model combines **CNN-based spatial feature extraction** with **temporal sequence learning**:

* **MobileNetV2 (CNN)**

  * Extracts spatial features from each frame
  * Lightweight and efficient for video-based systems

* **TimeDistributed Wrapper**

  * Applies the same CNN to every frame independently

* **BiLSTM (Temporal Modeling)**

  * Captures motion dynamics and temporal dependencies
  * Learns how actions evolve across frames

* **Sigmoid Output Layer**

  * Outputs probability of violent activity

---

### 4. Prediction Logic

* Probability ≥ 0.5 → **Violent**
* Probability < 0.5 → **Non-Violent**
* Displays confidence score for transparency

---

## Application Workflow

1. User uploads a CCTV video clip
2. Frames are extracted and preprocessed
3. Preprocessed clip is passed to the trained model
4. Model predicts violence probability
5. Result and confidence score are displayed

---

## Project Structure

```
smart-city-violence-detection/
│
├── app.py                         # Streamlit application
├── violence_detection_model.keras # Trained deep learning model
├── notebooks/
│   └── training_pipeline.ipynb    # Model training & experimentation
├── data/                          # Sample or reference datasets
├── requirements.txt               # Dependencies
└── README.md
```

---

## Dataset

* CCTV-style surveillance videos
* Contains violent and non-violent scenarios
* Videos are split into fixed-length clips for training

> The system is designed to work even with **limited datasets** by using transfer learning and frame-level feature reuse.

---

## Technologies Used

* Python
* OpenCV
* NumPy
* TensorFlow / Keras
* Streamlit

---

## Model Strengths

* Handles variable video length robustly
* Efficient CNN backbone suitable for real-time scenarios
* Learns motion patterns instead of relying on single images
* Clean separation of preprocessing, inference, and UI

---

## Future Enhancements

* Multi-class violence categorization
* Violence localization (frame-level or bounding boxes)
* Integration with alerting systems
* Explainability using Grad-CAM
* Support for live camera streams

---

## Disclaimer

This project is intended **only as a decision-support system**. Final judgment and action should always involve human review.

---

## Author

**Salva**
Diploma in Data Science with Artificial Intelligence
