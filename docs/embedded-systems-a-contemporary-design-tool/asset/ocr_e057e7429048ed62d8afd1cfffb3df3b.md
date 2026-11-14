# 21.4.4 Unterminated Signal Path

Let's now examine three environmental conditions affecting the signal path and thus the transmitted signal:

+   1. The line is unterminated.
+   2. The line is driven by a low output impedance device.
+   3. The line is driven by a high output impedance device.

We consider a line to be _unterminated_ when neither the source nor the load impedance matches the characteristic impedance of the line. Observe, once again, that even with LSI and VLSI circuits we have many boundaries where we can have impedance mismatches, which can lead to signal reflections.

Let's now analyze an unterminated signal path driven first by a low source impedance device and then by a high source impedance device.

# 21.4.4.1 Low Source Impedance – TTL/ECL Drivers

TTL and ECL devices have a low source impedance _Z<sub>S</sub>_ compared to the path's characteristic impedance _Z<sub>0</sub>_.

```
Z_S \ll Z_0
```

With an unterminated line, we have an infinite load impedance _Z<sub>L</sub>_ compared to the path's characteristic impedance.

```
Z_L = \infty
```

Under typical operation, the signal:

+   - Leaves source.
+   - Travels down the path to the load.
+   - Reflects off load.
+   - Returns back down the path to the source.
+   - Reflects off source with decreasing amplitude.

From Eqs. (21.41) and (21.42), we get Eq. (21.43):

```
V_2^- = \left( \frac{-Z_0}{+Z_0} \right) \left( \frac{Z_L}{Z_L} \right) V_1^+ \rightarrow -1
(21.43)
```

which gives a reflection coefficient \(\Gamma\) approaching -1. With a reflection coefficient of -1, we have the following behavior:

+   - Successive reflections are of opposite signs and, typically, of decreased amplitude, as shown in Figure 21.24.
+   - Two round trips (4 traversals) are required before successive signals have the same polarity.

After a single round trip, \(V_2^- = -V_1^+\) as illustrated in Figure 21.24. If the rise time of the signal is shorter than the round trip delay, \(\tau_{line} > \tau_{rise}\), we have a distributed rather than lumped model and overshoot will be evident in the output signal.