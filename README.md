v1.0 

This repo contains MATLAB files for the model and code used in the research paper "Optimal Singular Perturbation-based Model Reduction for Heterogeneous Power Systems"

The model is located at: System_LTI_Model/sys_6_bus.mat

The live script code (.mlx) for the Greedy algorithm is located at: Optimization Codes/Greedy Algorithm/Greedy.mlx

The live script code (.mlx) for the Nonlinear optimization is located at: Optimization Codes/Nonlinear Optimization/nonlinear_optimization.mlx

Power System Model
Model Overview

This repository contains a power system model with 56 dynamical states distributed as follows:

    18 synchronous machine states (2 machines × 9 states each)

    12 inverter states (2 inverters × 6 states each)

    26 line states (remaining states)

Note: A bold-face "dq" state represents a vector of two individual states: $\mathbf{x}_{dq} = [x_d^\top, x_q^\top]^\top \in \mathbb{R}^2$.
External Inputs

The external input vector $\in \mathbb{R}^{12}$ is:

[V₁,fdᵀ, 𝐈*dq,inv₁ᵀ, P₁,refᵀ, 𝐈*dq,load₁ᵀ,
 V₂,fdᵀ, 𝐈*dq,inv₂ᵀ, P₂,refᵀ, 𝐈*dq,load₂ᵀ]ᵀ
 
Outputs

The primary output vector $[w_1^\top, w_2^\top]^\top \in \mathbb{R}^2$ represents the frequencies at the two synchronous machine buses. Additional outputs such as line currents and bus voltages are also available.
Component Models
Grid-Following (GFL) Inverter Model

6th-order model with internal states:
text

[𝐈dqᵀ, 𝚪dqᵀ, Φᵀ, Θᵀ]ᵀ ∈ ℝ⁶

Where:

    𝐈dq: inverter current outputs

    𝚪dq: current controller states

    Φ, Θ: Phase-Locked Loop (PLL) states for frequency dynamics and angle extraction

Both GFL inverters have identical parameter values.
Synchronous Machine Model

9th-order model with internal states:
text

[Iᵀd, Iᵀq, Iᵀfd, Iᵀ1d, Iᵀ1q, δᵀ, ωᵀ, Gᵀ, τᵀm]ᵀ ∈ ℝ⁹

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
