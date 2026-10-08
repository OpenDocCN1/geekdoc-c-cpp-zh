
Using a feedback filter to generate an exponentially decaying output.

![](img/b42d0dca53f4a889d8162d55f78c05_355_0.png)
Figure 6.19: Using a feedback filter to generate an exponentially decaying output.

When a constant offset $x_0$ is subtracted from each successive output, the signal decays below 0.0.

![](img/b42d0dca53f4a889d8162d55f78c05_355_1.png)
Figure 6.20: When a constant offset $x_0$ is subtracted from each successive output, the signal decays below 0.0.

# EG Output

The envelope output in digital and analog modes, the sustain level is 0.5 for both. The time (samples) is the time for the segment to rise from 0 to 1, or decay from 1 to 0 (i.e. the full range), and is calculated from the time control on the interface. We supply the value for the TCO to control the curvature, for example, if we let TCO = 0.00673 (since $e^{-5} = 0.00673$) then:

$$ln\left(\frac{1+0.00673}{0.00673}\right) = \frac{-5}{-b}$$

For our analog EG, we just let TCO equal the decay exponent (see Equation 6). This gives us proper charge/discharge cycles. For the digital version, we can make the attack more linear by setting the TCO to 1.0 and then use the linear envelope. The outputs are plotted in Figure 6.21.

$$\begin{aligned}
analog & TCO_{in\_start} = e^{-3} & TCO_{out\_start} = 0.9999 \\
digital & TCO_{in\_end} = e^{-4.95} & TCO_{out\_end} = e^{-1.0}
\end{aligned}$$

Calculating the offset $x_0$ is different for each segment. It is the value that is added or subtracted from the iterative multiplication in the form:

$$y(n) = x_0 + b(n-1)$$
y(n-1) = last EG output

These two values for the coefficient and offset are all set so that the initial value is correct for each segment. They are:

$$x_{attack} = (1+attackTCO)b$$
$$x_{decay} = (sustain-decayTCO)b$$
$$x_{release} = -releaseTCOb$$

These two values for the coefficient and offset are all that's needed to generate the exponential segment. Since the segments often overshoot or undershoot their target values, we can use this mechanism to move through the segments of the envelope generator.

## Biased Envelope Generator Output

The EGs in Figure 6.21 will work fine for controlling the amplitude of our notes. The envelope starts and ends at a value of 0.0. If this EG is used to modulate the pitch of an oscillator or the cutoff frequency of a filter, it might not get the desired effect. For example, the EG is used to alter the pitch of an oscillator with a maximum offset of 2 semitones. The EG would start at 0.0, so no pitch is applied. Then the note would go two sharps as the EG advances through the attack. During the decay, the pitch would fall to the sustain level and remain sharp. Only at the end of the release segment would the note's pitch become correct. In this case, the switch would be playing out of tune. It's worth noting that on some values, this is the standard mode of operation. Pitch EGs and filters often use a biased EG. The sustain level is subtracted from the output so that there is no modulation. In the case of a Pitch EG, the note would start flat, then go sharp, then drop to pitch during the sustain segment. After release, the pitch would go flat. Setting non-zero start and end values is an option to keep the note in pitch at these extremes. The biased EG is shown in Figure 6.22.

## Envelope Generator Intensity Controls and Connections

Many features have an additional control placed between the EG and the target value it modulates. The control is usually labeled intensity and usually has a range of [-1,+1]. The intensity control scale and, if negative, invert the output of the EG. This changes the patch depending on how the user controls are set. Suppose the normal biased EG is used to filter the cutoff frequency, and the user controls the filter cutoff position as shown in Figure 6.23. The intensity control may be the apparent setting of the user–the control does not move, but it is the center of operation for the EG. In Figure 6.23(a) the intensity is set to +1, and at the end of the attack, the cutoff frequency will have the maximum value. With the intensity +0.5, the cutoff moves the same thing in the opposite direction, causing the cutoff frequency to decrease as the attack increases. What if the user had placed the control near the top of the range in Figure 6.23(a)? The answer is that the filter would try to go above its maximum value to the maximum value. Likewise for the negative values. The intensity control is the apparent setting of the user–the control does not move, but it is the center of operation for the EG.

## Envelope Implementation

The EG can be modeled as a Finite State Machine (FSM) with the following states:

- OFF
- ATTACK
- DECAY
- SUSTAIN
- RELEASE
- SHUTDOWN (optional)

The EG starts in the OFF state. A note event advances the FSM into the ATTACK state, and output begins. When the output of the EG reaches the sustain level, the FSM advances to the SUSTAIN state, where it simply waits. A note event advances the FSM into the RELEASE state, where the output begins until it reaches zero. If the EG is shut down (reset-to-zero), the FSM moves into the SHUTDOWN state, where a short linear taper is applied. If a note event occurs in any of the states, the FSM goes back to the RELEASE state.
