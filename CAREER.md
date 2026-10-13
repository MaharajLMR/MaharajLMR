# Career Materials — Maharaj L M R

## Resume Bullets

### Projects Section

**Resilient Warehouse AGV Fleet** · ROS 2 Jazzy, Nav2, C++, Python, Gazebo Harmonic
- Developed a 3-robot autonomous warehouse fleet with deadlock-free traffic management via a directed lane-graph reservation system; proved acyclicity of wait-for dependency eliminates all deadlocks
- Implemented WMS link resilience: task cache + automatic resync on reconnect; 23 unit tests, 0 collisions/deadlocks over 100 simulated runs
- Built Nav2 integration (AMCL + DWB + NavFn A*) with multi-robot namespacing in Gazebo Harmonic; fault injection CLI for failure scenario testing

**Clavel Delta Parallel Robot** · C++17, ROS 2, Gazebo Harmonic, Python
- Derived and implemented closed-form inverse/forward kinematics and analytical Jacobian for a Clavel delta robot in pure C++17; FK↔IK round-trip error < 1×10⁻⁹ m over 10,000 random points
- Solved half-angle (Weierstrass) IK formulation; corrected parallelogram forearm tangential offset (Lf_eff = √(Lf²−τ²)) critical for off-axis accuracy
- Implemented singularity detection via Jacobian condition number; CartesianCommander ROS 2 node rejects configurations with κ > 100; Gazebo SDF loop-closing joints for closed-chain physics

**5-DOF CNC Lathe Loading Arm** · ROS 2, MoveIt 2, Gazebo, STM32, Dynamixel
- Built digital twin of a competition robot arm (RANE SLD Hackathon 2026 — 1st runner-up, ₹75,000) automating CNC lathe loading/unloading in 4.75 s per cycle
- Implemented teach mode (keyboard jog → waypoint YAML) + MoveIt 2 replay for rapid cycle programming; STM32F446RE + Dynamixel XM430 firmware with hardware e-stop

**Weld Defect Detector** · YOLOv8, FastAPI, Python, OpenCV
- Built 5-class weld defect detection pipeline (crack, porosity, undercut, incomplete fusion) using YOLOv8n with mosaic/mixup augmentation; FastAPI inference server with phone browser camera client
- Implemented real-time inference endpoint (< 50 ms on GTX 1650); HTML5 getUserMedia capture → POST → canvas overlay

---

## LinkedIn Posts

### Post 1 — After P1 competition

> Just wrapped up building the simulation version of the AGV fleet I took to the Bonfiglioli Smart Motion Hackathon 2026 (2nd runner-up 🏆).
>
> The real robot was fun. The software was... improvised.
>
> So I rebuilt it properly in ROS 2 Jazzy:
> → 3 AGVs navigating a 30×20 m warehouse
> → Deadlock-free traffic via a directed lane graph (proved: wait-for graph is always acyclic → no deadlock possible)
> → WMS link resilience: the fleet keeps running when comms drop, resyncs automatically when they come back
> → 23 unit tests, 0 collisions over 100 runs
>
> Everything is open source. Numbers in the README are produced by scripts in the repo — nothing fabricated.
>
> Link in bio. #ROS2 #Robotics #AGV #Mechatronics #OpenSource

---

### Post 2 — After P2 delta robot

> Spent the last few weeks implementing the Clavel delta parallel robot from first principles.
>
> The challenge: parallel robots have closed kinematic chains. URDF can't represent them. You have to choose: SDF ball joints in Gazebo (physics closes the loop) or tree URDF + computed passive joints in RViz.
>
> I did both.
>
> The math highlights:
> → IK: half-angle (Weierstrass) substitution turns A·cosθ + B·sinθ = C into a clean quadratic
> → Critical bug I fixed: parallelogram forearms have a tangential offset τ — the effective length in the radial plane is Lf_eff = √(Lf² − τ²), not Lf. Off-axis error drops from 3.8 mm to < 1e-9 m after this fix.
> → FK: sphere intersection — subtract sphere equations pairwise to get planes, intersect for line, quadratic with sphere
>
> Result: < 1×10⁻⁹ m round-trip error over 10k random points. IK under 10 µs.
>
> Will be working on parallel robotics research at IIT Madras from November.
>
> #ParallelRobotics #DeltaRobot #Kinematics #ROS2 #CPP

---

### Post 3 — IIT Madras internship announcement

> Starting November, I'll be joining IIT Madras as a Research Intern in Parallel Robotics.
>
> This portfolio work (delta robot, AGV fleet, lathe arm) was partly preparation for that. Building things that work and that you can explain mathematically — that's the bar I was aiming for.
>
> If you're working on robotics (manipulation, navigation, kinematics), I'm always up to talk. DM me.
>
> #IITMadras #Robotics #Internship #Mechatronics

---

## Interview Q&A Bank

### "Tell me about your AGV fleet project."

The project simulates a 3-robot autonomous warehouse fleet in ROS 2 Jazzy and Gazebo Harmonic. The headline feature is resilience: when the warehouse management system link drops, robots finish their currently cached task using the last-validated Nav2 path, new idle events buffer internally, and when the link restores the fleet drains the buffer and resyncs completed task IDs. No tasks are lost, no manual intervention.

The other headline is deadlock-free traffic. I modelled the warehouse aisle network as a directed graph with 13 nodes and 28 edges. Each robot holds at most one edge reservation at a time — it releases the current edge before requesting the next. The proof: deadlock requires a cycle in the wait-for graph (A waits for B waits for … waits for A). Since no robot holds two edges simultaneously, the wait-for graph is always a forest, which is acyclic, so deadlock is impossible.

### "How does your delta robot IK work?"

For each of the three arms at azimuth φᵢ = (i−1)·120°, I project the wrist point onto the arm's radial-vertical plane and solve A·cosθ + B·sinθ = C for the upper arm angle. I use the Weierstrass half-angle substitution t = tan(θ/2), which converts it to a quadratic in t. Negative discriminant means the point is unreachable and I throw immediately.

The critical bug I found: parallelogram forearms have a tangential offset τ from the arm's radial plane. The effective forearm length in the radial-vertical plane is Lf_eff = √(Lf² − τ²), not Lf. Without this correction, off-axis errors were ~3.8 mm. After the fix: < 1e-15 m (floating-point noise).

### "What's the hardest technical problem you've solved?"

The closed-chain URDF problem for the delta robot. Standard URDF is a tree — it can't represent the parallelogram closure physically. My solution was to use two representations: SDF with ball joints to close the loop in Gazebo (Gazebo's constraint solver handles it), and a tree URDF with a passive joint publisher node that computes forearm angles from FK for RViz. This way the simulation is physically correct and the visualisation works in standard tools.

### "Why ROS 2 over ROS 1?"

DDS transport means no rosmaster single point of failure, which matters for multi-robot. Lifecycle nodes give deterministic startup/shutdown — important for fleet management where you need robots to come up in order. The action interface is built-in and cancellable. For real-time control, the real-time executor (rclcpp::executors::StaticSingleThreadedExecutor) is a clean path to determinism without rt-preempt patching.

### "How would you scale the AGV fleet to 50 robots?"

The lane graph approach hits a scalability wall once the warehouse has hundreds of intersections — the lock contention on edge reservations becomes a bottleneck, and the cost-based allocation becomes expensive. I'd switch to a hierarchical approach: zone managers own subgraphs and expose capacity signals, a global scheduler assigns robots to zones, within-zone traffic handled locally. For the WMS resilience layer the architecture already scales well since it's per-robot task caching.

### "What would you do differently on the delta robot?"

The Jacobian condition number check (κ > 100) is a conservative hard reject. In practice I'd want a softer response: scale down the velocity command when approaching singularity rather than rejecting outright. Also, the workspace estimate (47.7% of the ±12 cm cube) is conservative. I sampled joint angles uniformly — the reachable workspace in terms of task-space volume is larger if you allow non-uniform joint angle distributions tuned to the actual task.
