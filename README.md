# Self-driving Car — Autonomous Navigation Platform

Meet our self-driving car project! A sophisticated autonomous vehicle platform built with Raspberry Pi 4B, multiple sensors, and custom control electronics.

## Overview
This self-driving car is an advanced autonomous navigation platform featuring real-time road follow, autonomous path planning, and motorized control. The project combines hardware integration with software algorithms to create a fully functional autonomous vehicle capable of navigating complex environments.

## Features
- **Multi-sensor detection** using 4× VL53L0X Time-of-Flight distance sensors
- **Inertial measurement** with MPU6050 accelerometer and gyroscope for motion tracking
- **Autonomous navigation** algorithms running on Raspberry Pi 4B
- **Servo-based steering control** using MG996R servo motor
- **DC motor propulsion** with BTS7960 high-current motor driver
- **Real-time data processing** and decision making
- **Power management** with LiPo batteries and buck converters regulation

## Hardware Architecture

### Processing Unit
- **Raspberry Pi 4B**: Central processing unit handling sensor fusion, decision making, and motor control

### Sensors
- **4× VL53L0X Flight Time Distance Sensors**: Time-of-flight distance measurement to not run into walls
  - Sensor 1: Front-right
  - Sensor 2: Front-left
  - Sensor 3: Left
  - Sensor 4: Right
- **MPU6050 Accelerometer + Gyroscope**: 6-DOF inertial measurement for motion estimation and stability

### Actuation & Control
- **BTS7960 Motor Driver**: High-current DC motor control (up to 43A)
- **PCA9865 PWM Controller**: 16-channel PWM generator for precise motor and servo control
- **Motor (540-J DC Motor)**: Primary propulsion
- **MG996R Servo Motor**: Steering control

### Power System
- **2 Zeee 7.4V 4000mAh 50C 2S LiPo Battery**: Main power sources
- **24/5V Buck Converters**: Voltage regulation for logic circuits
- **Power Distribution Board**: Centralized power management with multiple regulated outputs

## Bill of Materials
| Component | Quantity | Description |
|-----------|----------|-------------|
| Raspberry Pi 4B | 1 | Central processing unit |
| VL53L0X ToF Sensor | 4 | Distance measurement |
| MPU6050 IMU | 1 | Accelerometer + Gyroscope |
| BTS7960 Motor Driver | 1 | DC motor control |
| PCA9865 PWM Controller | 1 | Servo and motor PWM |
| Motor 540-J | 1 | Propulsion motor |
| MG996R Servo Motor | 1 | Steering servo |
| 24/5V Buck Converter | 2 | Voltage regulation |
| Power Distribution Board | 1 | Power management |
| Zeee LiPo Battery | 2 | 7.4V 4000mAh 50C 2S |
| Switch | 1 | Master power switch |
| Wires & Connectors | Various | I2C, PWM, power |

## Wiring

### I2C Bus (SCL: GPIO3, SDA: GPIO2)
All I2C devices share the same data and clock lines:
- **VL53L0X Sensors (4×)**
  - SDA → GPIO2
  - SCL → GPIO3
  - VIN → Power Distribution Board outputs (1-4)
  - GND → Corresponding ground outputs
  - XSHUT → GPIO26, GPIO21, GPIO20, GPIO16 (individual shutdown pins)

- **MPU6050 IMU**
  - SDA → GPIO2
  - SCL → GPIO3
  - VCC → Power Distribution Board Output 7+
  - GND → Power Distribution Board Output 7-

- **PCA9865 PWM Controller**
  - SDA → GPIO2
  - SCL → GPIO3
  - VCC → Power Distribution Board Output 6+
  - GND → Power Distribution Board Output 6-

### Motor Control
- **DC Motor (540-J)**
  - V+ → BTS7960 M+
  - GND → BTS7960 M-

- **BTS7960 Motor Driver**
  - VM+ → 24/5V Buck Converter VIN+
  - VM- → 24/5V Buck Converter VIN-
  - VCC → 24/5V Buck 5V
  - GND → 24/5V Buck GND
  - L_PWM → PCA9865 PWM0
  - R_PWM → PCA9865 PWM1
  - L_EN, R_EN → PCA9865 V+

### Servo Control
- **MG996R Servo Motor**
  - VCC → PCA9865 V+
  - GND → PCA9865 GND
  - SIG → PCA9865 PWM15

### Power Distribution
- **Zeee 7.4V LiPo Battery**
  - (+) → 24/5V Buck VIN+
  - (-) → 24/5V Buck VIN-

- **24/5V Buck Converter**
  - VIN+ → Battery (+)
  - VIN- → Battery (-)
  - 5V → Switch Vin
  - GND → Switch GND

- **Master Power Switch**
  - Vin → 24/5V Buck 5V
  - GND → Raspberry Pi GND
  - Vout → Raspberry Pi 5V

- **Raspberry Pi 4B**
  - 5V → Switch Vout
  - GND → Power Distribution Board, Switch GND

### Complete Pin Mapping

| Raspberry Pi Pin | Function | Connected To |
|------------------|----------|--------------|
| GPIO2 (SDA) | I2C Data | All I2C sensors |
| GPIO3 (SCL) | I2C Clock | All I2C sensors |
| GPIO16 | VL53L0X Sensor 4 XSHUT | Distance sensor shutdown |
| GPIO20 | VL53L0X Sensor 3 XSHUT | Distance sensor shutdown |
| GPIO21 | VL53L0X Sensor 2 XSHUT | Distance sensor shutdown |
| GPIO26 | VL53L0X Sensor 1 XSHUT | Distance sensor shutdown |
| 5V | Main power | Power switch output |
| GND | Ground | All grounds (common) |

## Circuit Diagram

<img src="https://github.com/Loufok0/Self-driving-car/blob/main/medias/circuit_true_true_true_true.png">

## Software Setup

### Requirements
- Raspberry Pi OS (Bullseye or later)
- Python 3.8+
- Required Python libraries:
  - `smbus2` (I2C communication)
  - `RPi.GPIO` or `gpiozero` (GPIO control)
  - list to continue

### Installation
1. Clone this repository:
   ```bash
   git clone https://github.com/Loufok0/Self-driving-car.git
   cd Self-driving-car

## Safety Disclaimer
This project is for educational purposes only. Ensure you operate in a safe environment and comply with local laws and regulations regarding autonomous vehicles.
We do not takes any responsabilities in reproducing this repo instructions.
