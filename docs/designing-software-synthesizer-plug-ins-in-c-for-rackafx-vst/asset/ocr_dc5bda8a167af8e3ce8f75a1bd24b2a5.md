The pitch and exponential modulation inputs use the same pitch multiplier to calculate their shift. Linear modulation will add or subtract an offset that represents the modulation amount at any given time. For pitch bend, the curve chooses the minimum and maximum value for the shift. For linear modulation in FM synthesis, the hard-coded or defined limits are employed. For FM synthesis, the limits are +/- Nyquist as described in Chapter 13 (note that we will actually use phase modulation in Chapter 13, but we will discuss that later).

# Bipolar Modulation

We will allow the pulse width to be modulated if the waveform is a square wave. The oscillator's PWM modulation input accepts values from [-1.+1]. It is worth noting the pulse width in detail since we will see other modulation calculations done the same time. The pulse width control voltage acts as the center of modulation. The current modulation dPWMod from [-1.+1], by multiplying this by the values in the limit defined by modulation produces a proper output value. For any kind of bipolar modulation, the function will be:

In case of unipolar modulation, will always simply convert the unipolar value to bipolar first. The next few chapters you will see the exceptions to this rule.

```
finalValue = center + modValue * \frac{highLimit - lowLimit}{lowLimit}
```

Finally, we also note that any oscillator should be modulated by any other oscillator. For example, a LFO code modulates the frequency of. Figure 5.39 (a) shows the detailed block diagram for this oscillator, Figure 5.39 (b) shows the simplified version. For our first we will use many oscillators, so we can focus on now. The inputs to the oscillator block consist of two types of modulation: control and bipolar. Typically (but not all) Figure 5.39 (a) shows all possible control modulation inputs on the user interface, which will connect to other objects. In our diagrams, we may exclude some of the inputs if we are not using them (for example, the Phase Modulation input is only used in our FM synthesis. In Figure 5.39 (b) notice how the input at the bottom is opposed to the bipolar frequency modulation.

Figure 5.39: two oscillator symbols: (a) the generic, detailed block diagram and (b) the simplified version.

![](bbox=[0.368, 0.506, 0.922, 0.706])

# 5.25 Pit Oscillator Starting Phase Considerations

For quasi banded oscillators, it is important that the phases of the oscillator line up properly with a sinus. This means that the zeros at the half point line up, assuming 50% duty cycle for the square wave. The square wave already lines up with properly, but the sawtooth and triangle wave do not. The zero crossing edge is 50% offset from the sinus or square. This means their module's starting point needs to be. The sawtooth and triangle waves will start with the modulo = 0.5. This is shown graphically in Figure 5.40. We will not implement this phase-line for LFOs because we desire their intrinsically shake, especially in one-shot. This is also not necessary for the wavetable, since their location is based on a index and not a module value and the banded wavetables are already aligned properly in Figure 5.40 (b).

# 5.26 LFO Features

For a LFO, the user is allowed to adjust the wavetable rate (frequency) and depth (amplitude) of the oscillator. Additional controls may also include:

+   - time delay before oscillations start