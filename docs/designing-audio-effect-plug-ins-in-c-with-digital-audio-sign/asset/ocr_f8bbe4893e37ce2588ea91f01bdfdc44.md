+   - Type: LPF
+   - F_pass low: 1 kHz (the low edge cut-off frequency)
+   - F_stop low: 2 kHz (the lowest frequency that must receive the required stop band attenuation)
+   - Filter order: 16

Now, use the Calculate button to generate the filter. You can see from Figure 8.24 that the filter is not performing exactly to specifications. Although the pass band looks good, the stop band does not. Next, begin increasing the order of the filter using the slider or nudge buttons until you get the stop-band attenuation you desire; for –48 dB of attenuation, you will need a 104th-order filter as shown in Figure 8.25. Finally, check the IR and you will see a truncated version of the sin x(x)/x function (Figure 8.26).

![](bbox=[0.15, 0.26, 0.85, 0.42])

Figure 8.24: The pass-band ripple is well within spec; however, the stop-band attenuation is only getting to about –12 dB.

![](bbox=[0.15, 0.5, 0.85, 0.66])

Figure 8.25: The 104th-order optimal method LPF produces the desired stop-band attenuation.

> The Remez exchange algorithm is not guaranteed to converge. You will receive an error message if it does not converge. Even if the algorithm does converge, the resulting IR is not guaranteed to be finite. Increasing the filter order will not necessarily produce a better design.