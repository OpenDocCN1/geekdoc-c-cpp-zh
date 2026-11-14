where N is the bit depth of the system.

# 1.8 Basic DSP Test Signals

You need to know the data sequences for several fundamental digital signals in order to begin understanding how the DSP theory works. The basic signal set consists of

+   - Direct Current (DC) and step: DC is a 0Hz signal
+   - Nyquist
+   - ½ Nyquist
+   - ¼ Nyquist
+   - Impulse

The first four of these signals are all you need to get a ballpark idea of the frequency response of some basic DSP filters. The good news is that all the sequences are simple to remember.

# 1.8.1 DC and Step

The DC or 0 Hz and step responses can both be found with the DC/step input sequence: {...0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1...}.

This signal in Figure 1.11 contains two parts: the step portion where the input changes from 0 to 1 and the DC portion where the signal remains at the constant level of 1.0 forever. When you apply this signal to your DSP filter and examine the output, you will get two pieces of information. The step portion will tell you the transient attack time and the DC portion will give you the response at DC or 0 Hz.

![](bbox=[0.32, 0.56, 0.68, 0.73])

Figure 1.11 Representation of the DC/Step sequence.

# 1.8.2 Nyquist

The Nyquist input sequence represents the Nyquist frequency of the system and is independent of the actual sample rate. The Nyquist sequence is {...-1, +1, -1, +1, -1, +1, -1, +1...}.

The Nyquist frequency signal in Figure 1.12 is the highest frequency that can be encoded. It contains the minimum of two samples per cycle with each sample representing the maximum and minimum values. The two-sample minimum is another way of stating the Nyquist frequency as it relates to the sampling theorem.