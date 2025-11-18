
This repo contains MATLAB files for the model and code used in the research paper "Optimal Singular Perturbation-based Model Reduction for Heterogeneous Power Systems"

The model is located at: System_LTI_Model/sys_6_bus.mat

The live script code (.mlx) for the Greedy algorithm is located at: Optimization Codes/Greedy Algorithm/Greedy.mlx

The live script code (.mlx) for the Nonlinear optimization is located at: Optimization Codes/Nonlinear Optimization/nonlinear_optimization.mlx


The overall model has $\textbf{56}$ dynamical states, of which 18 are synchronous machine states, 12 are inverter states and remaining are line states. Here, a bold-face "dq" state represents a vector of two individual states, i.e., $\mathbf{x}_{dq} =  [x_d^\top, x_q^\top]^\top \in \mathbb{R}^2$.

The external input vector is $ 
\begin{aligned}
    &[V_{1,fd}^\top ,  \mathbf{I}_{dq, inv_1}^{\star \top}, P_{1,ref}^\top,,\mathbf{I}_{dq, load_1}^{\star\top },\\
    &V_{2,fd}^\top , \mathbf{I}_{dq, inv_2}^{\star\top },P_{2,ref}^\top, \mathbf{I}_{dq, load_2}^{\star\top }]^\top  
    \in \mathbb{R}^{12}
\end{aligned} $

The output vector $[w_1^\top, w_2^\top]^\top \in \mathbb{R}^2 $ represent the frequencies at the two synchronous machine buses. Other outputs are also possible (such as line currents, bus voltages etc.). The load consumes current based on the reference current value.

A $6-th$ order model of GFL as derived in \cite{per_unit_inverter_modeling} is used in this work. The interal states of the inverter are:
\begin{equation}
   \begin{aligned}
    &[\mathbf{I}_{dq}^\top, \mathbf{\Gamma}_{dq}^\top,\Phi^\top,\Theta^\top]^\top \in \mathbb{R}^6
\end{aligned} 
\label{inverter_states}
\end{equation}
where, $\mathbf{I}_{dq}$ are inverter current outputs, $\mathbf{\Gamma}_{dq}$ are current controller states. Frequency dynamics are governed by a phase-locked-loop (PLL), which extracts the angle $\Theta$ whose dynamics are represented by $\Phi$. The two GFL inverters have the same parameter values.

A synchronous machine is represented by a $9-th$ order model whose internal states are given as
\begin{equation}
    \begin{aligned}
     &[I_d^\top   ,I_q^\top   , I_{fd}^\top   ,I_{1d}^\top   , I_{1q}^\top   , \delta^\top, \omega^\top   , G^\top   , \tau_m^\top    ]^\top \in \mathbb{R}^{9}  
    \end{aligned}
    \label{sm_states}
\end{equation}
where, $[I_d^\top   ,I_q^\top ]$ represent the stator circuit currents, $[I_{fd}^\top   ,I_{1d}^\top   , I_{1q}^\top]^\top$ represent the rotor circuit currents,  $\delta$ and $ \omega$ represent rotor angle and frequency respectively, $G$ is the governor valve/gate position state and $\tau_m$ is the mechanical torque. The electrical parameters for the machine are obtained from \cite{kundur_stability_book} (Chapter 4: Synchronous Machine Parameters) Page 153-Example 4.1. All the values are in per unit.
The two synchronous machines in the network have the same electrical parameters (Winding resistance, inductances etc.) but slightly different mechanical parameters (MOI, governor time constant, and droop coefficient). 
