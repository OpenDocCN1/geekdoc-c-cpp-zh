![](bbox=[0.283, 0.083, 0.483, 0.158])

# Figure 2.24 A Parallel Plate Capacitor

The capacitor may be a conventional capacitor, the device formed by the power and ground planes on a printed circuit board, the device formed by two parallel circuit board traces, parallel wires, adjacent pins on an integrated circuit package, P and N material inside of an integrated circuit, or any number of other devices in our circuit. The capacitance of the device is given by the standard formula from physics, Eq. (2.17).

```
C = \frac{\epsilon A}{d} (2.17)
```

+   where
+   C Capacitance
+   A Cross-sectional area of the capacitor
+   \(\epsilon\) The permittivity of the dielectric material between the plates
+   d The separation of the plates

As with the resistor, the key point to understand from the formula is that as d increases or decreases, C decreases or increases and as A increases or decreases, C increases or decreases.

In a printed circuit, two signal traces can form the two plates of a capacitor. That capacitor appears as a parasitic device between the two signal traces we see in Figure 2.25. As we continue to reduce the size of a design, those traces are moved closer and closer together; the distance between the plates decreases, thereby increasing the associated capacitance. The capacitor appears as a parasitic device in Figure 2.26.

![](bbox=[0.283, 0.58, 0.45, 0.64])

# Figure 2.25 Parallel PCB Traces

![](bbox=[0.283, 0.65, 0.45, 0.71])

# Figure 2.26 A Parallel Plate Capacitor from Two Signal Traces

**noise ground bounce** Because the voltage across a capacitor cannot change instantaneously, a portion of the signal originating at the logic gate on the left will be coupled into the lower trace (ground) as noise or what is called ground bounce. Routing any signal trace through a microprocessor, gate array, or programmable logic devices is going to produce the same effect to varying degrees.

We find a similar parasitic devices between parallel planes such as power and ground, where we want the capacitance or coupling between human bodies, and the circuit, where we don't. As a result, we have conflicting requirements: make the geometry smaller vs. move components farther apart