# Table 8.1 Comparison of ODE solvers for different equations.

| Eq. No. | Method | Initial h | No. of flops | Time (ms) | Relative error |
|---|---|---|---|---|---|
| (8.41) | rk4 | 0.01 | 1000 | 5.2 | 2.2 × 10⁻⁸ |
|  | rk45 | 1.00 | 72 | 1.5 | 1.8 × 10⁻⁸ |
| (8.42) | rk4 | 0.01 | 227 | 8.9 | 1.8 × 10⁻⁸ |
|  | rk45 | 0.1 | 3143 | 36.7 | 5.7 × 10⁻¹¹ |

# 8.8
Solution for Nonlinear Oscillations (Assessment)

Use your rk4 program to study anharmonic oscillations by trying powers in the range p = 2–12, or anharmonic strengths in the range 0 ≤ αx ≤ 2. Do not include any explicit time-dependent forces yet. Note that for large values of p, the forces and accelerations get large near the turning points, and so you may need a smaller step size h than that used for the harmonic oscillator.

+   1. Check that the solution remains periodic with constant amplitude and period for a given initial condition regardless of how nonlinear you make the force. In particular, check that the maximum speed occurs at x = 0 and that the velocity v = 0 at maximum x’s, the latter being a consequence of energy conservation.
+   2. Verify that nonharmonic oscillators are nonisochronous, that is, vibrations with different amplitudes have different periods (Figure 8.7).
+   3. Explain why the shapes of the oscillations change for different p’s or α’s.
+   4. Devise an algorithm to determine the period T of the oscillation by recording times at which the mass passes through the origin. Note that because the mo-

![](bbox=[0.15, 0.66, 0.5, 0.83])

Figure 8.7 The position vs. time for oscillations within the potential V ∝ x⁷ for four different initial amplitudes. Each is seen to have a different period.