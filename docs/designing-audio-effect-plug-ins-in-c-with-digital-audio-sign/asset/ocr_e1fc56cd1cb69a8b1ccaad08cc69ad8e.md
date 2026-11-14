cos(Dω) + j sin(Dω) = 1 + j0
if
Dω = 0, ± 2π/D, ± 4π/D, ± 6π/D, ..., ± Nπ/D
until
N > D - 1
(7.17)
or
poles at ω = ± kπ/D k = 0, 2, 4, 6, ..., D

Equation 7.17 shows that the poles will occur at even multiples of π and DC (0 Hz) when Euler's equation becomes 1+j0; the analysis is nearly identical to the zero case. Consider the case of four samples:

cos(Dω) + j sin(Dω) = 1 + j0
cos(4ω) + j sin(4ω) = 1 + j0
ω = ± kπ/D k = 0, 2, 4, 6, ..., D
(7.18)
ω = 0, ± π/2, ± 4π/4
ω = 0, ± π/2, ± π

Figure 7.18 shows the effect of 100% feedback – the response is technically infinite at the pole frequencies. It produces a comb filter (with the teeth of the comb pointing up) rather than the inverse comb filter you saw when examining the zeros. The amount of feedback will affect the radius of the poles and the zeros, but not the pole or zero frequencies, which are only dependent on the amount of delay. Consider the transfer function with a feedback value of 0.75:

![](bbox=[0.14, 0.64, 0.86, 0.76])

**Figure 7.18:** The z-plane pole/zero plot and resulting frequency response for **D = 4** samples with **fb = 1.0**. The peaks theoretically go to infinity.

H(z) = \frac{1 + (1-fb)z^{-D}}{1 - fb z^{-D}}
H(z)|_{fb=0.75} = \frac{1 + 0.25z^{-D}}{1 - 0.75z^{-D}}
(7.19)

The poles will have a radius of 0.75, while the zeros will have a radius of 0.25. This will result in