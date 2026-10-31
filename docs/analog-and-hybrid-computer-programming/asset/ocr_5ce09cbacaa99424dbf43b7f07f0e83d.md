![](bbox=[0.3, 0.05, 0.8, 0.2])

Fig. 5.11. Basic circuit of a low pass filter

normal distribution of the output signal is required, it can be readily obtained by using a suitable function generator.

Implementing a low pass filter on an analog computer is extremely simple as it just resembles a 1st-order time lag with the general transfer function

$F(p) = \frac{1}{1 + pT}$

where $T$ represents the time constant of the delay line.52 This setup, shown in figure 5.11, basically yields a time varying mean value of its input signal. This mean gets "better" as the time constant of the circuit increases – but this also implies that the circuit needs a longer time span to settle on the mean value.

Typically, both coefficient potentiometers are set to identical values although sometimes a certain deviation from the "ideal" setting may be advantageous depending on the desired output signal.

Figure 5.12 shows a white noise signal ranging from 0 Hz to 100 kHz obtained from a professional noise generator in the upper third of the screen. The curve in the middle is the result of applying one low pass filter of the structure shown above while the lower trace results represents the output signal of a second low pass filter connected to the output of the first filter.

# 5.5 Triangle/square wave generator

Sometimes it is desirable to have a triangle or square wave signal available. Typical applications for a triangle wave are the x-deflection for an oscilloscope or plotter while square waves are often handy to control electronic switches to display more than one curve or figure on an oscilloscope.53

52 Cf. [GLOI et al. 1963, p. 308] and appendix B for more details. p is an operator implementing a time derivative.

53 Cf. [KORN et al. 1964, ch. 9-5].