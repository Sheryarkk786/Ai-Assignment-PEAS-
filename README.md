# Ai-Assignment-PEAS-
Ai assignment By sir rajesh
# Assignment 1: AI System Specification

## Student Information
* **Name:** Sheryar
* **Roll No:** 2k23/CSE/140
* **Course:** Introduction to Artificial Intelligence
* **Topic:** PEAS Framework & Environment Analysis
* **Selected Application:** Option C – Agricultural Monitoring Drone for Crop Disease Detection

---

## Task 1: PEAS Specification

### Performance Measures
* **Catch Rate (True Positive Rate):** The percentage of real crop infections the drone successfully finds, making sure we don't skip an outbreak that could destroy the harvest.
* **False Alarm Rate:** How often the AI mistakes healthy leaves for sick ones; keeping this low stops the farmer from wasting money on unnecessary chemical sprays.
* **Battery Coverage Efficiency:** Total acreage scanned per single battery charge, showing how practical the system is for commercial use.
* **Mapping Precision:** The accuracy of marking infected areas on a map, which must be accurate within centimeters so ground crews can find the exact spot.

### Environment
* The drone operates in real-world, dynamic outdoor farmlands, crop fields, and commercial plantations.
* **Key External Factors:** Includes unpredictable wind patterns, sudden temperature shifts, changing cloud shadows that mess with light levels, variable crop heights, birds, and obstacles like power poles.

### Actuators
* **Propulsion:** Four electric brushless motors and electronic speed controllers (ESCs) that drive the propellers to fly, steer, and balance.
* **Camera Stabilization:** A motorized 3-axis physical gimbal mechanism that keeps the camera level and steady during turbulent flight conditions.
* **Communication:** An onboard digital radio transmitter that sends live coordinates and disease alerts back to the farmer's ground station.

### Sensors
* **Vision Payload:** A high-resolution 4K camera paired with a 5-band multispectral sensor array that tracks light wavelengths beyond what humans can see to spot early plant stress.
* **Positioning:** An RTK-enabled GPS receiver unit that reads satellite positioning data with high pinpoint precision.
* **Flight Tracking:** An internal 6-axis Inertial Measurement Unit (IMU) combined with a downward LiDAR altimeter to monitor flying height above uneven field terrain.

---

## Task 2: Environment Classification

* **Partially Observable:** The drone can only inspect the outer crop canopy from above and cannot see hidden root systems or infected leaves tucked underneath the top layer.
* **Multi-agent:** The drone operates alongside other active elements like wild birds, farm workers moving on foot, or driven tractors whose paths are completely independent.
* **Stochastic:** Weather forces like sudden wind gusts, passing cloud shadows, and stray animals are completely random and cannot be fully predicted ahead of time.
* **Sequential:** Choosing to spend battery power scanning a specific zone early in the flight limits the remaining charge and options available for the rest of the mission.
* **Dynamic:** The environment keeps changing on its own while the drone is flying and thinking, as the sun moves, winds shift, and birds fly past.
* **Continuous:** Parameters like flying speed, altitude, remaining battery level, and visual camera inputs change smoothly across an infinite range instead of clear, step-by-step numbers.

---

## Task 3: Critical Analysis

### 1. Greatest Technical Challenge
The **Partially Observable** dimension is definitely the hardest hurdle to clear when building this drone. While handling random winds or tracking speed can be solved with classic control loops, missing data is a fundamental problem. Plant illnesses usually start inside the stem or on the bottom sides of leaves where a top-down camera simply cannot see them. This means the AI engineer can't just build a basic image identifier; they have to design an algorithm that can reliably infer a hidden disease state from subtle color changes in the upper canopy under shifting, unreliable natural sunlight.

### 2. Utility Function & Weight Trade-off
To help the drone handle the trade-off between speed, accuracy, and physical safety, we can set up a simple scoring formula:

$$U(a) = w_1 \cdot A(a) - w_2 \cdot R(a) - w_3 \cdot E(a)$$

Where:
* $A(a)$ stands for the expected diagnostic accuracy of the images.
* $R(a)$ is the actual crash risk of that flight path.
* $E(a)$ is the rate of battery usage.
* $w_1, w_2, w_3$ are positive weights balancing each component.

#### Behavioral Shift if $w_2$ is Doubled:
If we double the safety penalty weight ($w_2$), the drone will become extremely cautious. Instead of flying low to the crop canopy to get sharp, high-quality images or pushing through heavy winds to finish scanning a row, the AI will prioritize avoiding any risk of a crash. It will automatically fly at higher, safer altitudes and make slow, wide turns clear of obstacles. While this keeps the drone safe, flying higher means the camera images lose their fine details, making it much harder for the AI to catch early-stage crop infections before they spread across the farm.
