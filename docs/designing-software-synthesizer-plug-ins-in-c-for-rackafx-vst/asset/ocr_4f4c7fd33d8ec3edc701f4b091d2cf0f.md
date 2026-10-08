the opposite. As it turns out, this sounds natural to our ears. For example, if we have a very low sustain level, we would expect it to have a shorter release time; we typically observe that softsounds decay faster. When we implement this kind of EG in software, we will still store the user's testing times but then calculate the actual decay and release times based on the sustain level. Additionally, we will refer to discharge and release rates rather than times. The equations for the charge Q and discharge of a capacitor normalized to a unit voltage and value are:

```
$$\text{charging} \quad \text{discharging}\nQ = C(1-e^{-t/	au}) \quad Q = Ce^{-t/tau} \qquad (6.1)$
```

The RC term is called the time constant or $	au$. The capacitor's charge/discharge time is related to the time constant. A real-world, non-ideal capacitor charges to up 98% at the time $t=5\tau$. It takes the same amount of time to discharge to 2%. To model the CEM3310, we will let the capacitor charge to 77% and discharge from there. It charges to 77% of the total at the approximate time $t=1\tau$. It discharges in about $t=4.95\tau$. This is shown in Figure 6.7(a). We will generate a graph with the x and y range over the range [0,1], where the x-axis is normalized time and the y-axis is the normalized charge. This allows us to generate these curves scaled by any time duration. Normalizing the R and C values to 1.0, we obtain the equations for a 77% capacitor charge/discharge over a range x $x=[0..1]$ and $y=[0..1]$.

```
$$\text{charging} \quad \text{discharging}\ny = \frac{1}{0.77}(1-e^{-t/\tau}) \quad y = e^{-t/tau} \qquad (6.2)$
```

So Figure 6.7(a) can be split into two components, one for the attack (charging) and the other for the decay and release (discharging) portions.

For controlling an amplifier, it might be desirable to implement an EG output that is linear-in-dB; when you use a fader on a mixing board to control the envelope of a signal, and you move the fader linearly over time, the amplitude changes in a way that is then linear-in-dB. The exponential capacitor voltage movement approximates the linear-dB behavior of a logarithmic potentiometer that is found in the mixing fader. Figure 6.8 shows the exponential capacitor discharge and linear-in-dB curves normalized over the range 0 to 1. For the linear-in-dB curve, the output is normalized over the range 0 dB to -96 dB (-96 dB is chosen as the lower limit since it is the theoretical noise floor for 16-bit digital audio).