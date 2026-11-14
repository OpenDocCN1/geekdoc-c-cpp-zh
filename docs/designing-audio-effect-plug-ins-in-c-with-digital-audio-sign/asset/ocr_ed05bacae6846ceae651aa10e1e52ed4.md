# 8.6 Using RackAFX's Frequency Sampling Method Tool

RackAFX allows you to implement frequency sampling method filters by drawing responses directly on the analyzer's frequency response plots. You can place as many points as you like as well as choose the order (even only) of the filter. The previous examples were done using the frequency sampling method tool. Let's do an example similar to the last one but in the log frequency domain instead. First, click on the radio button marked frequency sampling method and you will see a red horizontal line appear on the graphs. Make sure the frequency axis is log. In this design, let's try to make a resonant LPF with a peak frequency around 1 kHz.

You will see two boxes on the red line, one at DC, the other at Nyquist. These points cannot be removed. To enter points and move them, use the following rules:

+   - Right-click on the red line to add a new point.
+   - Click on the new point and drag it up or down.
+   - To remove a point, right-click on it and choose “delete point” from the pop-up menu.
+   - Hit the Calculate button when you are done to view the resulting filter.

Hit the Frequency Sampling button and note the filter order of 64 (if it is not 64, change it with the slider or the edit control). Create a resonant LPF with a peak frequency of 1 kHz. In Figure 8.18 you can see the bandwidth of the peak is 1.5 kHz and the response goes to –60 dB at = kHz. Next, hit the Calculate button to get Figure 8.19.

You can use the order slider to slowly increase the filter order until the response matches your sampled points as closely as possible. You can move the slider, or type an order into the edit box and hit the Tab button to inject it. You can also use the small up/down arrow buttons to advance the order up or down in even increments. Typically, the way you would use this is to first get close with the slider, then use the up/down arrows to fine tune the design. Figure 8.20 shows the same filter with the order set to 164.

![](bbox=[0.15, 0.62, 0.85, 0.79])

Figure 8.18: The prototype resonant LPF sampled points.