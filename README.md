# Analog PID Stabilization of a Quadcopter (Roll Axis)

**Author:** Akram Bouziane  
**CPGE MP – Errachidia, Morocco**  
**TIPE 2025–2026 – Theme “Cycles, Loops”**

This repository presents a formal electromechanical study of an analog PID controller for roll-axis stabilization of a quadcopter driven by brushed DC motors. It revisits the original TIPE project and adds quantitative values so that every resistor and capacitor in the corrector can be traced back to a physical requirement.

### Problem
A free quadcopter is mechanically unstable. Linearized around hover, the roll dynamics reduce to  
\( I_x \ddot{\varphi} = k_u u(t) \).  
Without feedback the angle drifts linearly under any initial angular-rate disturbance.

### Approach
The study closes the loop with a classical PID law and obtains the governing equation of the original project:

\[
\ddot{\varphi} + k K_d \dot{\varphi} + k K_p \varphi + k K_i \int_0^t \varphi(\tau)\,d\tau = 0
\qquad (k = k_u/I_x)
\]

Two deliberate simplifications keep the scope manageable:
- **H1** – Motors are ordinary brushed DC motors (no ESC or PWM stage).
- **H2** – The error signal \(e(t)\) is treated as an already-available voltage (no sensor chain).

### Main results
- Physical derivation of the actuator gain \(k_u \approx 0.072\,\mathrm{N\cdot m/V}\)
- Motor mechanical time constant \(\tau_m \approx 45\,\mathrm{ms}\) → closed-loop bandwidth limited to \(\approx 0.6\,\mathrm{Hz}\)
- Complete analog topology (subtractor + P / leaky-I / filtered-D + summer)
- Final component values (RC ≈ 270 ms) chosen from the bandwidth budget and Routh-Hurwitz conditions
- Stability confirmed by pole placement and time-domain simulation of an initial-rate disturbance

### Limitations (honest)
- Theoretical analysis and numerical simulation only — no physical board was built
- Single-axis model (gyroscopic coupling omitted)
- No aerodynamic damping term
- Sensor noise and real measurement dynamics ignored

### Repository contents
```
├── README.md
├── formal_study.pdf          # Full 17-page formal document
├── schematic/                # Circuit diagram with final values
├── simulation/               # Validation scripts / notebooks
└── original_tipe/            # Reference material from the original project
```

All notation and the governing equation follow the original TIPE project exactly. Numerical values are illustrative and can be replaced by measured parameters from a real platform.
