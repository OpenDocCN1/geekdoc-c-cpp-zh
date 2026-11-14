lumps the package, bus, outside world, and ground plane parasitic devices, which all add in parallel.

Once again, we use a simple voltage divider in equation Eq. (2.38) to compute Vout for a step input.

```
V_{out}(s) = \left( \frac{\frac{1}{Cs}}{R + Ls + \frac{1}{Cs}} \right) V_{in}(s)

V_{out}(s) = \left( \frac{1}{s^2 + \frac{R}{L}s + \frac{1}{LC}} \right)
```

The expression in the denominator on right-hand side can be written as the classic second-order characteristic equation as in equation Eq. (2.39). Thus,

```
V_{out}(s) = \frac{V_{in}(s)}{LC} \left( \frac{1}{s^2 + 2\xi\omega_n s + (\omega_n)^2} \right)

\omega_n = \frac{1}{\sqrt{LC}}

\xi = \frac{R}{2} \left( \frac{C}{L} \right)^{0.5}
```

The value of the damping factor \(\xi\) determines if circuit is

+   - Underdamped \(\xi < 1\)
+   - Critically damped \(\xi = 1\)
+   - Overdamped \(\xi > 1\)

For a digital system, we want neither underdamped (possible oscillation and noise) or overdamped (possible metastability) behavior. Critical damping permits the signal to reach full magnitude following a state change, the fastest of the alternatives with minimal overshoot.

# **quality factor** Q

The variable Q, or quality factor, is a parameter that describes the damping characteristics of an oscillator or resonator. It is a measure of a circuit's ability to support oscillation. Good oscillators have high Q and vice versa. For this circuit, the Q is given as:

```
Q = \frac{(\frac{L}{C})^{1/2}}{R} = \frac{\omega_n L}{R} = \frac{1}{2\xi}
```

If Vin is a 5.0 V step input and we solve for Vout(t) in the time domain, the inverse Laplace transform gives us the circuit output in Eq. (2.41).

```
V(t) = 5 - \left( 5 \exp \left( \frac{-\alpha t}{2Q} \right) \frac{\sin \left( \frac{1}{2} \omega \frac{\sqrt{4Q^2 - 1}}{Q} t \right)}{\sqrt{4Q^2 - 1}} \right) - \left( 5 \exp \left( \frac{-\alpha t}{2Q} \right) \cos \left( \frac{1}{2} \omega \frac{\sqrt{4Q^2 - 1}}{Q} t \right) \right)
```