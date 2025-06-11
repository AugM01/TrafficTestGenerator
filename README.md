
# Test Automation for Interactive Scenarios via Promptable Traffic Simulation

## Paper Summary

**Test Automation for Interactive Scenarios via Promptable Traffic Simulation**

Autonomous vehicle (AV) planners must be rigorously tested to ensure safe deployment, particularly in interactive scenarios involving uncertain human behavior. This work proposes a novel framework for **automatically generating realistic, diverse, and safety-critical test scenarios** using a **data-driven traffic simulator (ProSim)**.

Existing approaches often struggle to balance the competing objectives of realism, interactivity, diversity, controllability, and efficiency, typically favoring one at the expense of the others. This work addresses that challenge by unifying these aspects within a single, scalable system.

This paper proposes a framework to overcome this tradeoff. The key idea is to leverage a **promptable traffic model** to **parametrize complex human driver behaviors** through **low-dimensional final position goal prompts**, and to simulate their interactions with an AV in **closed-loop**. A **Bayesian Optimization (BO)** module then efficiently explores the space of goal prompts to assign to other agents to uncover scenarios that stress-test the AV planner.

### Main Contributions
- **Modular pipeline** for automated planner evaluation using goal-based behavioral prompts.
- **Efficient discovery** of safety-critical interactions via BO over a low-dimensional domain.
- **Planner-agnostic** design: applicable to any AV planner with minimal assumptions.

---

## Method Overview
<!-- ![Method Overview](Imgs_Paper/overview.png) -->
<p align="center">
  <img src="imgs/overview.png" alt="Poster Preview" width="600"/>
</p>

This framework is composed of three main modules:
- **Prompt Generator**: given fixed initial conditions, this module uses Bayesian Optimization to efficiently identify critical goal prompts for other agents within a low-dimensional domain to give as input to a promptable traffic simulator.
- **Episode Generator**: generates simulations where the AV planner is tested against other agents governed by [ProSim](https://arxiv.org/abs/2409.05863) in a closed-loop manner.
- **Episode Scorer**: evaluates criticality and informativeness of generated episodes by assigning a score which will be used to guide BO in the next iterations.

In other words, given a fixed initial condition, the framework outputs a set of informative and safety-critical episodes by optimizing over a user-defined domain the final goal to give to other agents.
<!-- ![Goal Domain](Imgs_Report/3_methodology/bayesian_optimization/goal_domain.png) -->
<p align="center">
  <img src="imgs/goal_domain.png" alt="Poster Preview" width="600"/>
</p>

---

## Examples of Generated Episodes

<!-- ### 🧪 Experimental Setup
- **AV Planner**: MPC-based (2 Hz), assumes constant-velocity, lane-centered behavior of others.
- **Simulator**: [ProSim](https://arxiv.org/abs/2409.05863) (pretrained, no fine-tuning), adapted for [CommonRoad](https://commonroad.in.tum.de/).
- **Scenarios**: 3 highway settings with different initial configurations of one other vehicle.
    -  **Front**: Other agent is in front of the AV in the same lane |
    - **Front-Right**: Other agent is ahead, in the adjacent right lane |
    - **Behind**: Other agent is in the same lane, but behind the AV |
- **Optimization**: 75 BO iterations per scenario (Matern kernel, UCB acquisition).
- **Metrics**:
  - **Safety-Criticality**: Collision rate, Min. Distance, Time-To-Collision (TTC)
  - **Diversity**: Average pairwise trajectory distance (ego & other agent)

--- -->

<p align="center">
  <img src="imgs\1073_gif.gif" alt="Poster Preview" width="600"/>
</p>
<p align="center">
  <img src="imgs\1007_gif.gif" alt="Poster Preview" width="600"/>
</p>
<p align="center">
  <img src="imgs\1036_gif.gif" alt="Poster Preview" width="600"/>
</p>
<p align="center">
  <img src="imgs\1062_gif.gif" alt="Poster Preview" width="600"/>
</p>
<p align="center">
  <img src="imgs\1067_gif.gif" alt="Poster Preview" width="600"/>
</p>
