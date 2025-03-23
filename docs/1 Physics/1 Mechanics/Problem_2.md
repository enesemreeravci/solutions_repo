## Problem 2

**Investigating the Dynamics of a Forced Damped Pendulum**

---

### 1. Theoretical Foundation

#### Deriving the Equations of Motion

The forced damped pendulum is governed by a second-order nonlinear differential equation that accounts for gravity (restoring force), damping (friction), and an external periodic force. The equation of motion is:

$\frac{d^2 \theta}{dt^2} + b \frac{d \theta}{dt} + \frac{g}{L} \sin(\theta) = F \cos(\omega t)$

Where:
- $\theta$: Angular displacement (radians)
- $b$: Damping coefficient (s$^{-1}$)
- $g$: Gravitational acceleration (m/s$^2$)
- $L$: Pendulum length (m)
- $F$: Driving force amplitude (s$^{-2}$)
- $\omega$: Driving frequency (rad/s)
- $t$: Time (s)

##### Small-Angle Approximation

For small angles ($\theta \ll 1$), $\sin(\theta) \approx \theta$, simplifying the equation to a linear form:

$\frac{d^2 \theta}{dt^2} + b \frac{d \theta}{dt} + \omega_0^2 \theta = F \cos(\omega t)$

Where $\omega_0 = \sqrt{\frac{g}{L}}$ is the natural frequency. The steady-state solution for this driven, damped harmonic oscillator is:

$\theta(t) = A \cos(\omega t - \phi)$

Where:
- Amplitude: $A = \frac{F}{\sqrt{(\omega_0^2 - \omega^2)^2 + (b \omega)^2}}$
- Phase: $\phi = \tan^{-1}\left(\frac{b \omega}{\omega_0^2 - \omega^2}\right)$

##### Resonance

Resonance occurs when the driving frequency $\omega$ approaches the natural frequency $\omega_0$, maximizing amplitude when $\omega = \sqrt{\omega_0^2 - \frac{b^2}{2}}$ (for underdamped cases, $b < 2 \omega_0$). This amplifies energy transfer from the external force to the pendulum.

#### Family of Solutions

The nonlinear equation admits a range of behaviors—periodic, quasiperiodic, and chaotic—depending on $b$, $F$, and $\omega$. For small $F$ and $b$, motion is regular; for larger values, chaos emerges, as explored below.

---

### 2. Analysis of Dynamics

#### Parameter Influence

- **Damping Coefficient ($b$)**: Low $b$ allows sustained oscillations; high $b$ suppresses motion, leading to decay.
- **Driving Amplitude ($F$)**: Small $F$ produces linear-like motion; large $F$ drives nonlinearity, potentially causing chaos.
- **Driving Frequency ($\omega$)**: Near $\omega_0$, resonance amplifies motion; far from $\omega_0$, motion may desynchronize or become chaotic.

#### Transition to Chaos

For large $F$ or specific $\omega$, the nonlinear $\sin(\theta)$ term dominates, leading to unpredictable motion. Chaotic behavior is characterized by sensitivity to initial conditions and aperiodic trajectories, observable in phase space or Poincaré sections.

---

### 3. Practical Applications

#### Real-World Scenarios

- **Energy Harvesting**: Pendulum-based devices capture ambient vibrations. *Example*: A pendulum in a watch converts wrist motion into energy.
- **Suspension Bridges**: Oscillations from wind (forcing) can resonate or destabilize structures.
- **Oscillating Circuits**: Electrical analogs mimic pendulum dynamics in signal processing.

#### Adaptations

- **Nonlinear Damping**: Replace $b \frac{d \theta}{dt}$ with $b \left| \frac{d \theta}{dt} \right| \frac{d \theta}{dt}$ for realistic friction.
- **Variable Forcing**: Use $F(t)$ for non-periodic inputs like gusts.

---

### 4. Implementation

#### Graphical Outputs

**Figure 1: Motion vs Time (Resonance Case)**  
![Motion vs Time](graph.png)

**Figure 2: Phase Portrait (Chaotic Case)**  
![Phase Portrait](graph2.png)

**Figure 3: Poincaré Section (Transition to Chaos)**  
![Poincaré Section](graph3.png)

#### Python Simulation

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

g = 9.81  # m/s²
L = 1.0   # m
omega0 = np.sqrt(g / L)

def pendulum_deriv(state, t, b, F, omega):
    theta, theta_dot = state
    dtheta_dt = theta_dot
    dtheta_dot_dt = -b * theta_dot - (g / L) * np.sin(theta) + F * np.cos(omega * t)
    return [dtheta_dt, dtheta_dot_dt]

t = np.linspace(0, 50, 1000)
initial_conditions = [0.1, 0]  # [theta, theta_dot]

# Resonance Case
sol_res = odeint(pendulum_deriv, initial_conditions, t, args=(0.1, 0.2, omega0))
plt.figure(figsize=(10, 6))
plt.plot(t, sol_res[:, 0], label='θ(t), b=0.1, F=0.2, ω=ω₀')
plt.xlabel('Time (s)')
plt.ylabel('Angle (rad)')
plt.title('Motion vs Time (Resonance)')
plt.grid(True)
plt.legend()
plt.show()

# Chaotic Case
sol_chaos = odeint(pendulum_deriv, initial_conditions, t, args=(0.2, 1.5, 1.2))
plt.figure(figsize=(10, 6))
plt.plot(sol_chaos[:, 0], sol_chaos[:, 1], 'b-', alpha=0.5)
plt.xlabel('θ (rad)')
plt.ylabel('dθ/dt (rad/s)')
plt.title('Phase Portrait (Chaotic, b=0.2, F=1.5, ω=1.2)')
plt.grid(True)
plt.show()

# Poincaré Section
poincare_theta = []
poincare_theta_dot = []
for i in range(len(t)):
    if abs(np.mod(t[i] * 1.2 / (2 * np.pi), 1) - 0) < 0.01:  # Sample at driving period
        poincare_theta.append(sol_chaos[i, 0])
        poincare_theta_dot.append(sol_chaos[i, 1])
plt.figure(figsize=(10, 6))
plt.scatter(poincare_theta, poincare_theta_dot, s=5, c='r', alpha=0.5)
plt.xlabel('θ (rad)')
plt.ylabel('dθ/dt (rad/s)')
plt.title('Poincaré Section (Chaotic)')
plt.grid(True)
plt.show()
```
*Code simulates pendulum motion, phase portraits, and Poincaré sections.*

#### Graphical Interpretation

- **Figure 1**: Shows resonance with large amplitude near $\omega = \omega_0$.
- **Figure 2**: Phase portrait reveals chaotic looping for high $F$.
- **Figure 3**: Poincaré section shows scattered points, indicating chaos.

---

### 5. Limitations and Extensions

#### Limitations

- **Linear Approximation**: Small-angle solution misses nonlinear effects.
- **Simplified Damping**: Assumes constant $b$, ignoring velocity-dependent friction.
- **Periodic Forcing**: Limits chaotic modeling to specific conditions.

#### Suggestions for Improvement

- **Nonlinear Damping**: Use $b \left| \frac{d \theta}{dt} \right| \frac{d \theta}{dt}$.
- **Non-Periodic Forcing**: Introduce random $F(t)$.
- **Bifurcation Analysis**: Map transitions with varying $F$ or $\omega$.

#### Example Scenarios

1. **Energy Harvester on a Bridge**:
   - A pendulum ($L = 1$ m, $b = 0.1$, $F = 0.2$, $\omega = \omega_0$) oscillates due to wind at resonance, yielding $A \approx 0.64$ rad (~37°). This motion powers a small generator, but chaotic wind gusts could disrupt efficiency.

2. **Suspension Bridge Sway**:
   - Wind drives a bridge segment ($b = 0.2$, $F = 1.5$, $\omega = 1.2$) into chaos. Initial $\theta = 0.1$ rad grows unpredictably, risking structural failure, as seen in phase portraits.

---

### Conclusion

This investigation reveals the forced damped pendulum’s rich dynamics, from resonance ($A = \frac{F}{\sqrt{(\omega_0^2 - \omega^2)^2 + (b \omega)^2}}$) to chaos, driven by $b$, $F$, and $\omega$. Simulations and visualizations highlight transitions, connecting theory to applications like energy harvesting and structural engineering. Future extensions could explore nonlinear damping or random forcing for broader realism.
