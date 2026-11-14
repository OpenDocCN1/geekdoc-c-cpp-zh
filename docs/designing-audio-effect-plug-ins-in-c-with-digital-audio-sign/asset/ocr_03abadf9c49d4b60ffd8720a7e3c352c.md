Poles are calculated as follows:

$b_2 = R_p^2 = 0.88$
$R_p = \sqrt{0.88} = 0.94$

![](bbox=[0.3, 0.12, 0.7, 0.34])

# Figure 5.63: Pole/zero plot for the example bi-quad filter.

and

$b_1 = -2R \cos(\phi) = -0.78$
$2 (0.94) \cos(\phi) = 0.78$
$\cos(\phi) = \frac{0.78}{2(0.94)}$
$\phi = \arccos(0.414)$
$\phi = 65.5^\circ$ (5.90)

The poles and zeros are in close proximity to each other. The zero is directly on the unit circle ($R_z = 1.0$), so we expect a notch to occur there. The pole is near the unit circle but not touching it, so we expect a resonance there.

We are not going to go through the full response estimation or direct evaluation since it's just repetitive algebra at this point. But, we can use RackAFX's bi-quad module to set up the filter and evaluate it (Figure 5.64). The frequency response clearly shows the resonant peaking due to the pole, then the sudden notch due to the nearby zero.

In Figure 5.64, it's easy to locate the places where the pole or zero dominates. In the low frequencies, the pole dominates and at high frequencies the zero dominates. This is an example of a direct z-plane design where we place a pole and zero pair directly in the z-plane, then calculate the coefficients. In the next chapter, we will examine some basic Infinite Impulse Response (IIR) design techniques and the direct z-plane method will be the first.

# Final Review Notes

In this chapter you learned the basics of DSP theory; specifically, you learned the sequence:

+   1. Take the z transform of the difference equation.