# Experimental Dataset: SAIM XPLORER-AC Modular Autonomous Mobile Robot

This repository contains the experimental dataset for the **SAIM XPLORER-AC**, a modular autonomous mobile robot utilizing a ROS 2-based navigation architecture. The dataset consists of **24 unique experimental trials** designed to rigorously evaluate the performance, stability, and computational efficiency of the local trajectory planner under varying environmental constraints and algorithmic configurations.

---

## System Overview

The SAIM XPLORER-AC uses the **Model Predictive Path Integral (MPPI)** controller as its local trajectory planner, integrated within the **Nav2** navigation stack on **ROS 2**. The experimental framework isolates specific kinematic behaviors and obstacle-avoidance capabilities, providing empirical evidence for optimizing controller behavior across five distinct scenarios.

---

## Repository Structure

```
Teste_robot_saim_xplorer_2/
├── straight_line_tests/          # Scenario 1: Translational Kinematics (10 trials)
│   ├── test_01_linie_dreapta/    #   Trial 1 — vx configuration A
│   ├── test_02_linie_dreapta/    #   Trial 2 — vx configuration B
│   ├── ...
│   └── test_10_linie_dreapta/    #   Trial 10 — vx configuration J
├── curba_tests/                  # Scenario 2: Angular Kinematics & Sharp Cornering (4 trials)
│   ├── test_01_curba/
│   ├── test_02_curba/
│   ├── test_03_curba/
│   └── test_04_curba/
├── obstacol_test/                # Scenario 3: Static Obstacle Clearance (1 trial)
│   └── test_obstacol/
├── slalom_tests/                 # Scenario 4: Multi-Obstacle Slalom Navigation (4 trials)
│   ├── test_01_slalom/
│   ├── test_02_slalom/
│   ├── test_03_slalom/
│   └── test_04_slalom/
├── batch_tests/                  # Scenario 5: Dynamic Obstacle Evasion (3 trials)
│   ├── test_batch_200/           #   Batch size 200
│   ├── test_batch_400/           #   Batch size 400
│   └── test_batch_850/           #   Batch size 850
├── README.md
└── LICENSE                       # MIT
```

---

## Methodology & Experimental Design

The testing framework systematically alters core MPPI navigation parameters across five distinct scenarios. Each scenario targets a specific kinematic behavior or obstacle-avoidance capability, providing controlled empirical measurements for controller optimization.

### Scenario 1 — Translational Kinematics & Velocity Scaling

**Description:** The robot executes a pure translational trajectory over a distance of 3 meters.

**Parameters Modified:** Maximum linear velocity (`vx`)

**Evaluation Objective:** To measure longitudinal tracking accuracy and steady-state error at varying speeds, identifying the threshold where high velocities introduce overshooting, oscillations, or actuator saturation.

| Trial | Folder |
|-------|--------|
| 1–10 | `straight_line_tests/test_01_linie_dreapta` → `test_10_linie_dreapta` |

---

### Scenario 2 — Angular Kinematics & Sharp Cornering

**Description:** The robot performs 90-degree rotational maneuvers distributed over a 2-meter navigational path.

**Parameters Modified:** Angular velocities (`omega_z`, `omega_y`)

**Evaluation Objective:** To assess heading accuracy and rotational stability, observing path deviation during sharp turns and evaluating how aggressively the robot can corner without losing localization or destabilizing the chassis.

| Trial | Folder |
|-------|--------|
| 1–4 | `curba_tests/test_01_curba` → `test_04_curba` |

---

### Scenario 3 — Static Obstacle Clearance

**Description:** Navigation around a single static obstacle positioned 1 meter from the robot's initial pose.

**Parameters Modified:** Obstacle Cost Critic and Cost Weight

**Evaluation Objective:** To determine the sensitivity of the local planner to costmap gradients, analyzing the trade-off between safety and efficiency to find optimal parameter weights that maintain a safe clearance buffer without generating excessively wide, inefficient trajectories.

| Trial | Folder |
|-------|--------|
| 1 | `obstacol_test/test_obstacol` |

---

### Scenario 4 — Multi-Obstacle Slalom Navigation

**Description:** Complex path planning through a sequence of three static obstacles spaced 1 meter apart, with the first obstacle located 1 meter from the start point.

**Parameters Modified:** Temperature (`T`) and Gamma (`γ`)

**Evaluation Objective:** To evaluate the exploration versus exploitation balance within the MPPI sampling algorithm, monitoring how the temperature parameter affects the spread of sampled trajectories, and how gamma influences the cost function's aggressiveness in tightly constrained environments.

| Trial | Folder |
|-------|--------|
| 1–4 | `slalom_tests/test_01_slalom` → `test_04_slalom` |

---

### Scenario 5 — Dynamic Obstacle Evasion

**Description:** The robot must evade a moving obstacle, beginning 1 meter away, with both robot and obstacle initiating movement simultaneously.

**Parameters Modified:** MPPI batch size (number of sampled trajectories)

**Evaluation Objective:** To analyze real-time computational efficiency and reaction latency, identifying the minimum batch size required to successfully generate collision-free trajectories against moving threats without inducing controller lag or CPU bottlenecking.

| Trial | Batch Size | Folder |
|-------|-----------|--------|
| 1 | 200 | `batch_tests/test_batch_200` |
| 2 | 400 | `batch_tests/test_batch_400` |
| 3 | 850 | `batch_tests/test_batch_850` |

---

## Experimental Summary

| Scenario | Description | Trials | Key Parameter |
|----------|-------------|--------|---------------|
| 1 | Translational Kinematics | 10 | Max linear velocity (`vx`) |
| 2 | Angular Kinematics | 4 | Angular velocities (`omega_z`, `omega_y`) |
| 3 | Static Obstacle Clearance | 1 | Obstacle Cost Critic & Weight |
| 4 | Multi-Obstacle Slalom | 4 | Temperature (`T`), Gamma (`γ`) |
| 5 | Dynamic Obstacle Evasion | 3 | MPPI Batch Size |
| **Total** | | **22** | |

---

## Software Stack

| Component | Technology |
|-----------|-----------|
| Robot Operating System | ROS 2 |
| Navigation Framework | Nav2 |
| Local Trajectory Planner | MPPI (Model Predictive Path Integral) |

---

## Authors

- **Mario Schmidt** — experimental design, data collection, analysis
- **Rares Constantin** — experimental design, data collection, analysis
- **Alexandru Gheorghiu** — experimental design, data collection, analysis
- **Andrei Slavescu** — experimental design, data collection, analysis

**Coordination & Supervision:**
- **B. F. Abaza** — supervision, formal analysis
- **C. V. Doicin** — supervision, validation, resources

Faculty of Industrial Engineering and Robotics (FIIR),
National University of Science and Technology POLITEHNICA Bucharest

---

## License

This project is released under the [MIT License](./LICENSE).
