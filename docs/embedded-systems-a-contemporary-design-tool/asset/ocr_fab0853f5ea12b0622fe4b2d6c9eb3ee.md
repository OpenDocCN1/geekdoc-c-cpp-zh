# 21.4.5.1 End Terminated – Biased Termination

Let's examine a technique by which we can operationally disconnect the termination resistor when transmission ceases. Our terminated transmission line is given in Figure 21.29. The biased scheme brings in a capacitor, here designated as C0, at DC, the capacitor appears as an open circuit; the resistor is disconnected from ground.

![](bbox=[0.26, 0.19, 0.46, 0.25])

Figure 21.29 Biased Termination

# Biased Termination

With a biased termination, the goal is to ensure that the termination spends approximately half the time in each state (0 or 1) and to ensure that we have no DC power dissipation.

In such an ideal case, during transmission, the voltage across the capacitor approaches that in Eq. (21.46).

```
V_C = \frac{V_{OH} - V_{OL}}{2} = \frac{\Delta V}{2} (21.46)
```

From which we get the average power dissipation in Eq. (21.47).

```
P_{RC} = \frac{\left( \frac{\Delta V}{2} \right)^2}{Z_0} = \frac{(\Delta V)^2}{4Z_0} (21.47)
```

![](bbox=[0.26, 0.49, 0.6, 0.57])

Figure 21.30 Computing the Signaling Rise and Fall Times

Using the model in Figure 21.30, the time constant, τ, for the rise and fall times for the signals are given in Eq. (21.48).

```
τ = 2Z_0C (21.48)
```

Note that C is going to be the parallel combination of C0 and the parasitic capacitors.

# 21.4.5.2 End Terminated – Split Termination

# Split Termination

The split termination scheme separates the terminating impedance into two pieces. A common implementation for the split termination scheme is given in Figure 21.31.

![](bbox=[0.26, 0.79, 0.5, 0.88])

Figure 21.31 Split Termination