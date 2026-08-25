# Lightweight ECG Signal Classification

## MSc Data Science Dissertation Project

An end-to-end machine learning and deep learning project investigating ECG-based classification of Wake and Sleep physiological states from wearable ECG recordings.

The project compares traditional feature-based machine learning models with waveform-based deep learning approaches and investigates model optimisation through pruning and post-training quantisation.

---

## Project Overview

The aim of this project was to develop and evaluate machine learning models capable of distinguishing Wake and Sleep states from ECG signals while investigating ways to make the final model more computationally efficient.

The project followed a complete pipeline:

**ECG data → preprocessing → feature engineering → model development → model comparison → CNN optimisation → final evaluation**

---

## Dataset

The project uses the Dryad 24-hour physiological monitoring dataset.

The study included:

- 30 participants
- 58 ECG recordings
- 250 Hz ECG sampling rate
- 10-second ECG windows
- 2,500 samples per window
- 50% window overlap

The raw dataset is not included in this repository.

---

## Data Preprocessing

The ECG recordings were inspected and processed before modelling.

The preprocessing pipeline included:

- ECG signal quality assessment
- Band-pass filtering
- Signal windowing
- Wake/Sleep annotation matching
- Participant-level train/validation/test separation

A 0.5–40 Hz Butterworth band-pass filter was used to reduce unwanted frequency components.

---

## Feature Engineering

For the traditional machine learning models, statistical features were extracted from the ECG windows.

The feature set included:

- Mean
- Standard deviation
- Minimum
- Maximum
- Range
- Median
- Interquartile range
- Root mean square
- Signal energy

These features were used as inputs to the traditional machine learning models.

---

## Models Evaluated

Four modelling approaches were investigated:

### Traditional Machine Learning

- Logistic Regression
- Linear Support Vector Machine (SVM)

### Deep Learning

- Convolutional Neural Network (CNN)
- Long Short-Term Memory (LSTM)

The traditional models used engineered statistical features, while the CNN and LSTM models operated on the ECG waveform representation.

---

## Model Comparison

The models were evaluated using participant-level validation to reduce the risk of data leakage between individuals.

The lightweight CNN achieved the strongest validation performance among the evaluated models.

| Model | Validation F1 |
|---|---:|
| Logistic Regression | 0.1403 |
| Linear SVM | 0.1305 |
| Lightweight CNN | 0.7932 |
| LSTM | 0.4947 |

Based on the validation results, the lightweight CNN was selected for further optimisation.

---

## CNN Optimisation

The selected CNN was investigated for computational efficiency using:

- Magnitude-based pruning
- Different sparsity levels
- Post-training dynamic-range quantisation

The purpose was to reduce model storage and prediction time while maintaining comparable predictive performance.

### Quantisation Results

| Metric | Original CNN | Quantised CNN |
|---|---:|---:|
| Model storage | 14.88 KB | 9.80 KB |
| Prediction time | 51.09 s | 27.69 s |
| Validation F1 | 0.7932 | 0.7888 |

The quantised model reduced measured model storage by approximately 34% and prediction time by approximately 46%, while maintaining similar validation performance.

---

## Final Evaluation

The final quantised CNN was evaluated on five previously unseen participants.

The final evaluation achieved:

- Accuracy: 0.6569
- Precision: 0.8993
- Recall: 0.6258
- F1-score: 0.7380
- ROC-AUC: 0.7736

These results demonstrate the potential of the lightweight CNN approach while also highlighting the challenges of generalising ECG-based physiological-state classification across unseen participants.

---

## Repository Structure

```text
lightweight-ecg-signal-classification/
│
├── 01_dataset_exploration.ipynb
├── 02_ecg_preprocessing.ipynb
├── 03_wakesleep_labels_feature_engineering.ipynb
├── 04_model_development_and_evaluation.ipynb
├── 05_Lightweight_CNN_Optimisation.ipynb
├── 06_Final_Analysis_and_Interpretation.ipynb
│
├── MSc_Dissertation_Lightweight_ECG_Classification.pdf
├── MSc_Project_Presentation.pptx
│
└── README.md
