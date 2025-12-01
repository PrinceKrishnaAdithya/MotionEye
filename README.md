# Ultrasonic-Based Dual-Servo Positioning System

This Arduino project uses **two ultrasonic sensors** to dynamically control **two servos** (left and right) based on detected distances along the **X-axis** and **Y-axis**.  
The system adjusts servo angles in real time to track objects or maintain alignment depending on proximity.

---

## Overview

The project measures distance using two HC-SR04–style ultrasonic sensors:

- **Sensor X** controls the **base servo angle**  
- **Sensor Y** introduces **fine adjustment (offset/differential)**  

Both values combine to create smooth dual-servo movement.

---

## Features

### Real-Time Distance Measurement
- Uses `pulseIn()` to measure echo duration  
- Converts timing to distance in centimeters  

### Dual Ultrasonic Sensor System
- **X-Sensor** → Primary servo position  
- **Y-Sensor** → Adds/subtracts an offset (`diff`) for finer alignment  

### Independent Servo Control
- Custom `servoControl()` function  
- Converts angle → pulse width (544–2400µs)  
- Direct servo signal output (no Servo library)

### Automatic Safety Constraints
- Limits distances to avoid invalid servo angles  
- Prevents servo over-rotation at edge cases

---

## Hardware Requirements

| Component | Quantity |
|----------|----------|
| Arduino Board | 1 |
| HC-SR04 Ultrasonic Sensors | 2 |
| Servo Motors (SG90/MG996R) | 2 |
| Jumper Wires | - |
| Power Supply | As required |

---

## Pin Connections

### Ultrasonic Sensors
| Function | Pin |
|----------|-----|
| trigPinX | 2 |
| echoPinX | 3 |
| trigPinY | 5 |
| echoPinY | 6 |

### Servo Motors
| Servo | Pin |
|--------|-----|
| Left Servo | 8 |
| Right Servo | 10 |

### Adjustable Parameters
```cpp
const int A = 20; // Range limit for X sensor (cm)
const int B = 15; // Range limit for Y sensor (cm)
