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
├── data/
│   ├── images/
│   └── labels/
├── models/
│   └── yolov8n_custom.pt
├── src/
│   ├── motion_detection.py
│   ├── object_detection.py
│   └── alert_system.py
├── notebooks/
│   └── data_preprocessing.ipynb
├── docs/
│   └── technical_flowchart.png
└── README.md
```

## Setup and Installation

[Include instructions for setting up the project environment]

## Usage

[Provide examples of how to run the detection system]

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
