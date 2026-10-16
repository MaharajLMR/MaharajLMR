<div align="center">

# Maharaj L M R

**Mechatronics Engineer · Robotics Software Developer**  
3rd Year B.E. Mechatronics · Chennai Institute of Technology  
Research Intern, Parallel Robotics · IIT Madras (Nov 2026)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Maharaj_LMR-0A66C2?style=flat&logo=linkedin)](https://linkedin.com/in/maharaj-lmr)
[![Email](https://img.shields.io/badge/Email-lmrrajan2005%40gmail.com-EA4335?style=flat&logo=gmail)](mailto:lmrrajan2005@gmail.com)

</div>

---

## About

I build real robotic systems — warehouse fleets, parallel robots, industrial arms — and take them from hardware to simulation to production-quality ROS 2 code. I care about correctness (closed-form math before numerical approximation), testability (every claim is a script that runs), and robustness (systems that degrade gracefully under failure).

Currently focused on: parallel robot kinematics, multi-robot coordination, and vision-based inspection.

---

## Projects

### Resilient Warehouse AGV Fleet · ROS 2 Jazzy / Nav2 / Gazebo Harmonic
> *Bonfiglioli Smart Motion Hackathon 2026 — 2nd runner-up, ₹1 lakh*

3 differential-drive AGVs navigate a 30×20 m simulated warehouse. The fleet keeps running when the WMS link drops — tasks are cached and resynced automatically on reconnect. Deadlock-free traffic via a directed lane graph with proven-acyclic wait-for dependency.

- **54/54** unit tests · **0 deadlocks** across 100 random 3-robot traversals · **0 collisions** in a 600 s fleet sim
- **390 tasks/hr** with 3 robots; throughput scales 224 → 439 → 671 tasks/hr from 1 → 3 robots
- Lane graph: 13 nodes, 28 directed edges, O(1) reservation check
- Nav2 stack: AMCL + DWB local planner + NavFn A* + slam\_toolbox map

[![resilient-agv-fleet](https://img.shields.io/badge/repo-resilient--agv--fleet-181717?style=flat&logo=github)](https://github.com/MaharajLMR/resilient-agv-fleet)

---

### Clavel Delta Parallel Robot · ROS 2 Jazzy / C++17 / Gazebo Harmonic

Closed-form IK, FK (sphere-intersection), and analytical Jacobian for a 3-DOF Clavel delta robot in pure C++17 — no numerical solver, no ROS dependency in the math layer. Singularity detection via Jacobian condition number. Gazebo simulation with SDF loop-closing joints.

- FK(IK(p)) round-trip error **< 1 × 10⁻⁹ m** over 10,000 random in-workspace points  
- IK computation time **≈ 0.2 µs** per call (C++17 −O2, Ryzen 7) — ~480× faster than a numerical solver
- Also: 6-UPS Stewart platform (closed-form IK, Newton–Raphson FK), min-jerk trajectories with 72% lower peak jerk
- Jacobian condition number at workspace centre: **1.45** (far from singularity)
- Workspace: 47.7 % of ±12 cm XY, Z −35 to −65 cm cube

[![ros2_parallel_robots](https://img.shields.io/badge/repo-ros2__parallel__robots-181717?style=flat&logo=github)](https://github.com/MaharajLMR/ros2_parallel_robots)

---

### 5-DOF CNC Lathe Loading Arm · ROS 2 / MoveIt 2 / Gazebo Harmonic
> *DriveNext RANE SLD Hackathon 2026 — 1st runner-up, ₹75,000*

Industrial design study of a 5-DOF serial arm that automates CNC lathe loading/unloading, grown from my hackathon concept. Teach mode lets an operator record a cycle via keyboard jog in minutes; the ROS 2 replay node executes it with MoveIt 2 trajectory planning. STM32 + Dynamixel XM430 hardware.

- **62/62** unit tests · estimated load/unload cycle **5.55 s** · 0.985 m reach
- Straight-line Cartesian insert/retract (0.000 mm deviation), diameter-sorted batch scheduling (0 gripper changeovers)
- Fault monitor (5 fault codes) and an OPC-UA server for SCADA integration

[![cnc-lathe-arm](https://img.shields.io/badge/repo-cnc--lathe--arm-181717?style=flat&logo=github)](https://github.com/MaharajLMR/cnc-lathe-arm)

---

### Weld Defect Detector · YOLOv8 / FastAPI / Phone Camera

5-class weld defect detection (crack, porosity, undercut, incomplete fusion, good weld) using YOLOv8n. FastAPI inference server with phone browser camera client — point your phone at a weld, get real-time bounding boxes.

- Training pipeline: augmentation + YOLOv8n → ONNX export
- Inference server: POST /predict → JSON detections (target < 50 ms on GTX 1650; model training pending dataset)
- Live phone camera demo via HTML5 getUserMedia + fetch

*Repo goes public once the dataset is collected with my teammate.*

---

## Tech Stack

| Domain | Tools |
|---|---|
| Robotics middleware | ROS 2 Jazzy · Nav2 · MoveIt 2 · slam\_toolbox |
| Simulation | Gazebo Harmonic · RViz 2 |
| Systems / kinematics | C++17 · CMake · gtest |
| Orchestration / analysis | Python 3.12 · NumPy · OpenCV · Matplotlib |
| CV / ML | YOLOv8 (Ultralytics) · ONNX |
| Industrial | OPC-UA (asyncua) · FastAPI |
| Testing | gtest · pytest · launch\_testing · GitHub Actions |
| Version control | Git · GitHub |

---

## Competition Record

| Year | Event | Result | Award |
|---|---|---|---|
| 2026 | Bonfiglioli Smart Motion Hackathon | 2nd runner-up | ₹1,00,000 |
| 2026 | DriveNext RANE SLD Hackathon | 1st runner-up | ₹75,000 |

---

## Education & Research

**B.E. Mechatronics Engineering** · Chennai Institute of Technology · 2023–2027  
**Research Intern, Parallel Robotics** · IIT Madras · Nov 2026 →

---

<div align="center">
<sub>All project numbers are produced by scripts in each repo — nothing is fabricated.</sub>
</div>
