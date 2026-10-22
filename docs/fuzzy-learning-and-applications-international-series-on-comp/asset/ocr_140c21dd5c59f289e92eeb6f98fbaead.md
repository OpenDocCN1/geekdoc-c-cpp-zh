![](bbox=[0.18, 0.09, 0.82, 0.48])

# Figure 9.7 The focus error nonlinearity

the system to the correct focus position starting from a given initial condition;

+   - a first-level closed loop controller which, after the start-up phase, keeps the system in the desired position;
+   - a second-level controller which takes large deviations from the correct position into account.

The start-up controller and the second-level controller only act during particular conditions and were implemented using traditional controllers. The most important part is the first-level closed-loop controller, which is active during most of the operating phases.

The following is a description of the design of the closed-loop first-level controller. At first a classical control system was built in the frequency domain in order to meet the following requirements:

+   - step error ≤ 1μm
+   - phase margin φ ≥ 60°
+   - rise time t_r ≥ 0.01s

The designed controller is:

```
C(s) = 1.5(1 + 0.0044s) / (1 + 0.000317s)    (9.2)
```