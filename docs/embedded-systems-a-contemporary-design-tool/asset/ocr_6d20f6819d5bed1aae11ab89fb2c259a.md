4. Finally, compute the crosstalk signal as the ratio between the induced voltage in B with respect to the change in A.

```
\frac{V_{\text{crosstalk}}}{\Delta V_\text{A}} = \frac{I_\text{M}R_\text{B}}{\Delta V_\text{A}} = \frac{R_\text{B}C_\text{M}}{\tau_\text{rise}} \qquad (20.32) \\
V_{\text{crosstalk}} = (\Delta V_\text{A}) \left( \frac{R_\text{B}C_\text{M}}{\tau_\text{rise}} \right)
```

# 20.4.1.1 Preventing or Reducing Crosstalk

To prevent such coupling, we have several alternatives:

+   • **Guarding.** As shown in Figure 20.11, we route a ground trace so as to cut the path. The Guard trace is grounded at only one end. The capacitance still exists but it cannot couple into circuit B, and no current can flow in the Guard trace. Why?

![](bbox=[0.312, 0.322, 0.5, 0.403])

Figure 20.11 Routing a Guard Trace.

+   • **Twisted Pair.** By twisting the conductors, the net crosstalk from alternating plus and minus coupling cancels.

+   • **Ground Plane or Ground Grid.** Provides a return path directly under a trace to give the lowest inductance and smallest loop area and minimizes the magnetic field interacting with other traces. A ground plane is the preferred solution, but a ground grid provides a good alternative.

# 20.4.2 Loops

Any electronic circuit contains loops; it's the only way they work. Again, from our studies of electromagnetic physics, a changing electromagnetic field passing through a circuit can induce parasitic currents in the circuit. Such fields are everywhere; radio and television stations and electric lights are two sources. They can create problems with high flying aircraft and objects launched into space.

Let's look at simple circuit in Figure 20.12.

![](bbox=[0.281, 0.672, 0.556, 0.856])

Figure 20.12 Mutual Inductance.