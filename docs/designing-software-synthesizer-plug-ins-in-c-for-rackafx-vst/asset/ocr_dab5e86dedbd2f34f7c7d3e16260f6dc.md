To form the transfer function H(z), take the z-Transform of Equation 4.5 by inspection:

```
y(n) = x(n - M)
apply z-Transform
y(n) \rightarrow Y(z)
x(n - M) \rightarrow X(z)z^{-M}
so
Y(z) = X(z)z^{-M}
H(z) = \frac{Y(z)}{X(z)} = z^{-M}  (4.7)
```

# 4.4 Digital Differentiation

We will see few oscillators with digital differentiators in them. The differentiator takes the time derivative of the signal. Since the derivative represents the rate of change, the differentiator's output is the current (or instantaneous) slope of the signal. This is easy to find the slope mi is:

```
\frac{\Delta y}{\Delta x}  (4.8)
```

For our digitized signal, the change in x is constant between points, so the digital differentiator will be providing:

```
\frac{\Delta y}{sample}  (4.9)
```

Since the change in y is the difference between the current and last input values, we can fashion the differentiator easily as shown in

Figure 4.5.

![](bbox=[0.196, 0.676, 0.803, 0.786])

Figure 4.5: A simple digital differentiator outputs the slope between the current and last inputs.

# 4.5 Analog and Digital Integration

Analog integrators integrate over continuous time; they calculate the area under the signal's curve. The traditional analog integrator circuit consists of an op-amp with a capacitor in the feedback path (if you don't know what that means, don't worry—worry that you're not analyzing it). You can think of the charge on a capacitor as the integrating component. The transfer function of an analog integrator shown in the block diagram in Figure 4.6 is found by applying