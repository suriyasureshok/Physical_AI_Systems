# Week 1: Discrete Physics Step Cost Analysis

This module explores the **computational cost, numerical stability, and scalability limits**
of physics-based simulation using a minimal, controlled experiment.

The goal is to understand **why physics simulation becomes a bottleneck** in robotics,
reinforcement learning, and embodied AI systems — even before learning begins.

---

## Objective

To experimentally analyze how:
- timestep resolution (`dt`)
- numerical integration
- state size (number of bodies)

affect **performance, accuracy, and stability** in a physics simulation loop.

This week focuses on **first-principles understanding**, without using any physics engines
or reinforcement learning frameworks.

---

## Concepts Explored

- Discrete-time physics simulation
- Semi-implicit Euler integration
- Numerical drift and discretization error
- Energy drift as an integrator quality signal
- Performance cost per simulation step
- State explosion and memory-driven scaling limits
- Accuracy vs performance trade-offs

---

## Experiment Design

### Workload Simulation

We simulate a simplified physics system using:
- Explicit state vectors for position and velocity
- Constant acceleration (gravity-like force)
- A tight simulation loop that advances the system in discrete timesteps

The physics step is intentionally minimal to isolate **system-level behavior** rather than
model complexity.

---

### Experimental Parameters

The following parameters are varied independently:

- **Timestep (`dt`)**:  
  `0.1`, `0.01`, `0.001`

- **Total simulated time**:  
  Fixed (constant physical duration)

- **Number of bodies (`N`)**:  
  `1`, `10`, `100`, `1000`

Each experiment resets initial conditions to ensure fair comparison.

---

### Metrics Measured

- **Numerical drift**  
  Absolute error between simulated position and analytical ground truth

- **Energy drift**  
  Change in total mechanical energy (kinetic + potential)

- **Performance cost**  
  - Total simulation runtime
  - Time per simulation step (µs)

- **Scalability behavior**  
  Cost per step as a function of number of simulated bodies

---

## Key Observations

- Numerical error increases rapidly with larger timesteps due to discretization effects
- Smaller timesteps improve stability and accuracy but increase computational cost linearly
- Semi-implicit Euler integration is stable but not energy-conserving, leading to energy drift
- Cost per simulation step is approximately constant with respect to timestep
- Increasing the number of bodies causes state explosion and memory-bound performance degradation
- Simulation scalability breaks due to memory hierarchy limits, not arithmetic complexity

---

## Why This Matters

Physics simulation is the dominant bottleneck in:
- Robotics training loops
- Reinforcement learning rollouts
- Sim-to-real transfer pipelines

This experiment demonstrates that:
- Simulation fidelity is constrained by compute and memory
- Learning algorithms must operate within these physical and system limits
- Optimizing AI systems requires understanding simulation behavior, not just models

---

## Outcome

By the end of this week, we establish that **physics simulation is a constrained numerical system**
where accuracy, stability, and performance cannot be optimized simultaneously.

This understanding forms the foundation for:
- Simulator-aware reinforcement learning
- Hardware-conscious AI system design
- Real-world robotics and embodied intelligence research
