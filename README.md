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

- **23/23** unit tests · **0 deadlocks** over 100 random runs · **0 collisions**
- Lane graph: 13 nodes, 28 directed edges, O(1) reservation check
- Nav2 stack: AMCL + DWB local planner + NavFn A* + slam\_toolbox map

[![resilient-agv-fleet](https://img.shields.io/badge/repo-resilient--agv--fleet-181717?style=flat&logo=github)](https://github.com/MaharajLMR/resilient-agv-fleet)

---

### Clavel Delta Parallel Robot · ROS 2 Jazzy / C++17 / Gazebo Harmonic

Closed-form IK, FK (sphere-intersection), and analytical Jacobian for a 3-DOF Clavel delta robot in pure C++17 — no numerical solver, no ROS dependency in the math layer. Singularity detection via Jacobian condition number. Gazebo simulation with SDF loop-closing joints.

- FK(IK(p)) round-trip error **< 1 × 10⁻⁹ m** over 10,000 random in-workspace points  
- IK computation time **< 10 µs** on AMD Ryzen 7
- Jacobian condition number at workspace centre: **1.45** (far from singularity)
- Workspace: 47.7 % of ±12 cm XY, Z −35 to −65 cm cube

[![ros2_parallel_robots](https://img.shields.io/badge/repo-ros2__parallel__robots-181717?style=flat&logo=github)](https://github.com/MaharajLMR/ros2_parallel_robots)

---

### 5-DOF CNC Lathe Loading Arm · ROS 2 / MoveIt 2 / Gazebo Harmonic
> *DriveNext RANE SLD Hackathon 2026 — 1st runner-up, ₹75,000*

Digital twin of a physical 5-DOF serial arm that automates CNC lathe loading/unloading. Teach mode lets an operator record a cycle via keyboard jog in minutes; the ROS 2 replay node executes it with MoveIt 2 trajectory planning. STM32 + Dynamixel XM430 hardware.

- Load/unload cycle time: **4.75 s** (sim)
- Max reach: 0.985 m · Payload: 5 kg
- Teach mode: 8-step cycle recorded → replayed with sub-degree joint accuracy

[![cnc-lathe-arm](https://img.shields.io/badge/repo-cnc--lathe--arm-181717?style=flat&logo=github)](https://github.com/MaharajLMR/cnc-lathe-arm)

---

### Weld Defect Detector · YOLOv8 / FastAPI / Phone Camera

5-class weld defect detection (crack, porosity, undercut, incomplete fusion, good weld) using YOLOv8n. FastAPI inference server with phone browser camera client — point your phone at a weld, get real-time bounding boxes.

- Training pipeline: augmentation + YOLOv8n → ONNX export
- Inference server: POST /predict → JSON detections in < 50 ms on GTX 1650
- Live phone camera demo via HTML5 getUserMedia + fetch

[![weld-defect-detector](https://img.shields.io/badge/repo-weld--defect--detector-181717?style=flat&logo=github)](https://github.com/MaharajLMR/weld-defect-detector)

---

## Tech Stack

| Domain | Tools |
|---|---|
| Robotics middleware | ROS 2 Jazzy · Nav2 · MoveIt 2 · slam\_toolbox |
| Simulation | Gazebo Harmonic · RViz 2 |
| Systems / kinematics | C++17 · CMake · Eigen3 |
| Orchestration / analysis | Python 3.12 · NumPy · OpenCV · Matplotlib |
| CV / ML | YOLOv8 (Ultralytics) · ONNX |
| Embedded | STM32 (Nucleo-F446RE) · Dynamixel Protocol 2.0 · Arduino |
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
