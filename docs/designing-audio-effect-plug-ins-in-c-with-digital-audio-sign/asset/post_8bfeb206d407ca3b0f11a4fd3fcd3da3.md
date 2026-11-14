
![](img/b54974d0a4317ec82d7ae02126d10a6f_148_0.png)

Figure 5.44: The poles of the filter.

\(\cos(\theta) = \frac{1.34}{2(0.95)}\)
\(\theta = \arccos(0.707)\)
\(\theta = 45^\circ\)

Figure 5.44 shows the complex conjugate pair of poles plotted in the z-plane at angles \(\pm 45^\circ\) and radii of 0.95. Evaluating the frequency response of the complex pair is similar to before, but with an extra step. When estimating the frequency response with more than one pole:

- Locate each evaluation frequency on the outer rim of the unit circle.
- Draw a line from the point on the circle to *each pole* and measure the length of these vectors. Do it for each evaluation frequency.
- For each evaluation frequency, the magnitude of the transfer function is the *product of the inverse lengths* of the two vectors to each pole pair.

Mathematically, this last rule looks like Equation 5.74:

\(|H(e^{j\omega})|_\omega = a_0 \frac{1}{\prod_{i=1}^N V_i}\) (5.74)

where

- \(N = \text{the filter order}\)
- \(V_i = \text{the geometric length from the point}(\omega) \text{ on the unit circle to the } i\text{th pole}\)

Thus, the process is the same as with the zeros, except that you take the inverse of the length to the pole.

For feed-forward filters:

- The closer the frequency is to the zero, the more attenuation it receives.
- If the zero is *on* the unit circle, the magnitude would go to zero at that point.

### For feed-back filters:

- The closer the evaluation frequency is to the pole, the more gain it receives.
- If a pole is *on* the unit circle, the magnitude would theoretically go to infinity, and it would produce an oscillator, ringing forever at the pole frequency.

You blew up the first-order feed-back filter as an exercise in Chapter 4. All feedback filters are prone to blowing up when their poles go outside the unit circle. We can now continue with the estimation process for our standard four evaluation frequencies. This time, we'll convert the raw magnitude values into dB. The reason for doing this is that there will be a very wide range of values that will be difficult to sketch if we don't use dB. Follow the evaluation sequence in Figures 5.45 through 5.48. Finally, you can put it all together to form the frequency response plot in Figure 5.49.

- In a digital filter:
  - Zeros may be located anywhere in the z-plane, inside, on, or outside the unit circle since the filter is always stable; its output can't go lower than 0.0.
  - Poles must be located inside the unit circle.
  - If a pole is on the unit circle, it produces an oscillator.
  - If a pole is outside the unit circle, the filter blows up as the output goes to infinity.

![](img/b54974d0a4317ec82d7ae02126d10a6f_149_0.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_149_1.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_150_0.png)

Figure 5.47: The magnitude response at \(\pi/2\) is –2.98 dB.

![](img/b54974d0a4317ec82d7ae02126d10a6f_150_1.png)

Figure 5.48: The magnitude response at Nyquist is –10.1 dB.

![](img/b54974d0a4317ec82d7ae02126d10a6f_150_2.png)

Figure 5.49: The composite magnitude response of the filter shows that it is a resonant low-pass filter; the resonant peak occurs at the pole frequency.

## Step 5: Direct evaluation

Now you can evaluate the filter the same way as before using Euler's equation to separate the real and imaginary components from the transfer function. Evaluate at the following frequencies:

- DC: 0
- Nyquist: \(\pi\)
- 1/2 Nyquist: \(\pi/2\)
- 1/4 Nyquist: \(\pi/4\)

First, get the transfer function in a form to use for all the evaluation frequencies:

H(z) = a_0 \frac{1}{1 + b_1 z^{-1} + b_2 z^{-2}}
= \frac{1}{1 - 1.34z^{-1} + 0.902z^{-2}}
Let z = e^{j\omega}.
H(\omega) = \frac{1}{1 - 1.34e^{-j\omega} + 0.902e^{-j2\omega}}

Apply Euler's equation:

H(\omega) = \frac{1}{1 - 1.34e^{-j\omega} + 0.902e^{-j2\omega}}
H(\omega) = \frac{1}{1 - 1.34[\cos(\omega) - j\sin(\omega)] + 0.902[\cos(2\omega) - j\sin(2\omega)]}

Now evaluate for each of our four frequencies starting with DC.

### 5.18.1 DC (0 Hz)

H(\omega) = \frac{1}{1 - 1.34[\cos(\omega) - j\sin(\omega)] + 0.902[\cos(2\omega) - j\sin(2\omega)]}
= \frac{1}{1 - 1.34[\cos(0) - j\sin(0)] + 0.902[\cos(2*0) - j\sin(2*0)]}
= \frac{1}{1 - 1.34[1 - j0] + 0.902} (5.76)
= \frac{1}{1 - 1.34 + 0.902}
= \frac{1}{0.562 + j0}

H(\omega) = \frac{1}{0.562 + j0}
|H(\omega)| = \frac{|1|}{|0.562 + j0|}
= \frac{1}{\sqrt{a^2 + b^2}} (5.77)
= \frac{1}{\sqrt{0.562^2}} = 1.78 = 5.00 \text{ dB}
\text{Arg}(H) = \text{Arg(Num)} - \text{Arg(Denom)}
= \tan^{-1}(0/1) - \tan^{-1}(0/0.562)
= 0^\circ

Remember that for magnitudes of fractions, you need to take the magnitude of the numerator and denominator separately; also for phase, the total is the difference of the Arg(num) and Arg(denom). The direct evaluation yields 5.0 dB and shows our sketch evaluation was a little off at 5.9 dB.

Table 5.4: Challenge answers.

| Frequency (ω) | \|H(ω)\| | Arg(H) |
|---|---|---|
| Nyquist (π) | −10.2 dB | 0.0° |
| ½ Nyquist (π/2) | −2.56 dB | −85.8° |
| ¼ Nyquist (π/4) | +123.15 dB | −40.3° |

![](img/b54974d0a4317ec82d7ae02126d10a6f_152_0.png)

### 5.18.2 Challenge

Finish the rest of the direct evaluation calculations on your own. The answers are in Table 5.4. The exact evaluation once again produces results pretty close to our estimated version. You can get the complete answers at the RackAFX websites.

## Step 6: z transform of impulse response

The impulse response for this filter is shown in Figure 5.50. Once again, finding the impulse response by hand is going to be tedious. Instead, I will use RackAFX to do the analysis so we can compare our estimated and direct evaluation results. The measured responses are shown in Figure 5.51.

## 5.19 First-Order Pole-Zero Filter: The Shelving Filter

The first-order pole-zero filter consists of a first-order pole and first-order zero in the same algorithm. The topology in the block diagram in Figure 5.52 is a combination feed forward and feed back since it contains both paths.

The difference equation is as follows:

```
y(n) = a₀x(n) + a₁x(n − 1) − b₁y(n − 1) ...... (5.78)
```

### Steps 1 to 3: Take the z transform of the difference equation to get the transfer function, then factor out a₀ as the scalar gain coefficient

```
Y(z) = a₀X(z) + a₁X(z)z⁻¹ − b₁Y(z)z⁻¹ ...... (5.79)
```

Separate variables:

Y(z) + b_1Y(z)z^{-1} = a_0X(z) + a_1X(z)z^{-1}
Y(z)[1 + b_1z^{-1}] = X(z)[a_0 + a_1z^{-1}]

Form the transfer function:

H(z) = \frac{Y(z)}{X(z)} = \frac{a_0 + a_1z^{-1}}{1 + b_1z^{-1}}

Factor out $a_0$:

H(z) = a_0 \frac{1 + \alpha_1z^{-1}}{1 + b_1z^{-1}}

where

\alpha_1 = \frac{a_1}{a_0}

![](img/b54974d0a4317ec82d7ae02126d10a6f_153_0.png)

Figure 5.51: RackAFX's frequency and phase responses are taken from the z-transform of the impulse response.

![](img/b54974d0a4317ec82d7ae02126d10a6f_153_1.png)

Figure 5.52: First-order pole-zero filter.

### Step 4: Estimate the frequency response

This transfer function has one pole and one zero and both are first order. Like the other first-order cases, we can find the pole and zero by inspection of the transfer function:

```
H(z) = a_0 \frac{1 + \alpha_1 z^{-1}}{1 + b_1 z^{-1}}
\tag{5.80}
= a_0 \frac{1 + \frac{\alpha_1}{z}}{1 + \frac{b_1}{z}}
```

In the numerator, you can see that if \(z = -\alpha_1\) the numerator will go to zero and the transfer function will go to zero. In the denominator, you can see that if \(z = -b_1\) the denominator will go to zero and the transfer function will go to infinity. Therefore we have a zero at \(z = -\alpha_1\) and a pole at \(z = -b_1\). For this example, use the following values for the coefficients: \(a_0 = 1.0, a_1 = -0.92, b_1 = -0.71\). Then, \(\alpha_1 = -0.92\), and so we now have a zero at \(z = -\alpha_1 = 0.92 + j0\) and a pole at \(z = -b_1 = 0.71 + j0\). The pole/zero pair are plotted in Figure 5.53.

Evaluating the frequency response when you have mixed poles and zeros is the same as before, but you have to implement both magnitude steps.

- Locate each evaluation frequency on the outer rim of the unit circle.
- Draw a line from the point on the circle to *each zero* and measure the length of these vectors. Do it for each evaluation frequency.
- Draw a line from the point on the circle to *each pole* and measure the length of these vectors. Do it for each evaluation frequency.

![](img/b54974d0a4317ec82d7ae02126d10a6f_154_0.png)

**Figure 5.53:** The pole and zero are both purely real and plotted on the real axis in the z-plane.

- Multiply all the zero magnitudes together.
- Multiply all the *inverse* pole magnitudes together.
- Divide the zero magnitude by the pole magnitude for the final result at that frequency.

Mathematically, this last rule looks like Equation 5.81:
