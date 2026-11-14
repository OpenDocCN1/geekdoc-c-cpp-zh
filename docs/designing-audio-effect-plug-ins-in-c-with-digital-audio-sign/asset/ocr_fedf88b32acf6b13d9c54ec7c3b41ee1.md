+   - Modulate the $f_c$ or $Q$ with an LFO and the other parameter with the envelope.
+   - Allow the user to select the detection mode: peak, MS, or RMS.
+   - Allow the user to change between linear and log detection (see CEnvelopeDetector's init() method).

# 12.6 Design a Phaser Plug-In

The phaser effect will be on par with the reverb algorithms as among the more complex in the book—the theory is not that difficult, but a nice analog sounding phaser requires many nearly duplicated components, in this case APFs. The phaser effect was an attempt at creating a flanging effect before the necessary analog integrated circuits were available. A flanger uses a modulated delay line to alter the delay time. A phaser uses APFs in an attempt to do the same. APFs have a delay response that is flat across the first one-third or so of the DC-to-Nyquist band. In fact, APFs can be designed to perform fractional delay as an alternative to interpolation. The phaser didn't sound like a flanger at all. The reason is that in a flanger, the notches in the inverse-comb filtering are mathematically related as simple multiples of each other. This is not the case for the phaser. The phaser is still used today in electronic music. Like the flanger, we will get the best results by first looking at the original analog design. Our phaser topology will be based off the analog counterpart in Figures 12.15 and 12.16. Even if you can't read schematics, it's worth a moment to take a look at the overall architecture since we'll be emulating it in digital form. The complete block diagram is shown in Figure 12.17.

The phase of the signal is shifted by 90 degrees at the frequency given by Equation 12.2:

$f_p = \frac{1}{2\pi C_1(R_I/r_{DS})}$ (12.2)

The positive control voltage is a triangle wave, which alters the resistance of the field effect transistor (FET) that is in parallel with $R_I$. This in turn changes the 90 degree phase shift frequency. The values of $C_I$ vary from 1 uF to 0.06 uF, and $r_{DS}$ varies from 100 $\Omega$ (FET on) to 10 K (FET off). The input signal is run through a cascade of such modules. The output of the last module, or stage, is then mixed with the dry input signal to create the effect. You only need to decide on the number of stages and the oscillator to complete the design.

The things to note about the analog design are:

+   - There are six first-order APF modules.
+   - The APF modules are in series, one feeding the next.
+   - The depth control is a blend of the dry and filtered signals; a depth of 100% is actually a 50/50 mix of wet and dry.