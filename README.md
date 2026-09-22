# Adaptive Traffic Signal Optimization Using YOLOv26 Object Detection and PCE-Weighted Fuzzy Logic

## Project Documents

* [Research Paper – Adaptive Traffic Signal Optimization](13-%20Adaptive%20Traffic%20light%20revisi.pdf)
* [Model Comparison Notebook](4_model_comparison.ipynb)

## 1. Title

**Adaptive Traffic Signal Optimization Using YOLOv26 Object Detection and PCE-Weighted Fuzzy Logic**

This project develops an adaptive traffic light system that combines YOLOv26 object detection with PCE-weighted fuzzy logic to dynamically determine green-light duration based on real-time traffic conditions.

---

## 2. Executive Summary

Traditional traffic lights generally use fixed-time signal durations, meaning that a lane can receive a green light for a predetermined amount of time regardless of the actual number of vehicles waiting. This can result in wasted green-light time and inefficient traffic flow.

This project proposes an adaptive traffic light system that uses YOLOv26 to detect vehicles in real time and PCE-weighted fuzzy logic to determine the appropriate green-light duration. The system considers different vehicle types, such as cars, motorcycles, trucks, buses, and pickups, because each vehicle has a different impact on traffic flow.

Four YOLO models were compared: YOLOv8n, YOLOv10n, YOLOv11n, and YOLOv26n. The reported results show that YOLOv26n achieved a precision of 0.9614 and mAP@0.50:0.95 of 0.8113. The adaptive fuzzy approach also reduced wasted green-light time from 4,781 seconds to 3,188 seconds, representing a reported 33.3% reduction compared with the fixed-time baseline.

---

## 3. Business Problem

Traditional fixed-time traffic lights do not respond to changes in real-time traffic conditions.

For example, a traffic light may stay green for 30 seconds even when there are only a few vehicles waiting. At the same time, another lane may have a much longer queue but still have to wait for its scheduled green phase.

This creates several problems:

* Wasted green-light time
* Longer vehicle waiting times
* Inefficient use of road capacity
* Increased fuel consumption
* Increased vehicle emissions
* Limited ability to respond to changing traffic conditions

The main problem addressed by this project is:

**How can traffic signals dynamically adjust their green-light duration according to real-time traffic conditions?**

The proposed solution uses vehicle detection to understand the current traffic situation and fuzzy logic to determine the appropriate signal duration.

---

## 4. Methodology

The project follows these main steps:

**Indonesian Vehicle Dataset → Data Preprocessing → YOLO Model Training → Vehicle Detection → Vehicle Tracking → PCE Calculation → Fuzzy Logic → Adaptive Green-Light Duration → Performance Evaluation**

### Dataset

The project uses an open-source Indonesian vehicle dataset from Roboflow.

The dataset contains:

* More than 10,500 images
* 5 vehicle classes
* Pickup
* Bus
* Car
* Motorcycle
* Truck
* High-definition images
* JPEG/JPG format

The dataset was selected to represent heterogeneous traffic conditions in Indonesia.

### Exploratory Data Analysis

Exploratory Data Analysis (EDA) was performed to understand the distribution of the vehicle classes.

The reported validation dataset has a relatively balanced distribution, with each vehicle category containing more than 2,000 instances. This helps reduce the effect of class imbalance during model training.

### Data Preprocessing

The YOLO framework handles several preprocessing operations during training, including:

* Checking the dataset structure
* Verifying bounding-box coordinates
* Removing corrupt files
* Resizing images
* Letterbox padding
* Converting images into tensors
* Data augmentation

Augmentation techniques include mosaic stitching, horizontal flipping, and color modifications.

### YOLO Model Training

Four models were compared:

* YOLOv8n
* YOLOv10n
* YOLOv11n
* YOLOv26n

The models were evaluated using precision, recall, F1-score, mAP@0.50, and mAP@0.50:0.95.

### Vehicle Detection and Tracking

The trained YOLO model detects vehicles from traffic video. Vehicle tracking is then used to maintain the identity of vehicles across different frames.

This helps prevent the same vehicle from being repeatedly counted.

### PCE Calculation

Passenger Car Equivalent (PCE) is used to account for the different effects of vehicle types on traffic flow.

The research uses:

* Light vehicle = 1.0
* Heavy vehicle = 1.3
* Motorcycle = 0.25

The detected vehicles are converted into PCE values to estimate overall traffic density.

### Fuzzy Logic

The PCE-based traffic density is passed to a fuzzy logic controller.

The controller uses four main stages:

1. Fuzzification
2. Rule evaluation
3. Inference
4. Defuzzification

Traffic density is categorized into levels such as low, medium, and high. The controller then produces the appropriate green-light duration.

For example:

* Low traffic → shorter green light
* Medium traffic → medium green light
* High traffic → longer green light

---

## 5. Skills

### Programming & Data Analysis

* Python
* Pandas
* NumPy
* Data preprocessing
* Exploratory Data Analysis
* Data visualization

### Machine Learning & Computer Vision

* YOLO object detection
* Model training
* Model comparison
* Object detection evaluation
* Vehicle tracking
* OpenCV
* ByteTrack

### Intelligent Systems

* Fuzzy logic
* Mamdani fuzzy controller
* Fuzzification
* Rule-based inference
* Defuzzification
* Passenger Car Equivalent (PCE)

### Tools & Libraries

* Google Colab
* Jupyter Notebook
* Roboflow
* Ultralytics
* PyTorch
* OpenCV
* Scikit-fuzzy
* Pandas
* NumPy
* Matplotlib
* Seaborn

---

## 6. Results & Business Recommendation

### YOLO Model Comparison

The reported model comparison produced the following results:

| Metric        | YOLOv26n | YOLOv8n | YOLOv10n | YOLOv11n |
| ------------- | -------: | ------: | -------: | -------: |
| Precision     |   0.9614 |  0.9477 |   0.9586 |   0.9582 |
| Recall        |   0.9317 |  0.9442 |   0.9350 |   0.9453 |
| F1-Score      |   0.9463 |  0.9459 |   0.9467 |   0.9517 |
| mAP@0.50      |   0.9693 |  0.9698 |   0.9705 |   0.9755 |
| mAP@0.50:0.95 |   0.8113 |  0.8033 |   0.8079 |   0.8081 |

YOLOv26n achieved a precision of **0.9614** and mAP@0.50:0.95 of **0.8113**.

YOLOv11n achieved the highest recall at **0.9453** and F1-score at **0.9517** among the compared models.

### Traffic Signal Efficiency

The adaptive fuzzy approach was compared with the fixed-time baseline:

| Approach       | Wasted Green Time |
| -------------- | ----------------: |
| Fixed Timer    |     4,781 seconds |
| Adaptive Fuzzy |     3,188 seconds |

The research reports a **33.3% reduction in wasted green-light time** using the adaptive approach.

The fuzzy controller also produced dynamic green-light durations, with the reported distribution concentrated around approximately 20–21 seconds.

### Edge Performance

The reported inference latency was:

* YOLOv26: 3.2 ms
* YOLOv8n: 8.5 ms
* Faster R-CNN: 45.0 ms

On a Tesla T4 GPU, the reported throughput was:

* YOLOv8n: 115.5 FPS
* YOLOv10n: 101.1 FPS
* YOLOv11n: 97.9 FPS
* YOLOv26n: 80.1 FPS

These results demonstrate a trade-off between detection performance and processing speed.

### Business Recommendation

The proposed system demonstrates how real-time vehicle detection and fuzzy logic can be combined to make traffic signal timing responsive to traffic demand.

Potential applications include:

* Smart city traffic management
* Adaptive traffic signals
* Traffic congestion management
* Intelligent Transportation Systems
* Real-time traffic monitoring
* Edge-based traffic management

The current system should be further tested in real-world traffic environments before practical deployment because the research was validated using a simulation environment and a public Indonesian vehicle dataset.

---

## 7. Next Steps

### Real-World Deployment

Test the system at an actual Indonesian intersection to evaluate performance under real traffic conditions.

### Multi-Intersection Coordination

Extend the system so that multiple traffic lights can communicate and coordinate their signal timings.

### Additional Sensors

Integrate additional sensors such as radar and thermal cameras to improve detection under difficult conditions such as poor lighting or weather.

### Improve the Fuzzy Logic Controller

Further develop the fuzzy rules to consider additional factors such as traffic density, queue length, waiting time, vehicle type, and traffic flow.

### Edge Device Deployment

Test the system on edge devices to determine whether real-time detection and traffic signal control can operate directly at an intersection.

### Testing Under Different Conditions

Evaluate the system under:

* Heavy traffic
* Low traffic
* Nighttime conditions
* Rain
* Vehicle occlusion
* Different camera angles
* Different intersection layouts

### Future Development

The long-term goal is to develop a complete intelligent transportation system that can connect real-time vehicle detection, adaptive traffic signals, and multiple intersections to improve traffic management.
