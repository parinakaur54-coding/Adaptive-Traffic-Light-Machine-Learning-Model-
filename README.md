# Adaptive-Traffic-Light-Machine-Learning-Model-

````markdown
# Adaptive Traffic Signal Optimization Using YOLOv26 Object Detection and PCE-Weighted Fuzzy Logic

## 📂 Project Documents

- 📄 [Research Paper](13-%20Adaptive%20Traffic%20light%20revisi.pdf)
- 💻 [Model Comparison Notebook](4_model_comparison.ipynb)

---

# 1. Title

## Adaptive Traffic Signal Optimization Using YOLOv26 Object Detection and PCE-Weighted Fuzzy Logic

This project proposes an adaptive traffic light system that combines YOLOv26 object detection with PCE-weighted fuzzy logic to dynamically determine traffic signal timing based on real-time vehicle density.

The system is designed for heterogeneous traffic conditions in Indonesia, where different types of vehicles such as motorcycles, cars, trucks, buses, and pickups have different effects on traffic flow.

---

# 2. Executive Summary

Traditional traffic lights commonly use fixed-time signal durations. This approach does not respond to changes in real-time traffic conditions. As a result, a traffic lane may continue receiving a green light even when there are few or no vehicles waiting.

This project develops an adaptive traffic light system that uses computer vision and fuzzy logic to address this problem.

The system uses **YOLOv26 Nano** to detect vehicles from traffic images and videos. The detected vehicles are then tracked and converted into **Passenger Car Equivalent (PCE)** values. PCE provides a weighted representation of traffic density because different vehicle types have different effects on traffic flow.

The PCE-based traffic density is then passed to a **fuzzy logic controller**, which determines an appropriate green-light duration. Instead of using one fixed duration, the system can provide different green-light durations depending on the current traffic demand.

Four YOLO models were evaluated:

- YOLOv8n
- YOLOv10n
- YOLOv11n
- YOLOv26n

The reported results show that YOLOv26n achieved a precision of **0.9614** and an mAP@0.50:0.95 of **0.8113**. The adaptive fuzzy approach also reduced wasted green-light time from **4,781 seconds to 3,188 seconds**, representing a reported **33.3% reduction** compared with the fixed-time baseline.

The research demonstrates how machine learning, computer vision, object tracking, PCE, and fuzzy logic can be combined to create a more responsive traffic signal management system.

---

# 3. Business Problem

## Problem

Traditional traffic signal systems often rely on predetermined fixed-time durations.

For example, a traffic light may provide a lane with 30 seconds of green time regardless of whether there are 20 vehicles waiting or no vehicles at all.

This creates several potential problems:

- Green-light time can be wasted when traffic demand is low.
- Vehicles on other approaches may have to wait unnecessarily.
- Traffic signals cannot immediately respond to changing traffic density.
- Fuel can be wasted when vehicles remain idle.
- Vehicle emissions can increase because of unnecessary waiting.
- Fixed-time systems are less suitable for highly dynamic traffic conditions.

The research identifies fixed-time signals as a limitation because they do not consider real-time vehicle density.

## Proposed Solution

The project proposes an adaptive traffic signal system that follows this process:

```text
Traffic Video
     ↓
YOLOv26 Vehicle Detection
     ↓
Vehicle Tracking
     ↓
Vehicle Counting
     ↓
PCE Calculation
     ↓
Traffic Density
     ↓
Fuzzy Logic Controller
     ↓
Green-Light Duration
````

Instead of giving every traffic lane the same fixed amount of green time, the proposed system uses detected traffic conditions to determine the green-light duration.

---

# 4. Methodology

## 4.1 Overall Workflow

The research follows the following workflow:

```text
Indonesian Vehicle Dataset
            ↓
Exploratory Data Analysis
            ↓
Data Preprocessing
            ↓
YOLO Model Training
            ↓
Vehicle Detection
            ↓
Vehicle Tracking
            ↓
PCE-Based Traffic Density
            ↓
Fuzzy Logic Controller
            ↓
Adaptive Green-Light Duration
            ↓
System Evaluation
```

The methodology combines machine learning for vehicle detection with fuzzy logic for traffic signal decision-making.

---

## 4.2 Dataset

The project uses an open-source Indonesian vehicle dataset from Roboflow.

The dataset contains:

* **10,500+ images**
* **5 vehicle classes**
* Pickup
* Bus
* Car
* Motorcycle
* Truck
* High-definition images
* JPEG/JPG format

The dataset was selected because it represents heterogeneous traffic conditions and contains different types of vehicles commonly found in Indonesian traffic.

---

## 4.3 Exploratory Data Analysis

Exploratory Data Analysis (EDA) was conducted to understand the distribution and characteristics of the dataset.

The analysis examined the distribution of the vehicle classes in the validation dataset.

The reported dataset distribution was relatively balanced, with each vehicle category containing more than 2,000 instances. This helps reduce the potential effect of majority-class bias during object detection model training.

---

## 4.4 Data Preprocessing

The YOLO framework performs several preprocessing operations during the training process.

These include:

* Checking the dataset directory structure
* Verifying bounding-box coordinates
* Removing corrupt files
* Resizing images
* Letterbox padding
* Converting pixel values into tensors
* Data augmentation

The training process also uses transformations such as:

* Mosaic augmentation
* Horizontal flipping
* Color-space modifications

These transformations help the model learn from different visual conditions.

---

## 4.5 YOLO Object Detection

The project compares four YOLO models:

```text
YOLOv8n
YOLOv10n
YOLOv11n
YOLOv26n
```

The purpose of the comparison is to evaluate the detection performance of different YOLO versions.

The models are evaluated using:

* Precision
* Recall
* F1-score
* mAP@0.50
* mAP@0.50:0.95

YOLOv26 Nano is used in the proposed adaptive traffic-light pipeline.

---

## 4.6 Vehicle Tracking

After vehicles are detected, vehicle tracking is used to maintain the identity of detected vehicles across consecutive video frames.

The project uses vehicle tracking to prevent the same vehicle from being repeatedly counted as a new vehicle.

The detected vehicles are then used to estimate the traffic demand in the relevant waiting-zone area.

---

## 4.7 Passenger Car Equivalent (PCE)

Simply counting vehicles is not always enough because different vehicle types occupy different amounts of road space and have different effects on traffic flow.

Therefore, the project uses **Passenger Car Equivalent (PCE)** to convert different vehicle types into weighted traffic values.

The research uses the following PCE values:

| Vehicle Type  | PCE Value |
| ------------- | --------: |
| Light Vehicle |       1.0 |
| Heavy Vehicle |       1.3 |
| Motorcycle    |      0.25 |

The PCE values are combined to estimate the overall traffic density.

For example:

```text
Traffic Density
=
(Number of Light Vehicles × 1.0)
+
(Number of Heavy Vehicles × 1.3)
+
(Number of Motorcycles × 0.25)
```

This provides a more representative measurement of traffic demand than simply counting every vehicle equally.

---

## 4.8 Fuzzy Logic Controller

The PCE-based traffic density is passed to a fuzzy logic controller.

The fuzzy logic process consists of:

### 1. Fuzzification

The numerical traffic-density value is converted into linguistic categories such as:

* Low
* Medium
* High

### 2. Rule Evaluation

Predefined fuzzy rules determine how the traffic density should affect the green-light duration.

For example:

```text
IF traffic density is LOW
THEN green-light duration is SHORT

IF traffic density is MEDIUM
THEN green-light duration is MEDIUM

IF traffic density is HIGH
THEN green-light duration is LONG
```

### 3. Defuzzification

The fuzzy output is converted into a specific numerical green-light duration.

This allows the traffic signal to dynamically adjust according to detected traffic conditions.

---

## 4.9 Evaluation

The system is evaluated using several types of metrics.

### Object Detection Metrics

* Precision
* Recall
* F1-score
* mAP@0.50
* mAP@0.50:0.95

### Traffic Efficiency

* Wasted green-light duration
* Queue length
* Adaptive green-phase duration

### Runtime Performance

* Inference latency
* Frames per second (FPS)

These metrics are used to evaluate both the vehicle detection model and the adaptive traffic-light system.

---

# 5. Skills

## Programming & Data Analysis

* Python
* Pandas
* NumPy
* Data preprocessing
* Exploratory Data Analysis (EDA)
* Data visualization

## Machine Learning

* YOLO object detection
* Model training
* Model evaluation
* Model comparison
* Precision, Recall, F1-score
* Mean Average Precision (mAP)

## Computer Vision

* Object detection
* Vehicle detection
* Vehicle tracking
* OpenCV
* ByteTrack
* Real-time video processing

## Intelligent Systems

* Fuzzy logic
* Mamdani fuzzy controller
* Fuzzification
* Rule-based inference
* Defuzzification
* Passenger Car Equivalent (PCE)

## Tools & Libraries

* Python
* Google Colab / Jupyter Notebook
* Ultralytics
* PyTorch
* OpenCV
* Scikit-fuzzy
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Roboflow

---

# 6. Results & Business Recommendation

## 6.1 YOLO Model Comparison

The reported comparison between the four YOLO models produced the following results:

| Metric        | YOLOv26n | YOLOv8n | YOLOv10n | YOLOv11n |
| ------------- | -------: | ------: | -------: | -------: |
| Precision     |   0.9614 |  0.9477 |   0.9586 |   0.9582 |
| Recall        |   0.9317 |  0.9442 |   0.9350 |   0.9453 |
| F1-Score      |   0.9463 |  0.9459 |   0.9467 |   0.9517 |
| mAP@0.50      |   0.9693 |  0.9698 |   0.9705 |   0.9755 |
| mAP@0.50:0.95 |   0.8113 |  0.8033 |   0.8079 |   0.8081 |

The reported results show that YOLOv26n achieved:

* **Precision: 0.9614**
* **mAP@0.50:0.95: 0.8113**

YOLOv11n achieved:

* **Recall: 0.9453**
* **F1-score: 0.9517**

Therefore, the models show different performance characteristics depending on the evaluation metric.

---

## 6.2 Wasted Green-Light Time

The adaptive traffic-light system was compared with a fixed-time baseline.

| Approach       | Wasted Green Time |
| -------------- | ----------------: |
| Fixed Timer    |     4,781 seconds |
| Adaptive Fuzzy |     3,188 seconds |

The research reports that the adaptive fuzzy approach reduced wasted green-light time by **33.3%** compared with the fixed-time approach.

This result indicates that the adaptive system can adjust the green phase according to traffic demand instead of maintaining a predetermined duration.

---

## 6.3 Adaptive Green-Phase Distribution

The fuzzy controller generated different green-light durations depending on traffic demand.

The reported distribution showed a high concentration of green-light durations around **20–21 seconds**.

This demonstrates that the controller can dynamically adjust the green phase rather than always using one fixed duration.

---

## 6.4 Edge Deployment Performance

The reported inference latency was:

| Model        | Latency |
| ------------ | ------: |
| YOLOv26      |  3.2 ms |
| YOLOv8n      |  8.5 ms |
| Faster R-CNN | 45.0 ms |

The reported Tesla T4 throughput was:

| Model    |   FPS |
| -------- | ----: |
| YOLOv8n  | 115.5 |
| YOLOv10n | 101.1 |
| YOLOv11n |  97.9 |
| YOLOv26n |  80.1 |

The results show a trade-off between detection performance and processing speed.

---

## 6.5 Business Recommendation

The proposed system demonstrates how an adaptive traffic signal can use real-time vehicle information instead of relying only on fixed signal timings.

Potential practical applications include:

* Smart city traffic management
* Congestion monitoring
* Adaptive traffic signals
* Intelligent Transportation Systems (ITS)
* Real-time traffic management
* Edge-based traffic monitoring

For implementation in real traffic environments, additional validation would be required because the current research was validated using a simulation environment and a public Indonesian vehicle dataset.

---

# 7. Next Steps

## 7.1 Real-World Deployment

The next step is to test the system at an actual Indonesian intersection.

Real-world testing would help evaluate the system under actual traffic conditions, camera positions, weather, road layouts, and vehicle behavior.

---

## 7.2 Multi-Intersection Coordination

The current system focuses on adaptive traffic signal control.

Future development could connect multiple intersections so that traffic lights can coordinate their signal timings across a larger road network.

---

## 7.3 Additional Sensors

Additional sensors could be integrated into the system, including:

* Radar
* Thermal cameras
* Other traffic sensors

These sensors could provide additional information when camera-based detection is affected by weather, lighting, or vehicle occlusion.

---

## 7.4 Improve the Fuzzy Logic Controller

The fuzzy logic rules can be further developed to handle more complex traffic situations.

Future versions could consider additional factors such as:

* Traffic density
* Queue length
* Waiting time
* Vehicle type
* Traffic flow
* Time of day

---

## 7.5 Edge Device Deployment

The system can be tested on edge computing hardware to determine whether real-time vehicle detection and fuzzy traffic control can operate directly near the traffic intersection.

This would reduce the need to send all video data to a remote server.

---

## 7.6 Testing Under Different Conditions

Future testing should include different traffic and environmental conditions, such as:

* Heavy traffic
* Low traffic
* Nighttime
* Rain
* Vehicle occlusion
* Different camera angles
* Different intersection layouts

---

## 7.7 Future System

The long-term development of the project can follow this structure:

```text
Real-Time Camera
       ↓
YOLO Vehicle Detection
       ↓
Vehicle Tracking
       ↓
Vehicle Classification
       ↓
PCE-Based Density Estimation
       ↓
Fuzzy Logic Controller
       ↓
Adaptive Traffic Signal
       ↓
Traffic Monitoring
       ↓
Multi-Intersection Coordination
```

This would extend the current prototype toward a larger intelligent transportation system.

---

# 📁 Project Structure

```text
Adaptive-Traffic-Light/
│
├── README.md
│
├── 13- Adaptive Traffic light revisi.pdf
│
├── 4_model_comparison.ipynb
│
└── dataset/
    └── Indonesian Vehicle Dataset
```

---

# 📚 References

The complete references used in the research are available in the research paper.

The project uses research related to:

* Adaptive traffic signal control
* YOLO-based vehicle detection
* Fuzzy logic
* Intelligent Transportation Systems
* Passenger Car Equivalent (PCE)
* Real-time vehicle detection
* Smart city traffic management

---

# 🔗 Project Files

* [📄 Research Paper](13-%20Adaptive%20Traffic%20light%20revisi.pdf)
* [💻 Model Comparison Notebook](4_model_comparison.ipynb)

```
```
