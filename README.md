# Camera-Based Intruder Detection System

## JLR x Amos Bursary Undergraduate Hackathon - 2nd Place Project

This repository contains the proof-of-concept for a camera-based intruder detection system developed during the JLR x Amos Bursary Undergraduate Hackathon in March 2025. Our team secured 2nd place with this innovative solution aimed at replacing ultrasonic sensors with existing interior cameras to reduce vehicle complexity and cost.

## Project Overview

The goal was to develop a system that leverages existing interior cameras in JLR vehicles to detect intruders, potentially replacing dedicated ultrasonic sensors. This approach aims to reduce sensor count, weight, and cost while maintaining or improving detection accuracy.

## Key Features

- Motion detection using OpenCV
- Object classification with custom-trained YOLOv8 Nano model
- Multi-camera fusion logic for improved accuracy
- Simulated alert system

## Technical Highlights

- Custom dataset creation and annotation (40+ simulated intrusion scenarios)
- Model training and preprocessing using Roboflow
- Basic multi-camera fusion implementation
- Edge case analysis and mitigation strategies

## Project Structure

```
├── intrusion_detector.ipynb  # Colab/Jupyter proof-of-concept notebook
├── LICENSE
└── README.md
```

The notebook contains the dependency installation, YOLO model loading, frame-difference motion detection, person detection, and intrusion logging demo code. If you export the notebook into scripts later, keep reusable detection code under a `src/` directory and trained weights under a `models/` directory.

## Setup and Installation

The current proof-of-concept is packaged as a Jupyter/Google Colab notebook (`intrusion_detector.ipynb`). The notebook installs the same Python packages it needs, but the steps below make the environment explicit for local development and repeatable demos.

### Prerequisites

- Python 3.10 or newer
- A webcam/video file or sample intrusion video to process
- Optional but recommended: NVIDIA GPU with CUDA support for faster YOLO inference
- Optional for local notebook use: JupyterLab

### Option 1: Run in Google Colab

1. Open `intrusion_detector.ipynb` in Colab using the badge at the top of the notebook.
2. Select **Runtime > Change runtime type** and choose a GPU runtime if available.
3. Run the dependency installation cell:

   ```python
   !pip install ultralytics opencv-python numpy albumentations torch torchvision
   ```

4. Upload a video when prompted by the notebook upload cell, or upload one manually to the Colab file browser.
5. Rename or update the sample path so the processing cell points to your file, for example `input_source_sample.mp4`.

### Option 2: Run locally

1. Clone the repository and enter it:

   ```bash
   git clone <repository-url>
   cd SecureDx
   ```

2. Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   # Windows PowerShell:
   # .venv\Scripts\Activate.ps1
   ```

3. Install the project dependencies used by the notebook:

   ```bash
   python -m pip install --upgrade pip
   python -m pip install ultralytics opencv-python numpy albumentations torch torchvision pillow ipython jupyterlab
   ```

4. Start JupyterLab and open the notebook:

   ```bash
   jupyter lab intrusion_detector.ipynb
   ```

5. Place your test video in the repository root, or update the `process_video(...)` call in the notebook with the correct path.

## Usage

### Quick notebook demo

The simplest way to run the detection system is from `intrusion_detector.ipynb`:

1. Install dependencies using the first notebook cell.
2. Confirm whether GPU acceleration is available with:

   ```python
   import torch
   print("GPU Available:", torch.cuda.is_available())
   ```

3. Load a YOLO model. For a pretrained lightweight model:

   ```python
   from ultralytics import YOLO
   model = YOLO("yolov8n.pt")
   ```

   If you have trained custom weights, update the model path used in the notebook:

   ```python
   model = YOLO("runs/detect/train/weights/best.pt")
   ```

4. Run detection on a video file:

   ```python
   process_video("input_source_sample.mp4")
   ```

When motion is detected, the notebook runs YOLO person detection on the frame. If a person is detected for the configured number of consecutive frames, an event is appended to `intrusion_log.txt`.

### Tuning detection behavior

The main parameters are defined near the top of the notebook detection cells:

```python
motion_threshold = 30        # Pixel-change threshold for frame differencing
frame_history = 3            # Consecutive detections required before alerting
confidence_threshold = 0.6   # Minimum YOLO confidence for person detection
```

Increase `confidence_threshold` to reduce false positives, decrease it to make detections more sensitive, and adjust `frame_history` to control how many consecutive person detections are required before logging an intrusion.

### Expected outputs

- Annotated video frames are displayed inline in the notebook.
- Intrusion events are written to `intrusion_log.txt` in the current working directory.
- Console output prints each intrusion event and a completion message when video processing finishes.

## Future Work

- Improve low-light performance
- Implement full 3D triangulation for precise intruder localization
- Integrate with vehicle's existing security systems

## Team

- [Don Aborah] - Computer Vision Lead
- [Sydney Silver]
- [Yosef Levine]
- [Winston Graham]

## Acknowledgments

Special thanks to JLR and the Amos Bursary for organizing this hackathon and providing us with this opportunity to innovate in automotive technology.
