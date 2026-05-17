Experimental Dataset: SAIM XPLORER-AC Modular Autonomous Mobile Robot

Overview
This repository contains the evaluation dataset for the SAIM XPLORER-AC, a modular autonomous mobile robot utilizing a ROS 2-based navigation architecture. The dataset consists of 24 unique experimental trials designed to rigorously evaluate the performance, stability, and computational efficiency of the local trajectory planner under varying environmental constraints and algorithmic configurations.

Methodology & Experimental Design
The testing framework isolates specific kinematic behaviors and obstacle-avoidance capabilities. By systematically altering core navigation parameters across five distinct scenarios, this dataset provides empirical evidence for optimizing the controller's behavior.
Below is the breakdown of the experimental scenarios, the parameters tuned, and the primary evaluation objectives for each test.

Scenario 1: Translational Kinematics & Velocity Scaling
Description: The robot executes a pure translational trajectory over a distance of 3 meters.
Parameters Modified: Maximum linear velocity (vx).
Evaluation Objective: To measure longitudinal tracking accuracy and steady-state error at varying speeds. We are specifically looking for controller stability, identifying the threshold where high velocities introduce overshooting, oscillations, or actuator saturation.

Scenario 2: Angular Kinematics & Sharp Cornering
Description: The robot performs 90-degree rotational maneuvers distributed over a 2-meter navigational path
Parameters Modified: Angular velocities (omega_z, omega_y).
Evaluation Objective: To assess the robot's heading accuracy and rotational stability. We are observing the path deviation during sharp turns and evaluating how aggressively the robot can corner without losing localization or destabilizing the chassis.

Scenario 3: Static Obstacle Clearance
Description: Navigation around a single static obstacle positioned 1 meter from the robot's initial pose.
Parameters Modified: Obstacle Cost Critic and Cost Weight.
Evaluation Objective: To determine the sensitivity of the local planner to costmap gradients. We are analyzing the trade-off between safety and efficiency, looking for the optimal parameter weights that maintain a safe clearance buffer without generating excessively wide, inefficient trajectories.

Scenario 4: Multi-Obstacle Slalom Navigation
Description: Complex path planning through a sequence of three static obstacles spaced 1 meter apart, with the first obstacle located 1 meter from the start point.
Parameters Modified: Temperature (T) and Gamma (gamma).
Evaluation Objective: To evaluate the exploration versus exploitation balance within the sampling algorithm. We are monitoring how the temperature parameter affects the spread of sampled trajectories, and how gamma influences the cost function's aggressiveness in tightly constrained, highly penalizing environments.

Scenario 5: Dynamic Obstacle Evasion
Description: The robot must evade a moving obstacle. The robot begins 1 meter away from the obstacle, and both initiate movement simultaneously.
Evaluation Objective: To analyze the system's real-time computational efficiency and reaction latency. We are identifying the minimum batch size required to successfully generate collision-free trajectories against moving threats without inducing controller lag or CPU bottlenecking.
