![](bbox=[0.22, 0.0, 0.78, 0.15])

Figure 5.9: One way to divide the 2π range of frequencies includes both positive and negative frequencies.

For filter evaluation, ω varies on a 0 to 2π radians/second range and one way to think about this 2π range is to split it up into the range from –π to +π corresponding to –Nyquist to +Nyquist (Figure 5.9).

![](bbox=[0.22, 0.3, 0.78, 0.45])

Figure 5.10: Mapping the 0 to 2π range of frequencies across the 0 to fs range.

> > To evaluate the transfer function, let ω vary from 0 to π and get the first half of the response. The other half is a mirror image of the data.

# ## 5.4.2 Frequencies Above and Below ±Nyquist

The sampling theorem sets up the Nyquist criteria with regards to completely recovering the original, band-limited signal without aliasing. However, frequencies above Nyquist and all the way up to the sampling frequency are also allowed mathematically. And in theory, any frequency could enter the system and you could sample it without limiting Nyquist. For a frequency or phase response plot, the frequencies from Nyquist up to the sampling frequency are a mirror image about Nyquist. This is another way to divide up the 2π range by going from 0 Hz to the sampling frequency (Figure 5.10).

Notice that in either method the same information is conveyed as we get both halves of the curves, and in both cases, Nyquist maps to π and 0 Hz to 0 and positive frequencies map to the range 0 to π.

# ## 5.5 Evaluating the Transfer Function H(ω)

DSP filter transfer functions will contain e^(-jωn) terms that need to be evaluated over the range of 0 to π; the way to do this is by using Euler's equation to decompose the sinusoid into its real (cos) and imaginary (sin) components. Then, evaluate the cos and sin terms at the frequency in question. In the