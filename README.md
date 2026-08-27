# DriveX Autonomous Vehicle and V2X Research Platform

**ROS 2 · Nav2 · LiDAR · Raspberry Pi 5 · Arduino · Ackermann Control · V2V/V2I**

DriveX is an experimental autonomous-vehicle research platform developed for studying physical mobile robotics, connected autonomous systems, and V2X-assisted cooperative autonomy.

The platform integrates low-level embedded vehicle control with ROS 2-based localization, autonomous navigation, path planning, path tracking, infrastructure-assisted information exchange, and experimental performance evaluation.

The current system has been experimentally validated on a physical indoor Ackermann-steering vehicle and is being extended toward a two-vehicle V2V/V2I research platform for cooperative-driving, communication-degradation, and runtime-safety experiments.

---

## Research Objectives

DriveX is designed to investigate the integration of autonomous navigation, vehicle control, and connected-vehicle information in physical robotic systems.

The main research objectives include:

* Developing reliable autonomous navigation for a physical Ackermann-steering vehicle.
* Integrating V2I infrastructure information with onboard ROS 2 perception and decision logic.
* Extending the platform to two autonomous vehicles for V2V state and intention exchange.
* Investigating cooperative decision-making and multi-vehicle coordination.
* Evaluating V2X communication latency and information freshness.
* Evaluating system behavior under communication delay and packet-loss conditions.
* Investigating runtime safety under nominal and communication-degraded operating conditions.

---

## System Overview

The DriveX platform combines three main engineering layers.

### 1. Embedded Vehicle Layer

* Motor actuation
* Steering control
* Encoder acquisition
* Embedded vehicle control
* Low-level Arduino communication

### 2. Autonomous Navigation Layer

* ROS 2
* SLAM Toolbox
* Nav2
* LiDAR-based mapping and localization
* Costmap-based obstacle representation
* Smac Hybrid-A* path planning
* Regulated Pure Pursuit path tracking
* Encoder-based odometry

### 3. Connected Autonomy Layer

* RSU-assisted V2I information
* TCP/IP communication over Wi-Fi
* Timestamp-based message freshness validation
* V2V state and intention exchange
* Cooperative decision-making
* Communication-degradation evaluation
* Runtime safety

---

## Hardware Platform

| Component              | Implementation                  |
| ---------------------- | ------------------------------- |
| Vehicle configuration  | Ackermann-steering mobile robot |
| High-level computer    | Raspberry Pi 5                  |
| Low-level controller   | Arduino Uno R3                  |
| Main perception sensor | 2D LiDAR                        |
| Motion feedback        | Wheel encoder                   |
| Steering               | Servo-based front steering      |
| Vehicle actuation      | Rear-wheel drive                |
| Infrastructure         | Roadside Unit (RSU)             |
| Communication          | TCP/IP over Wi-Fi               |

---

## Software Architecture

The autonomous vehicle software is based on ROS 2 and separates high-level autonomous decision-making from low-level vehicle actuation.

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
                         v
                  Motor / Steering
```

The platform is currently being extended toward a two-vehicle V2X architecture:

```text
        +-----------+               +-----------+
        |   DX01    | <--- V2V ---> |   DX02    |
        +-----------+               +-----------+
              ^                           ^
              |                           |
              +----------- RSU -----------+
                          V2I
```

---

## Autonomous Navigation

The physical vehicle uses a ROS 2-based autonomous-navigation stack.

### Mapping and Localization

* SLAM Toolbox
* 2D LiDAR
* ROS 2 TF-based coordinate transformations
* Map generation and map-based localization

### Path Planning

DriveX uses **Smac Hybrid-A*** for path planning while considering the nonholonomic motion constraints of an Ackermann-steering vehicle.

### Path Tracking

The vehicle uses **Regulated Pure Pursuit** for path tracking.

The navigation stack integrates:

* Global path planning
* Local obstacle representation
* Vehicle footprint modeling
* Costmap-based navigation
* Steering-constrained path tracking
* LiDAR-based obstacle detection

The navigation system has been experimentally tested on a physical indoor Ackermann-steering vehicle.

---

## Vehicle Control and Odometry

Low-level vehicle control is implemented using an Arduino-based embedded controller interfaced with the ROS 2 high-level computer.

The vehicle-control system includes:

* Motor actuation
* Steering-angle control
* Encoder acquisition
* Encoder-based odometry
* Steering calibration
* Wheel-motion calibration
* Vehicle motion parameter calibration
* Physical experimental validation

### Selected Odometry Results

| Experiment                      |                     Result |
| ------------------------------- | -------------------------: |
| Forward-distance odometry error |                     ~0.72% |
| Reverse-distance odometry error |                     ~0.13% |
| Experimental platform           | Physical Ackermann vehicle |
| Localization framework          |               SLAM Toolbox |
| Path planner                    |             Smac Hybrid-A* |
| Path-tracking controller        |     Regulated Pure Pursuit |

These results were obtained from physical vehicle experiments rather than simulation-only evaluation.

---

## V2I Communication

DriveX includes an RSU-assisted V2I pipeline for infrastructure-aware autonomous driving.

The current implementation:

* Transmits timestamped intersection information from the Roadside Unit.
* Uses TCP/IP communication over Wi-Fi.
* Checks message freshness before infrastructure information is accepted.
* Integrates valid V2I information with onboard ROS 2 perception and decision logic.
* Provides infrastructure-level information beyond the vehicle's onboard sensing capability.
* Supports communication-aware autonomous decision-making.

The RSU provides information to the vehicle decision layer rather than directly controlling the vehicle actuators.

---

## V2V and Cooperative Autonomy

DriveX is currently being extended from a single-vehicle platform to a two-vehicle connected-autonomy research system.

The ongoing development focuses on:

* Vehicle-state exchange
* Vehicle-intention exchange
* V2V communication
* Combined V2V/V2I information
* Cooperative intersection behavior
* Communication latency evaluation
* Packet-loss experiments
* Communication-degradation experiments
* Multi-vehicle coordination
* Safe autonomous decision-making

> **Status:** Under active development.

---

## Runtime Safety

A runtime-safety layer is being developed as an independent supervisory mechanism for detecting or preventing unsafe autonomous decisions.

Planned evaluation scenarios include:

* Unsafe command detection
* Delayed V2X information
* Packet loss
* Stale V2X messages
* Communication interruption
* Safety intervention
* Conflict between nominal autonomy and safety constraints

The objective is to evaluate whether the autonomous system can maintain safe behavior when communication or decision-making conditions become degraded.

> **Status:** Under active development.

---

## Experimental Evaluation

DriveX is designed as a physical research testbed for quantitative evaluation across autonomous navigation, vehicle control, V2X communication, cooperative behavior, and runtime safety.

### Autonomous Navigation

Potential evaluation metrics include:

* Navigation success rate
* Path-tracking error
* Goal-reaching performance
* Obstacle avoidance behavior
* Localization consistency

### Vehicle Control

Evaluation includes:

* Odometry accuracy
* Steering calibration
* Distance-tracking error
* Vehicle motion repeatability

### V2X Communication

Evaluation focuses on:

* Communication latency
* Message freshness
* Packet loss
* Communication degradation
* Information availability

### Cooperative Autonomy

Evaluation will include:

* Coordination success rate
* Intersection conflict behavior
* Vehicle waiting time
* Cooperative decision consistency
* Multi-vehicle safety

### Runtime Safety

Evaluation will include:

* Unsafe-state detection
* Safety intervention frequency
* Safety response time
* Collision/conflict prevention
* Behavior under degraded communication conditions

---

## Experimental Scenarios

The research platform is intended to support scenarios such as:

1. Local autonomous driving without V2X assistance.
2. V2I-assisted autonomous driving.
3. V2V-assisted vehicle coordination.
4. Combined V2V and V2I cooperative driving.
5. Communication-delay scenarios.
6. Packet-loss scenarios.
7. Stale-information scenarios.
8. Unsafe or conflicting decision scenarios.
9. Runtime-safety intervention scenarios.

A complete set of experimental scenarios will be progressively documented as the two-vehicle platform is completed.

---

## Project Portfolio

Videos, hardware demonstrations, experimental materials, system documentation, and supporting results are available in the DriveX project portfolio:

[**DriveX Project Portfolio**](https://drive.google.com/drive/folders/147Pp82Ls9ovT0m0YNKJmgXiO2AjZyxZU?usp=sharing)

The portfolio contains selected materials such as:

* Physical vehicle demonstrations
* Autonomous navigation experiments
* Mapping and localization results
* Odometry calibration
* V2I experiments
* Experimental scenario documentation
* Hardware photographs
* Technical diagrams
* Supporting research materials

---

## Current Development Status

| Module                                 | Status                      |
| -------------------------------------- | --------------------------- |
| Physical Ackermann vehicle             | ✅ Implemented               |
| Raspberry Pi 5 high-level control      | ✅ Implemented               |
| Arduino low-level vehicle control      | ✅ Implemented               |
| ROS 2 integration                      | ✅ Implemented               |
| LiDAR integration                      | ✅ Implemented               |
| SLAM mapping                           | ✅ Implemented               |
| Map-based localization                 | ✅ Implemented               |
| Nav2 autonomous navigation             | ✅ Implemented               |
| Smac Hybrid-A* planning                | ✅ Implemented               |
| Regulated Pure Pursuit tracking        | ✅ Implemented               |
| Encoder odometry                       | ✅ Experimentally validated  |
| RSU-assisted V2I pipeline              | ✅ Implemented               |
| Timestamp/message-freshness validation | ✅ Implemented               |
| Second autonomous vehicle              | 🔄 In development           |
| V2V state exchange                     | 🔄 In development           |
| V2V intention exchange                 | 🔄 In development           |
| Cooperative decision logic             | 🔄 In development           |
| Runtime safety layer                   | 🔄 In development           |
| Communication-degradation experiments  | 🔄 Planned / In development |
| Multi-vehicle quantitative evaluation  | 🔄 Planned / In development |

---

## Planned Repository Structure

The repository will be progressively organized into the following structure:

```text
drivex-v2x-platform/
├── README.md
├── .gitignore
│
├── docs/
│   ├── architecture/
│   ├── hardware/
│   ├── experiments/
│   └── figures/
│
├── src/
├── config/
├── launch/
├── maps/
├── scripts/
└── results/
```

### Directory Purpose

* **`docs/`** — system architecture, hardware documentation, experimental scenarios, and technical figures.
* **`src/`** — selected ROS 2 source code and custom vehicle-control nodes.
* **`config/`** — Nav2, SLAM, localization, and system parameter configuration files.
* **`launch/`** — ROS 2 launch files.
* **`maps/`** — selected maps used for physical experiments.
* **`scripts/`** — experimental analysis and supporting scripts.
* **`results/`** — selected processed experimental results.

Source code and experimental materials will be added progressively after review for research, publication, and intellectual-property compatibility.

---

## Research Areas

* Autonomous Vehicles
* Mobile Robotics
* ROS 2
* Autonomous Navigation
* Control Systems
* Embedded Vehicle Control
* Connected Autonomous Systems
* V2V / V2I / V2X
* Cooperative Autonomy
* Multi-Vehicle Coordination
* Intelligent Transportation Systems
* Runtime Safety
* Experimental Robotics

---

## Technologies

**Robotics and Autonomy**

ROS 2 · Nav2 · SLAM Toolbox · RViz2 · LiDAR · Smac Hybrid-A* · Regulated Pure Pursuit

**Control and Vehicle Systems**

Ackermann Steering · Encoder Odometry · PID Control · Vehicle Motion Calibration · Path Tracking

**Embedded Systems**

Raspberry Pi 5 · Arduino Uno R3 · C/C++ · Sensor Integration · Motor Control · Servo Control

**Connected Systems**

V2I · V2V · V2X · TCP/IP · Wi-Fi · RSU-assisted Infrastructure Information

**Research and Analysis**

MATLAB/Simulink · Ubuntu Linux · Experimental Logging · Quantitative Performance Evaluation

---

## Development Note

DriveX is an active research project.

Some source code, experimental datasets, cooperative-driving algorithms, and runtime-safety implementations may remain private while related research and publication activities are ongoing.

Publicly released materials will focus on reproducible technical documentation, selected implementation components, and experimentally validated results.
