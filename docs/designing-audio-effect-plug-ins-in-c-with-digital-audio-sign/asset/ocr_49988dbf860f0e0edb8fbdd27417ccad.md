![](bbox=[0.25, 0.01, 0.75, 0.24])

# Figure 6.8: Block diagram for the Smith-Angell improved resonator.

Specify:

+   * \( f_c \), center frequency
+   * \( BW \), 3 dB bandwidth; or \( Q \), quality factor

The design equations are as follows:

```
\theta_c = 2\pi f_c f_s
BW = f_c/Q
b_2 = e^{(-2\pi \frac{BW}{f_s})}
b_1 = \frac{-4b_2}{1+b_2} \cos(\theta_c)
a_0 = 1 - \sqrt{b_2}
a_2 = -a_0
(6.8)
```

This design is also gain normalized with \( a_0 \) and as before, the radius is set with \( b_2 \) first, then \( b_1 \) is calculated using the \( b_2 \) coefficient and the desired pole frequency. The filter is not truly normalized to 0.0 dB; there is actually a slight fluctuation of less than 1 dB.

The improved resonator is also named the Smith-Angell resonator, after its inventors. They improved the design by dropping two zeros into the filter, one at \( z=1 \) and one at \( z=-1 \) in order to pin down DC and Nyquist with a response of zero. This forces the filter to become somewhat more symmetric (but not entirely) and has the advantage of making the band pass even more selective in nature (Figure 6.9).

![](bbox=[0.1, 0.83, 0.9, 0.98])