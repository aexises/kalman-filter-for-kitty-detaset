# kalman-filter-for-kitty-detaset
# Kalman Filter for GPS/IMU Sensor Fusion using KITTI Dataset

## Project Overview

This project demonstrates **sensor fusion using a Linear Kalman Filter** to estimate traveled distance by combining **GPS measurements** and **IMU acceleration data**.

The experiment uses the **KITTI dataset**, specifically the **OXTS sensor data**, which contains synchronized **GNSS (GPS)** and **IMU** measurements.

The goal is to compare:

- Distance measured directly from **GPS**
- Distance estimated using a **Kalman Filter**

The Kalman Filter reduces GPS noise and produces a smoother and more reliable distance estimation.

---

# Dataset

The project uses the **KITTI Vision Benchmark Suite** dataset.

Official website:  
https://www.cvlibs.net/datasets/kitti/index.php

Google Drive (dataset provided for the assignment):  
https://drive.google.com/drive/folders/1PsmBbRxVXZ7KeNohnBifpS6hnAXkhSFW

Dataset structure used in this project:

data/
│
├── velodyne/
│   └── 0000000000.bin        # LiDAR point cloud
│
└── oxts/
└── data/
0000000000.txt    # GPS + IMU data
0000000001.txt
…

Each **OXTS file** contains:

- Latitude
- Longitude
- Altitude
- Roll / Pitch / Yaw
- Velocities
- Linear acceleration (IMU)

---

# Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- Open3D
- Jupyter Notebook

---

# Project Structure

kalman-kitti/
│
├── kalman_kitti.ipynb     # Main notebook with implementation
├── kf_results.csv         # Output results
├── README.md              # Project description
└── data/                  # KITTI dataset

---

# Implementation Steps

## 1. Load KITTI Data

OXTS files are loaded and parsed to extract:

- GPS coordinates (latitude, longitude)
- IMU accelerations

---

## 2. Compute Distance from GPS

Distance is computed using the **Haversine formula**, which converts latitude and longitude coordinates into meters.

This gives the **raw GPS distance measurement**.

---

## 3. Estimate Sensor Noise

Two noise parameters are estimated:

### Accelerometer noise (`std_acc`)

Estimated from a segment where the vehicle is assumed to be static or moving at constant speed.

### GPS measurement noise (`std_meas`)

Estimated from the spread of GPS measurements when stationary or using typical GPS accuracy (3–5 meters).

---

## 4. Kalman Filter Model

State vector:

x = position, velocity^T

System model:

x_k = A x_{k-1} + B u_k + w_k

Where:

- `u_k` = acceleration from IMU
- `w_k` = process noise

Measurement model:

z_k = H x_k + v_k

Where:

- `z_k` = GPS distance measurement
- `v_k` = measurement noise

---

# Results

The final output compares:

- **GPS measured distance**
- **Kalman Filter estimated distance**

The Kalman Filter produces a **smoother and more stable distance estimate** by combining GPS and IMU information.

Visualization example:

GPS Distance vs Kalman Filter Distance

The filtered trajectory shows reduced noise compared to raw GPS measurements.

---

# Visualization of LiDAR Point Cloud

The project also includes an example of loading and visualizing a **KITTI Velodyne LiDAR point cloud** using **Open3D**.

Point cloud format:

x y z intensity

---

# How to Run

## 1. Install dependencies

```bash
pip install numpy pandas matplotlib open3d

2. Run Jupyter Notebook

jupyter notebook

Open:

kalman_kitti.ipynb

Run all cells.

⸻

Output

The notebook generates:
	•	Distance plots (GPS vs Kalman Filter)
	•	LiDAR point cloud visualization
	•	CSV file with results

kf_results.csv


⸻

Author

Student project – Sensor Fusion using Kalman Filter with KITTI dataset.


