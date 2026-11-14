```
|H(\omega)| = \sqrt{a^2 + b^2}
= \sqrt{0.19^2 + 1.27^2}
= 1.28
\text{Arg}(H) = \tan^{-1}(b/a)
= \tan^{-1}(1.27/0.19)
= 82^\circ
```

The exact magnitude is 1.28, which is pretty close to our estimated value of 1.26 using the z-plane graphical method.

# 5.17.4 ¼ Nyquist (π/4)

```
H(\omega) = 1 - 1.27[\cos(\omega) - j\sin(\omega)] + 0.81[\cos(2\omega) - j\sin(2\omega)]
= 1 - 1.27[\cos(\pi/4) - j\sin(\pi/4)] + 0.81[\cos(2\pi/4) - j\sin(2\pi/4)]
= 1 - 1.27[\cos(\pi/4) - j\sin(\pi/4)] + 0.81[\cos(\pi/2) - j\sin(\pi/2)]
= 1 - 1.27[0.707 - j0.707] + 0.81[-j1]
= 0.11 + j0.08
```

```
|H(\omega)| = \sqrt{a^2 + b^2}
= \sqrt{0.11^2 + 0.08^2}
= 0.136
\text{Arg}(H) = \tan^{-1}(b/a)
= \tan^{-1}(0.08/0.11)
= 36^\circ
```

The exact magnitude is 0.136, which is pretty close to our estimated value of 0.14 using the z-plane graphical method.

# Step 6: z transform of impulse response

This second-order feed-forward filter is actually pretty easy to examine for its impulse response. For an impulse stimulus, the impulse response h(n) is h(n) = {1.0, -1.27, 0.81}. Taking the z transform of the impulse response is easy, as shown in Equation 5.69:

```
H(z) = \sum_{n=-\infty}^{+\infty} h(n)z^{-n}
= 1.0z^0 - 1.27z^{-1} + 0.81z^{-2}
= 1 - 1.27z^{-1} + 0.81z^{-2}
```

This is exactly what we expect. This should help you understand two more very important details about pure feed-forward filters.