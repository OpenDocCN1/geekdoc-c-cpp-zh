![](bbox=[0.2, 0.1, 0.48, 0.3])

![](bbox=[0.53, 0.1, 0.81, 0.3])

![](bbox=[0.35, 0.35, 0.65, 0.55])

Fig. 6.40. Typical behaviour of the LORENZ-84 system, the three screen shots show x vs. y, z vs. z, and y vs. z

The mathematical description of this particular oscillator is based on three coupled differential equations of the form

```
\dot{x} = c_1 (y - x - f(x)),    (6.36)
\dot{y} = c_2 (x - y + z), and    (6.37)
\dot{z} = -c_3 y                 (6.38)
```

where f(x) describes the behaviour of the CHUA-diode and is defined as

```
f(x) = m_1 x + (m_0 - m_1)/2 (|x + 1| - |x - 1|).    (6.39)
```

The standard values for the parameters are

+   - c₁ = 15.6,
+   - c₂ = 1,
+   - c₃ = 28,
+   - m₀ = −1.143, and
+   - m₁ = −0.714.