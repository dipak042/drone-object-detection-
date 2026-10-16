# 🚁 Drone Detection System using YOLOv8

**Real-time drone detection | YOLOv8n | Python | OpenCV | Label Studio | Raspberry Pi 5**

An end-to-end computer vision project that detects drones in images and live video using a custom-trained YOLOv8n model. It covers dataset collection, annotation, training, real-time inference, and edge deployment on a Raspberry Pi 5.

<!-- Add a demo GIF or screenshot here, e.g. ![Demo](assets/demo.gif) -->

---

## 📊 Results

| Platform | Model | Performance |
| --- | --- | --- |
| Raspberry Pi 5 | Custom YOLOv8n | ~15 FPS real-time detection (occasionally higher) |
| Laptop + phone camera (IP Webcam) | Custom YOLOv8n | Real-time detection with bounding boxes |

<!-- After running `yolo val`, add: Precision / Recall / mAP@0.5 / mAP@0.5:0.95 -->

---

## ✨ Features

- Custom drone dataset annotated with **Label Studio** (YOLO format export)
- Training with **Ultralytics YOLOv8n** (single class: `drone`)
- Real-time inference with **OpenCV** and bounding-box visualization
- Live phone camera streaming through **IP Webcam**
- Edge deployment on **Raspberry Pi 5**

---

## 🛠️ Tech Stack

| Technology | Purpose |
| --- | --- |
| Python | Core language |
| YOLOv8 (Ultralytics) | Object detection model |
| Label Studio | Dataset annotation |
| OpenCV | Image and video processing |
| Raspberry Pi 5 | Edge deployment |
| IP Webcam | Phone camera streaming |

---

## 🔄 Project Workflow

1. Collect drone images from photographs, open-source datasets, and videos
2. Annotate drones with bounding boxes in Label Studio
3. Export annotations in YOLO format
4. Configure the dataset in `data.yaml`
5. Train the YOLOv8n model
6. Test detection on images and live camera streams
7. Deploy on Raspberry Pi 5 for edge inference

---

## 📂 Repository Structure

```
drone-object-detection-/
├── README.md
├── data.yaml              # Dataset configuration (1 class: drone)
├── object_detect-2.ipynb  # Training and testing notebook
└── test.rar               # Test samples
```

---

## ⚙️ Installation

```bash
git clone https://github.com/dipak042/drone-object-detection-.git
cd drone-object-detection-

python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install ultralytics opencv-python
```

To annotate your own data:

```bash
pip install label-studio
label-studio start              # opens http://localhost:8080
```

---

## 🏋️ Training

Dataset layout (YOLO format):

```
dataset/
├── images/
│   ├── train/
│   └── val/
└── labels/
    ├── train/
    └── val/
```

`data.yaml`:

```yaml
path: dataset
train: images/train
val: images/val

nc: 1
names:
  0: drone
```

Train:

```bash
yolo detect train model=yolov8n.pt data=data.yaml epochs=100 imgsz=640 batch=16 name=drone_detector
```

Best weights are saved to `runs/detect/drone_detector/weights/best.pt`.

Evaluate:

```bash
yolo detect val model=runs/detect/drone_detector/weights/best.pt data=data.yaml
```

---

## 📱 Real-Time Detection

```python
from ultralytics import YOLO

model = YOLO("best.pt")

# Webcam: source=0
# Phone camera (IP Webcam): source="http://PHONE_IP:8080/video"
results = model.predict(source=0, conf=0.5, show=True, save=True)
```

Make sure the phone and computer are on the same network when using IP Webcam.

---

## 🍓 Raspberry Pi 5 Deployment

The trained model runs on a **Raspberry Pi 5**, reaching about **15 FPS** for real-time detection. Frame rate can fluctuate with scene complexity and system load.

Planned improvements:

- Export to a lighter format (NCNN / TFLite) to push FPS higher
- Benchmark latency and memory usage across input sizes
- Mount the Pi on a drone for airborne detection

---

## 📈 Project Status

- [x] Dataset collection and annotation
- [x] YOLOv8n training
- [x] Real-time detection on a phone camera stream
- [x] Deployment on Raspberry Pi 5 (~15 FPS)
- [ ] Model optimization (NCNN / TFLite)
- [ ] Precision / recall / mAP evaluation
- [ ] Onboard drone integration

---

## 🎯 Applications

- Restricted-area drone monitoring
- Aerial object detection
- Edge AI and computer vision research

---

## 👨‍💻 Author

**Dipak Hrishi Das**
B.Tech, Electronics and Communication Engineering

GitHub: [@dipak042](https://github.com/dipak042)
