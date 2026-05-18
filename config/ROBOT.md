ROBOT -- SAIM XPLORER-AC Operator Profile

You are operating the SAIM XPLORER-AC, a modular autonomous mobile robot developed at the Faculty of Industrial Engineering and Robotics (FIIR), POLITEHNICA Bucharest. This profile describes the robot's hardware, software stack, and experimental configuration used during the evaluation dataset collection.

---

## Robot Description

The SAIM XPLORER-AC is a ground-based differential drive mobile robot designed for indoor autonomous navigation research. It serves as the physical validation platform for the Nav2 MPPI (Model Predictive Path Integral) local trajectory planner under controlled experimental conditions.

---

## Software Stack

| Component               | Technology          |
|-------------------------|---------------------|
| Operating System        | Ubuntu 24.04 LTS    |
| Robot Operating System  | ROS 2 Jazzy        |
| Navigation Framework    | Nav2                |
| Local Trajectory Planner| MPPI Controller     |
| Global Planner          | NavFn / Smac        |
| Localization            | AMCL                |
| Sensor Driver           | ROS 2 LiDAR driver  |

---

## Hardware Configuration

| Component        | Specification                        |
|------------------|--------------------------------------|
| Drive System     | Differential drive                   |
| Onboard Computer | Intel NUC / Raspberry Pi (embedded)  |
| LiDAR            | 2D LiDAR (360°)                      |
| IMU              | 6-DOF IMU                            |
| Power            | LiPo battery pack                    |

---

## ROS 2 Environment Setup

All ROS 2 commands require sourcing the environment first:

```bash
source /opt/ros/jazzy/setup.bash
```

To launch the full navigation stack:

```bash
ros2 launch nav2_bringup navigation_launch.py params_file:=config/mppi_params.yaml
```

To monitor the robot's current pose:

```bash
ros2 topic echo /amcl_pose
```

To send a navigation goal manually:

```bash
ros2 action send_goal /navigate_to_pose nav2_msgs/action/NavigateToPose "{pose: {header: {frame_id: 'map'}, pose: {position: {x: 1.0, y: 0.0, z: 0.0}}}}"
```

---

## Experimental Environment

All tests were conducted indoors on a flat surface. The test arena was configured per scenario:

| Scenario | Environment Setup                                      |
|----------|--------------------------------------------------------|
| 1        | Open corridor, 3-meter straight path, no obstacles     |
| 2        | Open corridor, 2-meter path with 90° turn markers      |
| 3        | Single static obstacle placed 1m from start pose       |
| 4        | Three static obstacles spaced 1m apart, first at 1m   |
| 5        | Single dynamic obstacle, 1m from start, simultaneous  |

---

## Key Nodes

| Node                  | Purpose                            |
|-----------------------|------------------------------------|
| `/controller_server`  | Runs the MPPI local planner        |
| `/planner_server`     | Global path planning               |
| `/amcl`               | Adaptive Monte Carlo Localization  |
| `/map_server`         | Serves the static map              |
| `/bt_navigator`       | Behavior tree navigation executor  |

---

## Authors

- Mario Schmidt
- Rares Constantin
- Alexandru Gheorghiu
- Andrei Slavescu

Supervision: B. F. Abaza, C. V. Doicin
Faculty of Industrial Engineering and Robotics (FIIR), POLITEHNICA Bucharest
