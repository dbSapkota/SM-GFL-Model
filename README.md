# Overview
This repo contains MATLAB files for the model and code used in the research paper \textit{"Optimal Singular Perturbation-based Model Reduction for Heterogeneous Power Systems"}.

The model is located at: System_LTI_Model/sys_6_bus.mat

The live script code (.mlx) for the Greedy algorithm is located at: Optimization Codes/Greedy Algorithm/Greedy.mlx

The live script code (.mlx) for the Nonlinear optimization is located at: Optimization Codes/Nonlinear Optimization/nonlinear_optimization.mlx

#### Note: Make sure to run the Greedy Algorithm before Nonlinear optimization (in the same workspace).

-------------------------------------------------------------------------------
# Model Overview

This repository contains a power system model with 56 dynamical states distributed as follows:

    18 synchronous machine states (2 machines × 9 states each)

    12 inverter states (2 inverters × 6 states each)

    26 line states (remaining states)

Note: A "dq" state represents a vector of two individual states: $\mathbf{x}_{dq} = [x_d^\top, x_q^\top]^\top \in \mathbb{R}^2$.

## External Inputs

The external input vector $\in \mathbb{R}^{12}$ is:

<img width="444" height="91" alt="image" src="https://github.com/user-attachments/assets/55442558-9fd4-46bb-9718-4d252480e3b2" />

## Outputs

The primary output vector $[w_1^\top, w_2^\top]^\top \in \mathbb{R}^2$ represents the frequencies at the two synchronous machine buses. Additional outputs such as line currents and bus voltages are also available.


## Grid-Following (GFL) Inverter Model

6th-order model, [1], with internal states:


<img width="297" height="59" alt="image" src="https://github.com/user-attachments/assets/770d2be9-7734-4a09-9814-f95533a3f1c4" />

Where:

    𝐈dq: inverter current outputs

    𝚪dq: current controller states

    Φ, Θ: Phase-Locked Loop (PLL) states for frequency dynamics and angle extraction

Both GFL inverters have identical parameter values.

## Synchronous Machine Model

9th-order model with internal states:

<img width="491" height="52" alt="image" src="https://github.com/user-attachments/assets/61641029-6298-436e-9df4-a6eec9260d7f" />


Where:

    Iᵀd, Iᵀq: stator circuit currents

    Iᵀfd, Iᵀ1d, Iᵀ1q: rotor circuit currents

    δ, ω: rotor angle and frequency

    G: governor valve/gate position

    τm: mechanical torque

Parameter Notes:

    Electrical parameters from Kundur Stability Book (Chapter 4, Example 4.1)

    All values in per unit

    Both machines have identical electrical parameters

    Mechanical parameters differ slightly (moment of inertia, governor time constant, droop coefficient)

## References

[1] D. Venkatramanan and S. Dhople, "Per-Unit Modeling via Similarity Transformation," in IEEE Transactions on Energy Conversion, vol. 38, no. 2, pp. 825-837, June 2023, doi: 10.1109/TEC.2022.3204933.

[2] P. Kundur, Power System Stability and Control, 1st ed., ser. The EPRI Power System Engineering Series. New York: McGraw-Hill, 1994.

v1.0
