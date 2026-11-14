The resistance of each of the components follows:

```
|Z_R(w)| = R   w = 0 -> no frequency dependent component   (2.6)
|Z_L| = wL   w = 0 -> short   (2.7)
|Z_C(w)| = 1/wC   w = 0 -> open   (2.8)
```

# At AC – we speak of impedance

+   R is a resistor - it has no frequency-dependent component
+   L has finite nonzero impedance
+   C has finite nonzero impedance

The impedance of each of the components follows:

```
|Z_R(w)| = R   no frequency dependent component   (2.9)
|Z_L(w)| = wL   finite nonzero impedance - w increase -> open   (2.10)
|Z_C(w)| = 1/wC   finite nonzero impedance - w increase -> short   (2.11)
```

Observe that if the frequency is increased, the impedance of the inductor will increase and that of the capacitor will decrease. As the frequency is increased further, the capacitor will eventually form a low-impedance path across the resistor, and the impedance of the inductor will then dominate that of the resistor. What had been a wire or resistor at low frequencies has suddenly become a frequency-dependent impedance.

The problem is actually more complex. If we write the transfer function looking into the network as a Laplace transform:

```
Z(s) = Ls + R || 1/Cs
     = (Ls + R / RCs + 1)   (2.12)
```

Evaluating the expression for s = jω and solving for the impedance and phase angle of the transfer function, we have:

Let s -> jω

```
|Z(w)| = sqrt( R^2(1 - LCw^2)^2 + (Lw)^2 / 1 + (RCw)^2 )   (2.13)
```

Checking the boundaries for the impedance, for

```
w = 0
|Z(w)| = R   (2.14)
w -> ∞
|Z(w)| = L   (2.15)
```

These values are consistent with those that we estimated earlier. Because of the inductive and capacitive elements, we also get a phase shift through the path indicated by