# 20.3.3 Board Level Bypass

Let's look at the problem in the circuit in Figure 20.5. Assume that we are switching the output of the gate from a logic 0 to a logic 1, which must charge the parasitic capacitor C1. Further assume that our signal has a rise time of 5 ns and that C1 is 50 pF, which is typical for 5–7 unit loads.

![](bbox=[0.28, 0.195, 0.58, 0.33])

**Figure 20.5** Simple Switching Circuit.

We compute the maximum di/dt starting with Eq. (20.4), then add a little calculus.

```
i = C (dv/dt)
(20.4)
```

We get Eq. (20.5). A typical TTL signal gives a dV = 4.5 V when switching from logic 0 to logic 1. The state change gives us the charging current in Eq. (20.5).

```
max di/dt = 1.52 dV / (trise)^2 C = 1.5 x 10^7 (amps/(second))
(20.5)
```

Assume we have two parallel power distribution paths: power conductor and a ground plane, as illustrated in Figure 20.6.

![](bbox=[0.28, 0.58, 0.44, 0.63])

**Figure 20.6** Power and Ground Distribution.

Specific formulas for such an inductance can become complex and can be dependent upon the specific environment and circuit geometry. A generally accepted version for a wire over a ground plane is given in Eq. (20.6).

```
L_psw = (10.16 • X) • (ln (2H / D)) = 186 nH
(20.6)
```

+   - L – Inductance in nH.
+   - X – Length of wire Assume 10 in.
+   - H – Height above ground Assume 0.1 in.
+   - D – Diameter of wire Assume 20 AWG – 0.032 in.

We now compute peak switching noise voltage from Eq. (20.5). Below certain frequencies, we will see that the impedance of PSW is sufficiently low that we don’t need to do anything.