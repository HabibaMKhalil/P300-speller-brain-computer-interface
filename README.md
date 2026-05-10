# P300 Speller BCI System
---

## Overview

A Brain-Computer Interface (BCI) that decodes EEG signals to spell characters using the P300 paradigm. The system reads raw EEG data recorded while a subject focuses on characters in a 6×6 speller matrix, classifies which row and column the subject was attending to, and reconstructs the intended word/sentence.

---

## How It Works

1. **EEG Acquisition** — 64-channel EEG signals recorded at 240 Hz (BCI Competition dataset, Subject A)
2. **Bandpass Filtering** — 4th-order Butterworth filter (1–15 Hz) removes drift and muscle noise
3. **Epoch Extraction** — EEG segments are windowed around each row/column flash event (−0.2s to +0.8s)
4. **CSP Feature Extraction** — Common Spatial Patterns reduces 64-channel epochs to discriminative spatial features
5. **LDA Classification** — Linear Discriminant Analysis predicts the probability that each flash is a P300 target
6. **Character Decoding** — Probabilities are aggregated across 12 flashes per character (6 rows + 6 columns); highest-scoring row and column pinpoint the intended character
7. **GUI Visualization** — A tkinter window displays the 6×6 speller matrix with animated row/column flashing and shows the decoded sentence in real time

---

## Project Structure

```
├── P300 Speller BCI System.ipynb        # Main notebook (full pipeline + GUI)
├── Project Task.pdf                     # Assignment specification
└── dataset/
    ├── Subject_A_Train_Signal.txt        # Training EEG signals (channels × time)
    ├── Subject_A_Train_Flashing.txt      # Flashing events (train)
    ├── Subject_A_Train_StimulusCode.txt  # Row/column codes (train)
    ├── Subject_A_Train_StimulusType.txt  # Target / non-target labels (train)
    ├── Subject_A_Train_TargetChar.txt    # Ground-truth characters (train)
    ├── Subject_A_Test_Signal.txt         # Testing EEG signals
    ├── Subject_A_Test_Flashing.txt       # Flashing events (test)
    ├── Subject_A_Test_StimulusCode.txt   # Row/column codes (test)
    ├── output_real.txt                   # Decoded sentence output
    └── readme.txt                        # Dataset format description
```

---

## Requirements

```
numpy
scipy
scikit-learn
tkinter  (included with standard Python)
```

Install dependencies:

```bash
pip install numpy scipy scikit-learn
```

---

## Usage

1. Clone the repo and place the `dataset/` folder in the project root
2. Open `P300 Speller BCI System.ipynb` in Jupyter
3. Update the `dataset_dir` path in the second cell to match your local path
4. Run all cells sequentially
5. In the GUI window, press **Space** to step through character decoding one letter at a time

---

## Speller Matrix

```
A  B  C  D  E  F
G  H  I  J  K  L
M  N  O  P  Q  R
S  T  U  V  W  X
Y  Z  1  2  3  4
5  6  7  8  9  0
```

---

## Pipeline Summary

```
Raw EEG → Bandpass Filter → Epoch Extraction → CSP → LDA → Decode → GUI
```
