# Audio Deepfake Detection

This project is an audio deepfake detection system that combines three complementary approaches to detect manipulated audio. The system allows users to upload audio files through a web interface and receive real-time predictions on whether the audio is genuine or deepfake with confidence scores.

## Architecture

The system uses a three-module ensemble system:

1.  **AntiDeepfake Module (Primary Detector)**: Uses a pre-trained wav2vec2 or HuBERT model fine-tuned on the ASVspoof2019 dataset.
2.  **SafeEar Module (Acoustic Features)**: Extracts basic acoustic features like pitch, energy, MFCCs, and spectral features to train a simple classifier.
3.  **CodecFake Enhancement (Robustness)**: Applies data augmentation using audio codecs during training to make the model robust to real-world audio quality.

A simple fusion mechanism averages the probabilities from the three modules to produce the final prediction.

## Project Structure

```
├── backend
│   ├── api
│   │   └── endpoints.py
│   ├── core
│   │   └── config.py
│   ├── main.py
│   ├── models
│   │   ├── antideepfake
│   │   │   └── model.py
│   │   └── safeear
│   │       └── model.py
│   ├── services
│   │   └── fusion.py
│   └── utils
│       └── audio.py
├── data
│   └── raw
├── frontend
│   ├── css
│   │   └── style.css
│   ├── js
│   │   └── script.js
│   └── index.html
├── scripts
│   ├── train_antideepfake.py
│   └── train_safeear.py
├── requirements.txt
└── README.md
```

## Setup

1.  Install the required packages:
    ```
    pip install -r requirements.txt
    ```
2.  Download the dataset from [here](https://datashare.ed.ac.uk/bitstream/handle/10283/3336/LA.zip?sequence=3&isAllowed=y) and place it in the `data/raw` directory.
3.  Train the models:
    ```
    python scripts/train_antideepfake.py
    python scripts/train_safeear.py
    ```
4.  Run the backend server:
    ```
    uvicorn backend.main:app --reload
    ```
5.  Open the `frontend/index.html` file in your browser.
