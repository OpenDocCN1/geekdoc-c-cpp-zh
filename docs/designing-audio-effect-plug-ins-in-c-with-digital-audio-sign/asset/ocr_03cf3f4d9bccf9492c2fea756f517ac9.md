last chapter you manually calculated the input/output relationship of a filter by cranking through the filter operation, one step at a time. In this improved method, you only need to solve the transfer function equation. Start with the block diagram in Figure 5.11.

The transfer function is as follows:

```
$H(\omega) = a_0 + a_1 e^{-j\omega}$ (5.15)
```

![](bbox=[0.3, 0.15, 0.7, 0.28])

# Figure 5.11: First-order feed-forward block diagram.

# Table 5.1: Sine and cosine function evaluations at DC, 1/4 Nyquist, 1/2 Nyquist, 3/4 Nyquist, and Nyquist.

| Frequency \(\omega\) | \(\cos(\omega)\) | \(\sin(\omega)\) |
|---|---|---|
| 0 | 1.0 | 0.0 |
| \(\pi/4\) | 0.707 | 0.707 |
| \(\pi/2\) | 0.0 | 1.0 |
| \(3\pi/4\) | 0.707 | -0.707 |
| \(\pi\) | -1.0 | 0.0 |

Use the filter coefficients \(a_0 = 0.5, a_1 = 0.5\). You can use Table 5.1 to help with the evaluation. Evaluate at the following frequencies:

+   * DC: 0
+   * Nyquist: \(\pi\)
+   * 1/2 Nyquist: \(\pi/2\)
+   * 1/4 Nyquist: \(\pi/4\)

Evaluation is a two-step process for each frequency:

+   1. Use Euler's equation to convert the \(e\) terms into real and imaginary components.
+   2. Find the magnitude and argument of the complex equation.

# 5.5.1 DC (0 Hz)