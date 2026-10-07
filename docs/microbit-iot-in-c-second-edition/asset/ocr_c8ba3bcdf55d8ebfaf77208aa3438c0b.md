To see the analog wave form, we need to put the digital output into a low-pass filter. A simple resistor and capacitor work reasonably well - the cut-off frequency for the filter is shown is 200Hz.

![](bbox=[0.335, 0.178, 0.662, 0.293])

The filter's cut-off is a little on the low side as can be seen by the slow fall to ground the end of each waveform. However, if you increase the cut-off then even more irregularities will show in the ramp. The reason for these irregularities is the short time each duty cycle is presented and the glitches occur when changing duty cycle.

![](bbox=[0.335, 0.431, 0.703, 0.601])

If you change the wait to 200 so that six or so duty cycles are presented the result looks smoother and with fewer glitches:

![](bbox=[0.335, 0.659, 0.703, 0.829])