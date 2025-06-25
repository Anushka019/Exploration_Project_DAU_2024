# 🦴 TKR 3D Tracking and Visualization System

## Overview

This project implements a real-time ArUco marker-based 3D tracking and visualization system tailored for use in **Total Knee Replacement (TKR)** surgeries. It uses **OpenCV** for camera calibration and marker detection, and **PyVista** for real-time rendering and pose tracking of anatomical bone models.

By detecting spatial movement of physical markers, it synchronizes and aligns corresponding STL-format 3D models in the virtual space, enabling accurate intraoperative feedback.

---

## 🎯 Purpose

To assist orthopedic surgeons in TKR procedures by:
- Precisely tracking surgical tools or bones using ArUco markers.
- Visualizing STL-based anatomical models in real-time.
- Measuring relative distances and positions between key landmarks.
- Providing an easily configurable system using JSON and calibration inputs.

---

## Key Features

- ✅ Real-Time ArUco Marker Tracking  
  Detects multiple markers using a live webcam feed with accurate pose estimation.

- ✅ 3D Model Alignment and Control  
  Maps each marker to a corresponding 3D model (e.g., bone or implant), ensuring alignment between physical movement and digital visualization.

- ✅ Pivot Point Projection  
  Projects a pivot offset point (e.g., 5 cm along a diagonal) for a given marker, aiding in identifying anatomical reference points during surgery.

- ✅ Distance Measurement Between Markers  
  Computes and logs real-time 3D distances between markers (e.g., femur and tibia alignment in TKR).

- ✅ Camera Calibration Integration  
  Uses intrinsic parameters (cameraMatrix.pkl, dist.pkl) to correct distortion and improve tracking accuracy.

- ✅ Configuration with JSON  
  Easily map markers to models and adjust settings like scale, orientation, and texture in config.json.

- ✅ Multithreaded Video Processing  
  Separates frame capture from processing to ensure low-latency, real-time performance.
  
- ✅ High-Resolution 3D Rendering  
  STL bone models rendered interactively using PyVista with texture mapping and dynamic camera positioning.

---

## 🧠 Technologies Used

- Languages: Python
- Libraries: OpenCV, ArUco, PyVista, NumPy, pandas, JSON  
- Visualization: STL, real-time PyVista plotter  
- Tools: JSON-configurable pipeline, Excel export (via pandas)

---

## 📁 File Structure

| File                        | Description                                                     |
|-----------------------------|-----------------------------------------------------------------|
| markerNBone.py              | Main script for marker detection, pose estimation, STL alignment |
| cameraCalibration.py        | Generates camera calibration files                              |
| config.json                 | Stores marker-to-model mappings and transformation parameters   |
| Femur.stl                   | Example 3D bone model used for testing                          |
| marker_distances.xlsx       | Automatically generated distance logs between markers           |
| aruco_marker.png            | ArUco marker image used in real-world tracking                  |
| cameraMatrix.pkl, dist.pkl  | Camera calibration matrices                                     |
| interactivePyramidModel.py  | Alternate visualization with procedural geometry (no STL)       |

---

## ⚙️ Configuration

Calibration must be completed using cameraCalibration.py if no cameraMatrix.pkl and dist.pkl are available.  
Marker-model relationships and display parameters (e.g., marker size, window size, plotter config) are defined in config.json.

Example JSON structure:

{
  "marker_model_map": {
    "0": "cuboid_model_1",
    "1": "cuboid_model_2"
  },
  "models": {
    "bone_model": {
      "file": "Femur.stl",
      "scale_factor": 1.0
    }
  }
}

---

## Dependencies

Install the required libraries using pip:

pip install opencv-python numpy pyvista pandas openpyxl

---

## How to Run

1. Clone the repository:
   git clone https://github.com/Anushka019/Exploration_Project_DAU_2024 
   cd TKR_3D_Tracker

2. Calibrate your camera:
   python cameraCalibration.py

3. Start the system:
   python markerNBone.py

4. Interact:
   - Hold the printed ArUco marker in front of the camera.
   - Watch the corresponding STL bone model move in real time.
   - Press q to quit.
   - Press d to display and freeze a pivot point in the scene.

---

## Live Feedback & Output

- Distance logs between Marker 0 and Marker 1 are saved in:
  marker_distances.xlsx

- These logs include:
  - 3D position differences (x, y, z)
  - Euclidean distance (in cm)

---

## Demonstration Workflow

1. Display Marker 0 and Marker 1 in front of your camera.  
2. Observe STL models moving and aligning in the 3D viewer.  
3. Pivot Point will be projected (if enabled) for Marker 1.  
4. Excel log of relative position and distance between the markers is continuously updated.

---

## Sample Output

- ✅ Bone model rotates and moves with real-world marker.  
- ✅ Textured cuboids(virtual ArUco marker model) follow marker IDs.  
- ✅ Red dot (pivot) appears offset from Marker 1's diagonal.  
- ✅ Distance between markers is printed and saved.

---

## ✅ Applications

- Pre-operative planning for TKR  
- Surgical tool alignment  
- Training systems for orthopedic procedures  
- Marker-based augmented reality in medical visualization
