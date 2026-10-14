# 🚁 Drone Detection System Using YOLOv8

**Real-Time Object Detection | Python | Label Studio | OpenCV | Raspberry Pi**

An end-to-end computer vision project for detecting drones in images and live video streams using a custom-trained YOLOv8 model. The project covers dataset collection, annotation, model training, real-time inference, and edge deployment.

## 📌 Project Overview

The Drone Detection System uses deep learning and computer vision to identify drones in real time. A custom drone dataset is annotated using Label Studio and used to train a YOLOv8 object detection model.

The trained model has been tested successfully with a phone camera feed. Raspberry Pi deployment is partially implemented, with further optimization required to achieve stable real-time performance on resource-constrained hardware.

## ✨ Features

- Real-time drone detection using YOLOv8
- Custom dataset annotation with Label Studio
- Training with Ultralytics YOLOv8n
- Live video inference using OpenCV
- Phone camera streaming through IP Webcam
- Bounding-box visualization for detected drones
- Raspberry Pi edge deployment in progress
- Planned lightweight model optimization using NCNN or TFLite

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| YOLOv8 | Drone object detection |
| Label Studio | Dataset annotation |
| OpenCV | Image and video processing |
| Raspberry Pi | Edge deployment |
| IP Webcam | Phone camera streaming |

## 🔄 Project Workflow

1. Collect drone images from photographs, open-source datasets, and videos.
2. Annotate drones using bounding boxes in Label Studio.
3. Export annotations in YOLO format.
4. Configure the dataset using a YAML configuration file.
5. Train the YOLOv8 model.
6. Test detection on images and live phone-camera video.
7. Optimize and deploy the model on Raspberry Pi.

## ⚙️ Installation

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
```

Replace the URL with your actual GitHub repository URL.

### 2. Create a Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install ultralytics opencv-python
```

For dataset annotation, install Label Studio:

```bash
pip install label-studio
label-studio start
```

Open `http://localhost:8080` in your browser to access Label Studio.

## 📂 Dataset Configuration

Organize your dataset as follows:

```text
dataset/
├── images/
│   ├── train/
│   └── val/
└── labels/
    ├── train/
    └── val/
```

Create a `drone.yaml` configuration file:

```yaml
path: dataset
train: images/train
val: images/val

nc: 1
names:
  0: drone
```

Ensure each image has a corresponding YOLO-format label file.

## 🏋️ Model Training

Download the pretrained YOLOv8 Nano model and train it on your dataset:

```bash
yolo detect train \
  model=yolov8n.pt \
  data=drone.yaml \
  epochs=100 \
  imgsz=640 \
  batch=16 \
  name=drone_detector
```

The best-performing model weights are typically saved at:

```text
runs/detect/drone_detector/weights/best.pt
```

Adjust the batch size according to your available memory.

## 📱 Real-Time Detection

Use a webcam or phone camera stream to perform inference:

```python
from ultralytics import YOLO

model = YOLO("best.pt")

results = model.predict(
    source=0,
    conf=0.5,
    show=True,
    save=True
)
```

For a phone camera, replace `source=0` with your IP Webcam stream URL:

```python
source = "http://PHONE_IP:8080/video"
```

Ensure the phone and computer are connected to the same network and that the stream URL is accessible.

## 🍓 Raspberry Pi Deployment

The next stage is to run inference directly on Raspberry Pi hardware using a camera module or USB webcam.

Current challenges include limited computational resources and inference performance. Planned improvements include:

- Testing lightweight inference formats such as NCNN.
- Reducing inference latency and memory usage.
- Benchmarking performance on the target Raspberry Pi.
- Achieving stable real-time detection on edge hardware.

## 📊 Project Status

- [x] Drone dataset collection and annotation workflow
- [x] YOLOv8 model training workflow
- [x] Real-time detection using a phone camera feed
- [ ] Model optimization for Raspberry Pi
- [ ] Stable real-time Raspberry Pi deployment

## 🚀 Future Improvements

- Improve detection accuracy across different distances and lighting conditions.
- Expand the dataset with more drone types and backgrounds.
- Evaluate precision, recall, and mAP.
- Optimize inference speed for edge devices.
- Explore integration with automated monitoring and alert systems.

## 🎯 Applications

- Drone monitoring and surveillance
- Restricted-area monitoring
- Aerial object detection
- Edge AI and computer vision research

## 👨‍💻 Author

**Dipak Hrishi Das**

Electronics and Communication Engineering Student

GitHub: [@dipak042](https://github.com/dipak042)

## 📄 License

This project is intended for educational and research purposes. Add a suitable open-source license to the repository if you wish to permit reuse and redistribution.
