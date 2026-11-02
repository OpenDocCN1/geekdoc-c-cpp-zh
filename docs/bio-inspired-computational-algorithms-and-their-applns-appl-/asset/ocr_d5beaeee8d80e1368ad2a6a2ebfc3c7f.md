genetic parameters. In this work, adaptive mutation has been used to deal with the problem of premature convergence in BGA. The effectiveness of the proposed approach was demonstrated by the time and frequency domain simulation results. Eigenvalue analysis shows that the BGA based controller provides a better damping to the system for all operating conditions considered than a GA based controller. The conventional controller provides the least damping to all the operating conditions considered. The robustness of the BGA controller under large disturbance was also investigated by applying a three-phase fault to the system. Further research will be carried out in the direction of using multi-objective functions in the optimization and using a more complex power system model.

# ## 8. Appendix

# ### 8.1 Generator and Automatic Voltage Regulator (AVR) equations

# #### 8.1.1 Swing equations

$$\frac{d}{dt}\Delta\omega = \frac{1}{2H}(T_m - T_e - K_D\Delta\omega)$$

$$\frac{d}{dt}\Delta\delta = \omega_0\Delta\omega$$

where

+   - $\delta$ is the rotor angle in rad
+   - $\omega$ is the synchronous speed in per-unit (p.u.)
+   - $\omega_0$ is the synchronous speed in rad/sec
+   - $H$ is the inertia constant in sec.
+   - $T_m$ is the mechanical torque in p.u.
+   - $T_e$ is the electrical torque in p.u.
+   - $K_D$ is the damping coefficient in torque/ p.u.

# #### 8.1.2 Rotor circuit equations

$$\frac{d}{dt}\psi_{fd} = \omega_0\left(E_{fd} - \frac{R_{fd}}{L_{fd}}i_{fd}\right)$$

$$\frac{d}{dt}\psi_{1d} = -\omega_0 R_{1d}i_{1d}$$

$$\frac{d}{dt}\psi_{1q} = -\omega_0 R_{1q}i_{1q}$$

$$\frac{d}{dt}\psi_{2q} = -\omega_0 R_{2q}i_{2q}$$