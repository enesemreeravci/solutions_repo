## Problem 1

**Investigating the Range as a Function of the Angle of Projection**

---

### 1. Theoretical Foundation

#### Deriving the Equations of Motion

Projectile motion can be analyzed by breaking it into horizontal and vertical components. Assuming no air resistance, the only acceleration is due to gravity, acting downward. This assumption simplifies the equations, making it easier to analyze motion using basic kinematic principles.

##### Horizontal Motion:

- The horizontal component of velocity remains constant since there is no horizontal acceleration.
- The displacement in the horizontal direction is given by:

  x = v0 \* cos(theta) \* t

This equation shows that the horizontal motion is uniform and independent of gravity.

##### Vertical Motion:

- The vertical component of velocity changes due to gravitational acceleration.
- The displacement in the vertical direction is given by:

  y = v0 \* sin(theta) \* t - 0.5 \* g \* t\*\*2

The vertical component influences the total time of flight and peak height of the projectile.

##### Time of Flight

The projectile reaches the ground when y = 0. Solving for time:

```
t = 0 and t = (2 * v0 * sin(theta)) / g
```

The first solution represents the initial launch time. The second solution gives the total flight duration.

##### Range

Substituting the time of flight into the horizontal motion equation:

```
R = (v0**2 * sin(2 * theta)) / g
```

This equation shows that the range depends on the initial velocity and the launch angle. The function sin(2 \* theta) explains why the range is symmetric around 45 degrees.

#### Family of Solutions

From the range formula R = (v0\*\*2 \* sin(2 \* theta)) / g, we derive a family of solutions for different values of theta and v0. Notably:

- For every angle θ, there exists a complementary angle (90 - θ) that yields the same range.
- As v0 increases, the maximum achievable range increases quadratically.
- The trajectory and time of flight can be visualized as parametric functions of angle and initial velocity.

---

### 2. Practical Applications

#### Real-World Scenarios

Projectile motion applies to various real-world cases, including:

- **Sports**:
  - Soccer players use precise angles to shoot the ball past defenders.
  - Basketball shots require players to estimate the ideal arc for successful scoring.
- **Engineering**:
  - Projectile calculations are critical in artillery and missile guidance systems.
- **Space Exploration & Astrophysics**:
  - Scientists compute trajectories to optimize spacecraft landings.
  - The motion of celestial bodies and meteor impacts follow similar equations.

#### Adaptations

- **Uneven Terrain**: Adjust the initial height h to reflect varying ground levels.
- **Air Resistance**: Consider drag force, which modifies trajectory curves and reduces range.
- **Wind Effects**: Incorporate horizontal forces, affecting projectiles over long distances.

---

### 3. Implementation

#### Graphical Outputs

**Figure 1: Range as a Function of Angle of Projection (v₀ = 50 m/s)**  
![Range vs Angle - Basic](graph.png)

**Figure 2: Range vs Angle for Different Initial Velocities**  
![Multiple Velocities](graph2.png)

**Figure 3: Chaotic Range with Environmental Noise**  
![Chaotic Graph](graph3.png)



#### Python Simulation

```python
import numpy as np
import matplotlib.pyplot as plt

g = 9.81  # gravitational acceleration (m/s²)

def calculate_range(v0, theta):
    theta_rad = np.radians(theta)
    return (v0**2 * np.sin(2 * theta_rad)) / g

angles = np.linspace(0, 90, 100)
v0_values = [20, 35, 50, 65, 80]

plt.figure(figsize=(10, 6))
for v0 in v0_values:
    ranges = [calculate_range(v0, angle) for angle in angles]
    plt.plot(angles, ranges, label=f'v₀ = {v0} m/s')

plt.axvline(x=45, linestyle='--', color='black', label='Max Range at 45°')
plt.xlabel('Angle of Projection (degrees)')
plt.ylabel('Range (m)')
plt.title('Range vs Angle for Various Initial Velocities')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()
```
 in Python to generate the graphs shown above. Code available upon request.*

#### Graphical Interpretation

- **Figure 1** shows how the projectile's range changes with launch angle when the initial velocity is fixed at 50 m/s. The curve peaks at 45°, demonstrating the ideal angle for maximum distance.
- **Figure 2** compares several different initial velocities. While all curves peak at 45°, higher velocities yield longer ranges.
- **Figure 3** introduces randomness (e.g., wind/turbulence). It shows how real-world factors can cause unpredictable variations in range, even at the same angles. , showing that:
  - All curves peak at **45 degrees**, confirming it gives the maximum range.
  - Higher velocities produce **longer ranges**.
  - The symmetry of each curve is preserved.

---

### 4. Limitations and Extensions

#### Limitations

- **Idealized Model**:
  - Assumes a vacuum (no air resistance).
  - Ignores spin effects and real-world complexities.
- **External Factors**:
  - Wind, altitude changes, and rotational effects can alter expected trajectories.

#### Suggestions for Improvement

- **Incorporate Drag**: Model air resistance using differential equations that factor in object size and shape.
- **Variable Gravity**: Reflect gravitational changes on different planets or with altitude.
- **Wind Effects**: Introduce lateral forces and variable resistance based on wind velocity.
- **Interactive Simulations**: Build user-friendly interfaces that accept dynamic inputs (velocity, angle, gravity, drag).

---

### Conclusion

This investigation provides a comprehensive understanding of how projectile range depends on the angle of projection and other initial conditions. By developing a computational tool and visualizing results, we enhance both theoretical knowledge and practical application. Future extensions could include incorporating real-world effects such as wind and air resistance to refine predictions and develop more accurate and interactive educational models.

