# CodeAlpha_Object_Detection_and_Tracking
Object detection model using Yolov8

# 🔍 Object Detection Model using YOLOv8

A lightweight, high-performance object detection project implementing Ultralytics YOLOv8. This project demonstrates image inference, real-time bounding box plotting, and custom webcam integration logic designed to run in both local Python environments and Google Colab notebooks.

---

## 🎯 Project Objective

The primary objective of this project is to implement real-time object detection using the state-of-the-art **YOLOv8** (You Only Look Once) framework. 

### Key Features:
1. **Ultralytics YOLO Integration**: Uses pre-trained weights (`yolov8n.pt`, `yolo11n.pt`, etc.) to recognize 80 common object classes out of the box (like cats, dogs, people, vehicles).
2. **Inference & Visualization**: Automates loading images, running inference, and plotting boundary boxes with confidence levels.
3. **Webcam Capture Setup**: Contains scripts to stream feeds from a local OpenCV webcam or hook into a virtual browser webcam stream using JavaScript in Google Colab.

---

## 🛠️ Project Structure

```
Object detection model yolov8/
├── YOLOv8 (1).ipynb   # Jupyter Notebook containing setup, inference, and visualization
├── yolov8n.pt         # Pre-trained YOLOv8 Nano weights (6.2MB)
├── yolo11n.pt         # Pre-trained YOLOv11 Nano weights (5.4MB)
├── cat_dog.jpg        # Sample testing image 1
└── cat_dog2.jpg       # Sample testing image 2
```

---

## ⚙️ How the Code Works

1. **Environment Setup**: Installs the `ultralytics` library which contains the YOLO wrapper APIs.
2. **Model Loading**:
   ```python
   from ultralytics import YOLO
   model = YOLO('yolov8n.pt')  # Loads the nano version of YOLOv8
   ```
3. **Image Inference**:
   ```python
   result = model("cat_dog2.jpg")
   ```
4. **Result Rendering**:
   - `result[0].plot()` extracts the original image overlayed with detected labels, colors, and bounding boxes.
   - Saves or displays the rendered image using OpenCV (`cv2.imwrite()`) or IPython display.
5. **Live Webcam Tracking** (Commented block for local deployment):
   - Opens local webcam stream `cv2.VideoCapture(0)`.
   - Loops frame-by-frame, applying the YOLO detector to draw target boxes dynamically in a pop-up window until the user presses `q` to quit.

---

## 🚀 Getting Started

Follow these steps to run the object detector locally on your machine.

### 1. Installation
Install the necessary package dependencies via pip:
```bash
pip install ultralytics opencv-python pillow matplotlib
```

### 2. Running Inference on Sample Images
1. Open the Jupyter Notebook: **`YOLOv8 (1).ipynb`**.
2. Run the cells to download the `yolov8n.pt` weights (if not already downloaded).
3. Specify your target image file (e.g., `cat_dog2.jpg`) in the prediction cell:
   ```python
   result = model("your_image.jpg")
   result[0].show()
   ```

### 3. Running with a Local Webcam
Uncomment the local camera OpenCV block in the notebook:
```python
camera = cv2.VideoCapture(0)
while True:
    ret, frame = camera.read()
    if not ret:
        break
    results = model(frame, verbose=False)
    plot_frame = results[0].plot()
    cv2.imshow("YOLOv8 Real-Time Detection", plot_frame)
    if cv2.waitKey(1) & 0xFF == ord("q"):
        break
camera.release()
cv2.destroyAllWindows()
```
Run this block to launch a real-time object detection window!

---

## ⚡ Model Options
This folder contains multiple pre-trained weights for comparison:
* **`yolov8n.pt` (YOLOv8 Nano)**: Optimized for CPU and edge devices (fastest speed, lowest memory footprint).
* **`yolo11n.pt` (YOLO11 Nano)**: The newer generation edge detector from Ultralytics, showcasing advanced accuracy with similar low parameter sizes.

---

**Made with ❤️ for AI Project - 4th Semester**

