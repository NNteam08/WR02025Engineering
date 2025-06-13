Electrical
====


## Parts Explanation
| Part Name  | Explanation |Image |Datasheet |
| ------------- | ------------- | -------------|  -------------|
| KP Original Battery SM4PIN 7.4V 14500 1000 mAh Rechargeable Lithium ion Battery  | We use two separate batteries: one dedicated to power the motors (to ensure high current demands are met) and the other for logic and sensors to provide stable voltage and extend runtime. This dual-battery approach ensures uninterrupted operation and maximal performance throughout each run. | ![image] (https://drive.google.com/uc?export=view&id=1kfdiVbTWhyWyHCSF2aAfYXwkoSjrG1Fu) |
| LM2596 DC-DC Adjustable Buck Converter Step Down Module 1.23-30V  | Efficient step-down regulator that voltage-transforms from 7.4 V to stable 5 V/3.3 V for Arduino and sensors with minimal heat loss. It delivers up to 3 A with high efficiency (~92%) and built-in protection features (thermal shutdown, current limit) |
| L298N Dual H-Bridge Motor Driver| Drives two DC motors with independent direction and speed (via PWM). Supports up to 2 A per motor, ideal for differential drive. |
| GP2Y0A41SK0F IR Range Sensor | Side-facing angled IR sensor used during navigation and parking to measure proximity to track walls. Allows real-time wall detection and precise maneuvers. |
| GP2Y0A02YK0F IR Range Sensor| 	Front and rear long-range IR sensors for obstacle detection and wall following on the track; provides early warning of oncoming objects.
| CJMCU34725 TCS34725 RGB Light Color Sensor| Positioned under the chassis to detect colored track markers (blue/orange laps, parking zone). Enables color-triggered lane decisions and lap counting. |
| DC 6V Electric Motors 29RPM 6mm Shaft High Torque Gear Box Speed Reduction Fan Motors Electric Motor| Provides robust propulsion with gear reduction. The motor runs on its own high-current battery for maximum speed and torque. Ideal for reliable track performance. |
| Microservo Gsmin TowerPro SG90 (BT907570) | Controls steering linkage. Offers ~1.8 kg·cm stall torque, fast response (~0.1 s/60°), and stable operation at 4.8–6 V . |
| MPU6050 - 3 axis gyroscope and 3 axis acclerometer| Detects yaw and orientation for precise turning and straight-line stability. Gyro integration aids in accurate parking and obstacle avoidance. |
| Ultrasonic Module HC-SR04 Distance Measurement Sensor Sensor for Arduino| Mounted sideways to assist with parallel parking. Offers reliable short-range measurements to walls/fence during alignment. |
