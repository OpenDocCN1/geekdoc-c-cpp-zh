frequency axis. What makes this filter a low-pass filter? It is a combination of the coefficients and the filter topology (first-order feed-forward). There are three basic topologies: feed forward (FF), feed back (FB), and a combination of FF/FB. Once the topology has been chosen, it’s really the coefficients that determine what the filter will do.

![](bbox=[0.13, 0.11, 0.87, 0.27])

Figure 4.17: The time domain plots of the impulse response input/output.

A feed-forward filter will be a linear phase filter if its coefficients are symmetrical about their center. In this case (0.5, 0.5) is symmetrical. Another example would be (–0.25, 0, –0.25).

![](bbox=[0.13, 0.41, 0.87, 0.82])

Figure 4.18: Final frequency and phase response plots for the digital filter in Figure 4.6. Notice that this is a linear frequency plot since ½ Nyquist is halfway across the x-axis. The phase at Nyquist pops back up to 0 degrees since there is no Nyquist component present (output = 0).

# 4.2 Design a General First-Order Feed-Forward Filter