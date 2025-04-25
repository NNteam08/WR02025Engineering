Project Description

This project was developed for participation in the World Robot Olympiad (WRO). The robot is capable of color and object recognition, utilizes gyroscopic sensors for spatial orientation, obstacle avoidance, and efficient motor control.

Key Features

Color and object recognition using HuskyLens

Gyroscopic stabilization (MPU6050 sensor)

Distance measurement with IR sensors

Motor control via the L298N driver

Automatic navigation and obstacle avoidance

Installation

Clone the repository:

Upload firmware to Arduino:

Open Arduino IDE and upload the code from src/main.ino.

Usage

After uploading the firmware to Arduino:

Power on the robot.

Press the start button (pin 8) to begin program execution.

Project Structure

wro-robot
├── images
├── src
├── LICENSE.md
└── README.md

Component Connections

Component

Arduino Pin

HuskyLens RX           Pin 2

HuskyLens TX           Pin 3

MPU6050 SD             A4

MPU6050 SCL            A5

IR sensors             A0, A1, A2

Motors                 EnA=5, IN1=6, IN2=7

Servo                  Pin 9

Start button           Pin 8

License

This project is licensed under the MIT License.

Contact

GitHub: NNTeam08
