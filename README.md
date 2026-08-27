# DriveX Autonomous Vehicle and V2X Research Platform

**ROS 2 · Nav2 · LiDAR · Raspberry Pi 5 · Arduino · Ackermann Control · V2V/V2I**

DriveX is an experimental autonomous-vehicle research platform developed for studying physical mobile robotics, connected autonomous systems, and V2X-assisted cooperative autonomy.

The platform integrates low-level embedded vehicle control with ROS 2-based localization, autonomous navigation, path planning, path tracking, infrastructure-assisted information exchange, and experimental performance evaluation.

The current system has been experimentally validated on a physical indoor Ackermann-steering vehicle and is being extended toward a two-vehicle V2V/V2I research platform for cooperative-driving and runtime-safety experiments.

---

## Research Objectives

DriveX is designed to investigate the integration of autonomous navigation and connected-vehicle information in physical robotic systems.

The main research objectives include:

- Developing reliable autonomous navigation for a physical Ackermann-steering vehicle.
- Integrating V2I infrastructure information with onboard ROS 2 perception and decision logic.
- Extending the platform to two autonomous vehicles for V2V state and intention exchange.
- Evaluating communication latency and degraded communication conditions.
- Investigating cooperative decision-making and multi-vehicle coordination.
- Evaluating runtime safety under normal and communication-degraded operating conditions.

---

## System Overview

The DriveX platform combines three main engineering layers:

1. **Embedded Vehicle Layer**
   - Motor actuation
   - Steering control
   - Encoder acquisition
   - Low-level Arduino communication

2. **Autonomous Navigation Layer**
   - ROS 2
   - SLAM Toolbox
   - Nav2
   - LiDAR-based localization
   - Costmap-based obstacle representation
   - Smac Hybrid-A* path planning
   - Regulated Pure Pursuit path tracking

3. **Connected Autonomy Layer**
   - RSU-assisted V2I information
   - TCP/IP communication over Wi-Fi
   - Timestamp-based message freshness validation
   - V2V state and intention exchange
   - Cooperative decision-making
   - Runtime safety

---

## Hardware Platform

| Component | Implementation |
|---|---|
| Vehicle configuration | Ackermann-steering mobile robot |
| High-level computer | Raspberry Pi 5 |
| Low-level controller | Arduino Uno R3 |
| Main perception sensor | 2D LiDAR |
| Motion feedback | Wheel encoder |
| Steering | Servo-based front steering |
| Vehicle actuation | Rear-wheel drive |
| Infrastructure | Roadside Unit (RSU) |
| Communication | TCP/IP over Wi-Fi |

---

## Software Architecture

The autonomous vehicle software is based on ROS 2 and separates high-level autonomy from low-level actuation.

```text
                    Roadside Unit
                         |
                  TCP/IP over Wi-Fi
                         |
                         v
                  V2I Interface
                         |
                         v
              +---------------------+
              |    ROS 2 Vehicle    |
              |                     |
              |  Localization       |
              |  Nav2               |
              |  Path Planning      |
              |  Path Tracking      |
              |  Decision Logic     |
              |  Runtime Safety     |
              +----------+----------+
                         |
                         v
                  Arduino Control
                         |
                  Motor / Steering

The platform is currently being extended toward a two-vehicle architecture:
        DX01  <------ V2V ------>  DX02
          ^                       ^
          |                       |
          +-------- RSU ----------+
                    V2I
```

## Autonomous Navigation

The physical vehicle uses a ROS 2-based autonomous-navigation stack including:

- **SLAM Toolbox** for mapping and localization.
- **Nav2** for autonomous navigation.
- **Costmaps** for obstacle representation.
- **Smac Hybrid-A\*** for path planning under nonholonomic vehicle constraints.
- **Regulated Pure Pursuit** for path tracking.
- **LiDAR** for environmental perception and obstacle detection.

The navigation system has been experimentally tested on a physical indoor Ackermann-steering vehicle.

---

## Vehicle Control and Odometry

Low-level vehicle control is implemented using an Arduino-based embedded controller interfaced with the ROS 2 high-level computer.

The system includes:

- Motor-speed control
- Steering-angle control
- Encoder acquisition
- Encoder-based odometry
- Steering calibration
- Vehicle motion parameter calibration
- Physical experimental validation

### Selected Experimental Results

| Experiment | Result |
|---|---:|
| Forward-distance odometry error | ~0.72% |
| Reverse-distance odometry error | ~0.13% |
| Platform | Physical Ackermann vehicle |
| Localization | SLAM Toolbox |
| Path planner | Smac Hybrid-A* |
| Path-tracking controller | Regulated Pure Pursuit |

---

## V2I Communication

DriveX includes an RSU-assisted V2I pipeline for infrastructure-aware autonomous driving.

The current implementation:

- Transmits timestamped intersection information from the RSU.
- Uses TCP/IP communication over Wi-Fi.
- Checks message freshness before information is accepted.
- Integrates valid infrastructure information with onboard ROS 2 perception and decision logic.
- Provides infrastructure-level information beyond the vehicle's onboard sensing capability.

---

## V2V and Cooperative Autonomy

The platform is currently being extended to two autonomous vehicles.

The ongoing development focuses on:

- Vehicle-state exchange
- Vehicle-intention exchange
- V2V communication
- Combined V2V/V2I information
- Cooperative intersection behavior
- Communication latency evaluation
- Packet-loss and communication-degradation experiments
- Safe autonomous decision-making

> **Status:** Under active development.

---

## Runtime Safety

Runtime safety is being developed as an independent supervisory layer for evaluating and preventing unsafe autonomous decisions.

Planned experiments include:

- Unsafe command detection
- Communication-delay scenarios
- Packet-loss scenarios
- Stale V2X information
- Safety intervention analysis
- Comparison between nominal and degraded communication conditions

> **Status:** Under active development.

---

## Experimental Evaluation

DriveX is intended as a physical research testbed for quantitative evaluation of:

- Autonomous navigation performance
- Localization and odometry accuracy
- V2X communication latency
- Message freshness
- Cooperative-driving behavior
- Communication degradation
- Coordination performance
- Runtime safety

Additional experimental results will be added as the two-vehicle V2X platform is completed.

---

## Project Portfolio

Videos, hardware demonstrations, experimental materials, and supporting documentation:

[**DriveX Project Portfolio**](https://drive.google.com/drive/folders/147Pp82Ls9ovT0m0YNKJmgXiO2AjZyxZU?usp=sharing)

---

## Current Development Status

| Module | Status |
|---|---|
| Physical Ackermann vehicle | ✅ Implemented |
| ROS 2 integration | ✅ Implemented |
| LiDAR mapping and localization | ✅ Implemented |
| Nav2 autonomous navigation | ✅ Implemented |
| Encoder odometry | ✅ Experimentally validated |
| RSU-assisted V2I pipeline | ✅ Implemented |
| Two-vehicle platform | 🔄 In development |
| V2V communication | 🔄 In development |
| Cooperative decision logic | 🔄 In development |
| Runtime safety layer | 🔄 In development |
| Communication-degradation experiments | 🔄 Planned / In development |

---

## Research Areas

- Autonomous Vehicles
- Mobile Robotics
- ROS 2
- Autonomous Navigation
- Control Systems
- Connected Autonomous Systems
- V2V / V2I / V2X
- Cooperative Autonomy
- Intelligent Transportation Systems
- Runtime Safety
