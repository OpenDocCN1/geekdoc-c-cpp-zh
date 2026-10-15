![](bbox=[0.35, 0.08, 0.65, 0.36])

Figure 11.7: Sum of squares of deviations from the desired states as a function of the number of passes, using piecewise linear control with P = 30 time stages of equal length

The corresponding state trajectories are shown in Figure 11.9 where a very rapid change in the state variable x₁ is noted near the final time.

# Example 5: Two-stage CSTR system

Let us now consider the two-stage CSTR system we used in Section 10.4, but changing it very slightly with respect to the performance index. Instead of choosing the performance index as the sum of squares of the state variables at the final time, we introduce another variable x₅ to reflect the sum of squares of deviations from the desired state and the control effort, and impose the final state constraints at the final time t_f = 0.325. The system is described by

```
dx₁/dt = -3x₁ + g₁(x)  (11.80)

dx₂/dt = -11.1558x₂ + g₁(x) - 8.1558(x₂ + 0.1592)u₁  (11.81)

dx₃/dt = 1.5(0.5x₁ - x₃) + g₂(x)  (11.82)

dx₄/dt = 0.75x₂ - 4.9385x₄ + g₂(x) - 3.4385(x₄ + 0.122)u₂  (11.83)

dx₅/dt = x₁² + x₂² + x₃² + x₄² + 0.1(u₁² + u₂²)  (11.84)
```