fall times of the signals flowing through and only indirectly on the frequency of the signals. The rule of thumb or heuristic for PCB traces using point-to-point wiring versus transmission lines is that wiring shorter than 1/6 of the effective length behaves mostly in a lumped fashion.

# 21.3.3 Point-to-Point Wiring

We will now examine point-to-point wiring and identify some of the potential shortcomings. Consider today's evolving systems that are increasingly designed and implemented with a mix of hardware and software. Such a trend is giving rise to the field of Co-Design, which requires a solid understanding of both. We can have the best software in the world, but if signals initiated by that software cannot accurately propagate down a net from point A to point B, such software is of little use.

# 21.3.3.1 Signal Distortion

If we examine signal characteristics, we can observe two points: distributed circuits will ring if unterminated and lumped circuits may or may not ring. We have already seen that ringing arises in a circuit because of parasitic impedances. The extent of the ringing depends upon the magnitude of a unit-less parameter called the quality factor or Q of the circuit. As the value of Q increases, the damping of the circuit decreases and the slower circuit oscillations die out. The percentage of signal overshoot can be computed by Eq. (21.8):

```
Percentage Overshoot = 100 * e ^ (-pi / sqrt(1-zeta^2)) (21.8)

Q = 1 / (2 * zeta)

\zeta Damping factor
```

The rule of thumb relating circuit Q and signal overshoot for a perfect step input is given in Table 21.2.

Table 21.2 Q vs. Overshoot

| Q | Overshoot (%) |
|---|---|
| 1 | ~15 |
| 2 | ~45 |
| <0.5 | None |

Let's assume we've designed a circuit, kept geometries small, and line lengths short so that we can use a lumped model. We'll use the simple series resistor-inductor-capacitor circuit discussed earlier and illustrated in Figure 21.11 as a first order approximation.

![](bbox=[0.273, 0.813, 0.553, 0.883])

Figure 21.11 Basic Lumped Circuit Model