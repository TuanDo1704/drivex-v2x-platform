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
