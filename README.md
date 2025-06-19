# Team NNteam08 – WRO 2025 Future Engineers  
**Autonomous Self-Driving Car Project**

---

## Introduction

Team NNteam08 presents our entry for the WRO 2025 Future Engineers category: an autonomous self-driving car designed to tackle the official parkour course. Our robot is engineered to handle every required challenge – track following, obstacle avoidance, parallel parking, and color zone recognition – completely autonomously. This repository shares our full engineering documentation, code, hardware design, and media in line with the open-source spirit of WRO.

The documentation is written in English as required by WRO rules and provides a comprehensive overview of our goals, design choices, and implementation strategies.

---

## Project Overview and Goals

**Primary Goal:**  
Develop a reliable, fast, and intelligent autonomous car capable of navigating the WRO Future Engineers course under random and challenging conditions.

**Key Objectives:**  
- **Track Navigation:** Follow the race track at optimal speed, handling both clockwise and counterclockwise runs.
- **Obstacle Avoidance:** Detect and safely avoid static obstacles without human input.
- **Parking Challenge:** Execute precise parallel parking within the marked zone.
- **Color Zone Recognition:** Detect color markers/zones and respond (e.g., stopping, turning) as per competition tasks.

We address each task using dedicated sensor systems, robust control logic, and proven autonomous driving techniques.

---

## Hardware Components & Architecture

- **Controller:**  
  *Arduino Mega 2560* — chosen for its abundant I/O and memory. Runs the entire system and interfaces with all sensors and actuators.
- **Drive Motors & Motor Driver:**  
  2x DC gear motors (differential drive) powered via *L298N H-bridge* for independent wheel speed/direction via PWM.
- **Steering:**  
  *Ackermann* steering using an RC servo for front wheel angle (realistic car kinematics, smooth turning).
- **Power Supply:**  
  Dual 7.4V Li-ion packs (motors) + 5V regulated (logic), stable under high load (see `docs/power.md`).
- **Vision (HuskyLens AI Camera):**  
  Used for line following, object detection, and color recognition, offloading heavy vision tasks from Arduino. Communicates via UART.
- **Color Sensor:**  
  *TCS34725* RGB sensor (downward facing) for color line detection, lap counting, and parking zone identification.
- **IR Distance Sensors:**  
  Sharp GP2Y0A02YK0F and GP2Y0A41SK0F, front and angled, for wall following and obstacle avoidance.
- **Gyroscope/IMU:**  
  MPU-6050 (3-axis gyro/accel) to measure orientation, track turns, and improve stability during driving and parking.
- **Ultrasonic Sensors:**  
  Side-facing for accurate parallel parking; assists in keeping safe wall distance.
- **Wiring:**  
  Custom shield & breadboard, see `schemes/` for diagrams.

**System Architecture:**  
Arduino reads sensor data, processes it via state machine logic, and actuates motors/steering. All sensing, planning, and acting is performed on-board for full autonomy.  
_Block diagram and wiring schematic available in `schemes/`._

---

## Challenge Strategies

1. **Track Following:**  
   - HuskyLens line-following mode + TCS34725 color sensor for turns/zones.
   - PID controller for steering.
   - IMU for accurate turns and course corrections.

2. **Obstacle Avoidance:**  
   - Sharp IRs for direct obstacle detection.
   - HuskyLens for visual block ID.
   - Dynamic rerouting: steers around obstacles using real-time sensor fusion.

3. **Parking:**  
   - Recognizes parking zone by color marker or HuskyLens cue.
   - Executes a parallel parking sequence using side ultrasonic/IR sensors and IMU for angle.
   - Stops within marked boundaries with <2cm side offset.

4. **Color Zone Recognition:**  
   - RGB sensor detects zones for specific actions (e.g., stop, lap count).
   - Code prioritizes zone events for maximum scoring.

**Reliability:**  
Multiple sensors cross-validate all major events. If conflicting data arises, robot slows or stops to prevent errors/crashes.

---

## Software Structure

- All code in `src/`, modularized:
    - `main.ino`: setup, main loop, high-level state machine.
    - `line_following.cpp`: PID control, color/line detection.
    - `obstacle_avoidance.cpp`: detection/avoidance logic.
    - `parking.cpp`: full parking maneuver.
    - `sensors.cpp`, `actuators.cpp`: sensor/motor abstractions.
    - `imu.cpp`: gyro/IMU handling.
    - `config.h`: pins, calibration, constants.
- Code is **extensively commented** for readability and reproducibility.
- Libraries required are listed in `docs/libraries_used.md`.

---

## Assembly Instructions

- **Mechanical Build:**  
  3D/CAD models in `models/`, assembly steps in `docs/assembly_guide.md`.
- **Wiring:**  
  Schematic in `schemes/electronic_schematic.png`.
- **Calibration:**  
  `docs/calibration.md` (sensor, color, gyro, HuskyLens).
- **Testing:**  
  `src/tests/` for motors, sensors, etc.  
  *Test each sensor and actuator before integrating!*

---

## How to Run

1. Assemble hardware (see `docs/`, `models/`).
2. Upload code from `src/` to Arduino.
3. Train HuskyLens (line/object as required).
4. Place car on start. Power on. Wait 5s for sensor stabilization.
5. Robot runs automatically, logging status to serial and LED.
6. For re-run: power cycle/reset.  
   *Manual override available via hardware switch (for testing only).*

---

## Repository Structure

- `README.md` – Project overview (this file).
- `src/` – Source code (Arduino/C++), with comments.
- `schemes/` – Schematics and block diagrams.
- `models/` – 3D and CAD files for custom parts.
- `t-photos/` – Team photos (official and fun).
- `v-photos/` – Robot photos (6+ angles).
- `video/` – YouTube demo links for each challenge.
- `docs/` – BOM, assembly, calibration, test logs, project report.
- `other/` – Extra notes, logs, datasheets, etc.
- `LICENSE` – MIT license.
- `.gitignore` – For build/output files.

---

## Media & Resources

- Photos: See `v-photos/` and `t-photos/`.
- Videos: `video/video.md` (links for track, obstacle, parking, color zone).
- Official WRO 2025 rules and templates:  
  - [WRO Association](https://wro-association.org/)
  - [Future Engineers 2025 Rules PDF](https://robotics.nis.edu.kz/wp-content/uploads/2025/03/WRO-2025-Future-Engineers.pdf)

---

## Compliance with WRO Criteria

- **Public GitHub repo** with commit history and full documentation.
- **5000+ chars README**, all photos/videos, clear code comments.
- **Open-source (MIT) license**.
- **Thorough structure and clarity** inspired by top teams’ repositories.

---

## References

- [WRO Association – General Rules](https://wro-association.org/)
- [WRO FE 2022 Template](https://github.com/WRO-FutureEngineers/fe-template)
- [Falafel Tech (Palestine) – WRO 2024 repo](https://github.com/FalafelTech/wro2024)
- [MINDCRAFT (Morocco) – WRO 2024 repo](https://github.com/wro2024-mindcraft)
- [Official 2025 Rules PDF](https://robotics.nis.edu.kz/wp-content/uploads/2025/03/WRO-2025-Future-Engineers.pdf)

---

**Contact:**  
Team NNteam08 – For questions, see `t-photos/README.md` for our contact email.  
We share our work openly for the benefit of all WRO participants!

---
