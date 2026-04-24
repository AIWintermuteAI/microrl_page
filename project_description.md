Integrating RL Policies on Microcontrollers with ROS 2 via MicroROS

Reinforcement learning policies have shown great promise for robotics locomotion, far exceeding the limits of what is possible with classic control theory. The spotlight has always been on large policies, meant to run on relatively powerful single-board computers like Raspberry Pi or Jetson Nano. In this talk, we instead focus on smaller policies, optimizing them to run on microcontrollers and package them as MicroROS control nodes. The talk includes our experience deploying lightweight RL policies to an open-source robotic platform, sharing our open-source tools, lessons learned, and practical considerations for the ROS 2 community.

| Section | Time |
|---------|------|
| Introduction | 4 min |
| Background | 4 min |
| Technical Approach and Current Progress| 12 min |
| Challenges and Future work| 6 min |
| Q&A | 4 min |
| **Total** | **30 min** |

Introduction (4 min)
We open with the gap in ROS 2 for edge AI: RL policies deployment currently focuses on SBCs, not microcontrollers. This section establishes why this matters for locomotion control and what becomes possible when RL meets MCUs.

Background (4 min)
After reviewing existing RL deployments on Raspberry Pi/Jetson series, we explain why MCU deployment is fundamentally different (memory, compute, power constraints). We also introduce MicroROS as the way to bridge tiny constrained devices with larger ROS ecosystem.

Technical Approach and Current Progress (12 min)
Here we walk through the framework used, RL policies tried, PyTorch to TensorFlow Lite Micro conversion, model and runtime optimization pipeline, and MicroROS node integration. Attendees will see the simulation-to-hardware workflow and how policies communicate with ROS 2 stack. We also share what's working today: simulation benchmarks, MicroROS bridge prototype, and open-source repository. We will also showcase an open-source off-the-shelf robot, which runs RL policy for movement and is remote controlled using ROS 2.

Challenges and Future work (6 min)
Next, we discuss roadblocks encountered so far: memory constraints, latency trade-offs, and MicroROS compatibility quirks. Attendees learn what didn't work and why - valuable for others attempting similar deployments. We outline how attendees can contribute via trying this on their own hardware, feedback, or PRs. The section closes with a call-to-action for community collaboration.

Q&A (4 min)
We open the floor for questions on technical details, timeline, or how to get involved with the project.

The goal is to demonstrate a feasible path for running RL policies on MCUs within the ROS 2 ecosystem - something currently sparsely documented. By presenting at ROSCon, we aim to: (1) show the ROS community this is possible, (2) share our simulation-validated methodology for others to build on, and (3) encourage community to build on our lessons with their own hardware.

This talk is for anyone interested in edge AI within the ROS ecosystem: from beginners exploring RL to experienced embedded developers. Attendees will learn what's currently possible when combining reinforcement learning with microcontrollers, what tools exist today (and what's still needed), and how to contribute to the open-source project. No deep RL or embedded expertise required; we explain concepts accessibly while providing technical depth for advanced users.

This talk addresses a critical gap in ROS 2: how to deploy RL policies on the MCU portion of hybrid SBC+MCU systems—the architecture used in production robots. Currently, RL-based locomotion control runs entirely on SBCs, missing the opportunity for deterministic, real-time inference on the MCU. This matters for open-source robotics because it enables a cleaner separation of concerns: SBC handles perception/planning, MCU handles real-time control. By presenting our MicroROS integration approach on Arduino Uno Q, we demonstrate a production-ready pattern the community can adopt.

RL on SBCs (Established):
Projects like ROS 2 navigation with RL policies routinely being deployed on Jetson Orin series and similar SBCs.

RL on MCUs (Research and Exploration):
    Shawn Hymel (2026) is exploring RL for balance robots on ESP32, training in PyBullet/Stable-Baselines3 and deploying to hardware. Early results show 10+ minute balance times, but sim2real gap remains a key challenge.
    DigiKey/ST Tutorial (2023) demonstrates PPO-based swing-up on inverted pendulum using XIAO ESP32S3. Balancing proved too difficult; scope was reduced to swing-up only. Training occurs on CPU/GPU, inference on MCU.
    Molchanov et al. (2019) transfer RL policies from simulation to multiple Crazyflie quadrotors (STM32F405, Cortex-M4), but without ROS 2 integration.
    RLtools (Eschmann et al., 2023) provides a C++ RL library with MCU inference benchmarks (Teensy 4.1: 64μs, ESP32: 279μs). Claims "first-ever deep RL training directly on microcontroller," but focuses on standalone deployment without ROS.

MicroROS on MCUs (Established):
MicroROS runs on STM32, ESP32, and similar MCUs for sensor nodes and control loops—but no documented RL inference examples exist.

Our Contribution: We bridge these gaps by combining (1) quantized RL policies optimized for MCU memory constraints, (2) MicroROS for external ROS 2 communication (enabling integration with navigation stacks and perception systems), and (3) hybrid MPU+MCU deployment patterns (Arduino Uno Q as one example). Unlike prior work, our framework targets ROS 2 ecosystem integration rather than standalone MCU deployment.

I'm not presenting any software tools, libraries, projects or hardware as a single focus of the talk. However I do use the following (not exhaustive list):
- Arduino Uno Q (deployment hardware)
- ESP32 and ESP32-S3 (deployment hardware)
- PyTorch (NN training)
- Tensorflow Lite for Microcontrollers (edge deployment)
- MuJoCo (simulation)
- ROS 2 (control and communication)