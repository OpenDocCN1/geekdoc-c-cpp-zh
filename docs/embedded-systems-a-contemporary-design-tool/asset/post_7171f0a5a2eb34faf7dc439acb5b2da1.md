
Multilayer PCBs can provide variety of microstrip and stripline structures. In the design of either structure, the conductor geometry, and control of the conductor and dielectric layers, is critical. Particularly crucial to ensuring predictable transmission line characteristics is the characteristic impedance (impedance looking into a transmission line) and the propagation velocity (the velocity at which signal moves down a transmission line).

## 21.3.2 Signal Propagation

Electrical signals in conducting wires or circuit traces propagate at a velocity that is dependent upon the surrounding medium. Factors that can affect propagation velocity include the trace geometry and the dielectric material of the PCB, which is typically FR4. FR4 is a material composed of fiberglass cloth with an epoxy resin binder.

Propagation velocity is measured in picoseconds per inch and the delay along the conducting path increases in proportion to the square root of the dielectric constant of the surrounding medium. The propagation velocity delays for several common mediums are given in Table 21.1.

Table 21.1 Propagation Velocity vs. Surrounding Medium

| Medium | Delay (ps in⁻¹) | Dielectric constant |
| :--- | :--- | :--- |
| Air – Radio waves | 85 | 1 |
| Coaxial cable | 129 | 23 |
| FR4 PCB microtrace | 140-180 | 2.8–4.5 |
| FR4 PCB outer trace | 140-150 | 2.8–4.5 |
| FR4 PCB inner trace | 180 | 4.5 |

ᵃ Determines if electric field stays within board or goes into air.
ᵇ Note: Outer layer signals will always be faster than those on the inner layers.

From the diagrams and data above, we can make two observations.

Consider a system in which we have a 5-in. long data bus with 1 GHz signaling. Let the signal be a square wave. At such a frequency, the signal will have a 1000 ps period. Place some traces on an outer layer and others on an inner layer. From Table 21.1, a 40 ps/in difference in propagation delay between inner and outer layers is possible. With 1 GHz signaling and traces routed on both an inner layer and an outer layer, signals starting simultaneously at an initial point on the bus arrive at the destination with a potential signal skew of 5 x 40 ps = 200 ps. Such a difference is the equivalent to 20% of the signaling period. If the signaling frequency is increased to 10 GHz, which is in the range of feasible today, the signaling skew at destination is equivalent to 200% of the 100 ps signaling period.

Now, consider a signal that enters the conducting path at time t₀. Let the signal propagate the same distance down the two paths as shown in Figure 21.10.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_982_0.png)

Figure 21.10 Signal Propagating Along a Conducting Path

In the circuit on the left, the signal reaches point z at time t₁; however, in the circuit on the right, the signal does not arrive until time t₄. In the circuit on the right, when the signal reaches point x at time t₁, a potential difference will exist at that point between the forward path and the return path. At points y and z, however, the potential difference will be 0 until the signal reaches y at time t₂ or z at time t₃. Such a difference produces an electric field between the forward and return conductors along the signal path. Further, when current flows through the conductor, it produces a magnetic field around conductor.

### 21.3.2.4 Distributed Versus Lumped

- effective length
- lumped
- distributed

If we look at the time duration of a signal with respect to its propagation delay through the system, we find an interesting phenomenon. We can define a property called the *effective length* of an electrical feature or characteristic such as a signal’s rising or falling edge. Such a property governs whether to analyze a system using a *lumped* or *distributed* circuit model. In a lumped model, a signal change appears to all points connected to the signal source at the same time, as shown in the left-hand drawing in Figure 21.10. In a distributed model, a signal change appears to all points connected to the signal source at different times, as shown in the right-hand drawing in Figure 21.10.

The effective length, eL, of a feature depends upon its duration and its propagation delay through system. The effective length, eL, of a signal can be heuristically defined in Eq. (21.7).

```
eL = \frac{\tau_{rise}}{D} \tag{21.7}
eL = effective length in inches
\tau_{rise} = rise time
D = delay time on ps/in
```

Consider the intuitive extremes in Figure 21.10. If the signal rise time is less than the propagation delay to its destination, all associated inputs see (similar levels of) the signal at essentially the same time. However, if the signal rise time is greater than propagation delay to the destination, all associated device inputs will see (different levels of) the signal at different times as it propagates from source to destination.

The response of a system of conductors to an incoming signal depends greatly upon the effective length of the fastest electrical feature in signal. A conductor is considered electrically long if its physical length is a large fraction of the conducted signal’s wavelength.

Consider the following signals:

- (i) 1 ns rise time – typical for ECL (emitter coupled logic) 10 K
  - 140 ps/in delay – PCB outer
  - We compute an effective length, eL, of 7.1 in.

- (ii) 4 ns rise time – typical for TTLS (transistor transistor logic schottky)
  - 140 ps/in delay – PCB outer
  - We compute an effective length, eL, of 30 in.

What this means is that as a signal enters a trace and propagates along, the potential is not uniform along the trace. The reaction of the system to the incoming pulse is similarly distributed along the trace. We call systems that are physically small enough to react together with uniform potential *lumped*. Larger systems, with nonuniform potential, are called *distributed*. Classification into lumped versus distributed depends upon the *rise or fall times* of the signals flowing through and only indirectly on the frequency of the signals. The rule of thumb or heuristic for PCB traces using point-to-point wiring versus transmission lines is that wiring shorter than 1/6 of the effective length behaves mostly in a lumped fashion.

## 21.3.3 Point-to-Point Wiring

We will now examine point-to-point wiring and identify some of the potential shortcomings. Consider today's evolving systems that are increasingly designed and implemented with a mix of hardware and software. Such a trend is giving rise to the field of Co-Design, which requires a solid understanding of both. We can have the best software in the world, but if signals initiated by that software cannot accurately propagate down a net from point A to point B, such software is of little use.

### 21.3.3.1 Signal Distortion

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

![](img/679b8d2d47f1bf86e17aca48f596f5cc_984_0.png)

Figure 21.11 Basic Lumped Circuit Model
