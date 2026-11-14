
However, they will not share the same cutoff frequency, but will rather be mirror images of each other. Thus, the first filter design above with a cutoff point of 5.5 kHz would produce an HPF with a cutoff frequency 5.5 kHz below Nyquist. Table 8.1 shows the coefficients, while Figure 8.17 shows the frequency response.

Table 8.1: The LPF and complementary HPF coefficients for the current design.

| Low-Pass Filter | Complementary High-Pass Filter |
|---|---|
| a0 = 0.02598719 | a0 = -0.02598719 |
| a1 = 0.01331121 | a1 = 0.01331121 |
| a2 = -0.02018474 | a2 = 0.02018474 |
| a3 = -0.05761180 | a3 = -0.05761180 |
| a4 = -0.04827195 | a4 = 0.04827195 |
| a5 = 0.04957144 | a5 = 0.04957144 |
| a6 = 0.20692666 | a6 = -0.20692666 |
| a7 = 0.33027202 | a7 = 0.33027202 |
| a8 = 0.33027202 | a8 = -0.33027202 |
| a9 = 0.20692666 | a9 = 0.20692666 |
| a10 = 0.04957144 | a10 = -0.04957144 |
| a11 = -0.04827195 | a11 = -0.04827195 |
| a12 = -0.05761180 | a12 = 0.05761180 |
| a13 = -0.02018474 | a13 = -0.02018474 |
| a14 = 0.01331121 | a14 = -0.01331121 |
| a15 = 0.02598719 | a15 = 0.02598719 |

![](img/b54974d0a4317ec82d7ae02126d10a6f_256_0.png)

Figure 8.17: The complementary HPF has its cut-off point at 16.5 kHz and you can see the rotation about the ½ Nyquist frequency.

## 8.6 Using RackAFX's Frequency Sampling Method Tool

RackAFX allows you to implement frequency sampling method filters by drawing responses directly on the analyzer's frequency response plots. You can place as many points as you like as well as choose the order (even only) of the filter. The previous examples were done using the frequency sampling method tool. Let's do an example similar to the last one but in the log frequency domain instead. First, click on the radio button marked frequency sampling method and you will see a red horizontal line appear on the graphs. Make sure the frequency axis is log. In this design, let's try to make a resonant LPF with a peak frequency around 1 kHz.

You will see two boxes on the red line, one at DC, the other at Nyquist. These points cannot be removed. To enter points and move them, use the following rules:

- Right-click on the red line to add a new point.
- Click on the new point and drag it up or down.
- To remove a point, right-click on it and choose “delete point” from the pop-up menu.
- Hit the Calculate button when you are done to view the resulting filter.

Hit the Frequency Sampling button and note the filter order of 64 (if it is not 64, change it with the slider or the edit control). Create a resonant LPF with a peak frequency of 1 kHz. In Figure 8.18 you can see the bandwidth of the peak is 1.5 kHz and the response goes to –60 dB at = kHz. Next, hit the Calculate button to get Figure 8.19.

You can use the order slider to slowly increase the filter order until the response matches your sampled points as closely as possible. You can move the slider, or type an order into the edit box and hit the Tab button to inject it. You can also use the small up/down arrow buttons to advance the order up or down in even increments. Typically, the way you would use this is to first get close with the slider, then use the up/down arrows to fine tune the design. Figure 8.20 shows the same filter with the order set to 164.

![](img/b54974d0a4317ec82d7ae02126d10a6f_257_0.png)

Figure 8.18: The prototype resonant LPF sampled points.

![](img/b54974d0a4317ec82d7ae02126d10a6f_258_0.png)

Figure 8.19: The 64-tap FIR filter produces marginal results with poor stop-band attenuation.

Play an audio file through the new filter and listen to the resonant LPF characteristics. Here are some interesting things you can do in RackAFX while the audio file is playing or looping:

- You can move the order control; the filter will be updated in real time and you can hear the results.
- You can add or remove points on the desired response or move them around, then hit Calculate to update the filter in real time, and you can also hear the results.
- You can save the IR as a file, then load it into the Impulse Convolver module just as before.

## 8.7 Designing a Complementary Filter

You can convert any design into a complementary design by hitting the Complementary button. With the current 164th-order resonant LPF, first switch to the linear scale (Figure 8.21).

Hit the Complement button to create the complementary HPF filter. The original design points are left to show you the complementary nature of the filter. You can clearly see the rotation about ½ Nyquist here (Figure 8.22). You can perform this operation while audio files are playing in RackAFX as well. If you look at the IRs in the .sir file you can see the operation of negating the odd-numbered coefficients.

![](img/b54974d0a4317ec82d7ae02126d10a6f_258_1.png)

Figure 8.20: The 164th-order FIR filter produces an excellent match to the specifications.

![](img/b54974d0a4317ec82d7ae02126d10a6f_259_0.png)

Figure 8.21: The linear domain frequency response of the 1-kHz LPF.

![](img/b54974d0a4317ec82d7ae02126d10a6f_259_1.png)

Figure 8.22: The complementary HPF shows the mirror image nature of complementary filter designs; the new resonant peak is 1 kHz below Nyquist.

## 8.8 The Optimal (Parks–McClellan) Method

FIR filters produce all zeros in the z-plane. You can see the effect of these zeros in the frequency sampling method filters we designed—they create the notches and humps in the frequency response. In general, we seek to minimize the humps in the pass band and set some kind of limit for the largest lobe we see in the stop band. In the frequency sampling filters, we changed the design specifications or the order of the filter to get a response that satisfied our initial desired response to some extent. The optimal method is an algorithm for designing classical filters (LPF, HPF, BPF, BSF). You can create filters with extremely steep roll-off edges that would be difficult to synthesize in the analog domain. The word “optimal” comes from the engineering phrase “optimal in the Chebychev way,” which describes a filter design with a certain kind of rippling in the pass band and stop band.

The LPF in Figure 8.23 might be specified like this:

- Pass-band ripple: less than 0.1 dB
- Stop-band attenuation: greater than –24 dB

The pass-band ripple (0.1 dB) and stop-band attenuation (–24 dB) are converted into weighting values using Equation 8.6:

```
Pass-band-weight = (10^(p_ripple/20)) - 1
Stop-band-weight = (10^(s_atten/20))
(8.6)
```

The optimal method uses these weighting values in its design calculation. The weightings give acceptable error tolerances in each band. If the weights are equal, then there will be an equal deviation from the ideal in both bands. This is called an equiripple design. The specifications for the optimal method are:

![](img/b54974d0a4317ec82d7ae02126d10a6f_260_0.png)

Figure 8.23: An FIR LPF can be specified by the acceptable ripple in the pass band (barely observable here) and the minimum stop-band attenuation.

- The pass-band and stop-band frequencies
- The maximum pass-band ripple and minimum stop-band attenuation
- The order of the filter (the number of zeros in the frequency response)

The algorithm works by first distributing the zeros out equally across the frequency axis. This is going to produce a series of humps in the pass band (the ripple) and lobes in the stop band. The ripples and lobes will produce a set of maxima and minima frequencies. The problem is that for a given specification, the locations of the extremal frequencies are not known before hand. The optimal method must use a search algorithm to iteratively move the locations around until a solution is found that is within the tolerance of the specifications. The optimal method uses an algorithm called the Remez exchange method to iteratively move the zeros around until a solution converges. It must be noted that the Remez exchange algorithm is not guaranteed to converge for a given set of specifications.

Once the Remez exchange method finds the locations of the extremal frequencies, the resulting H(f) graph is sampled using the frequency sampling method to produce the IR, which is the set of FIR filter coefficients. To summarize the method:

- Specify the filter parameter and order.
- Equally distribute zeros across the spectrum.
- Set the pass-band and stop-band weights.
- Use the Remez exchange algorithm to iteratively find the location of the zeros.
- Sample the resulting frequency response to produce the final IR.

## 8.9 Using RackAFX's Optimal Method Tool

RackAFX lets you design any of the four classical filter types using the equiripple weighting for the pass band and stop band. BPF and BSF filters have an additional band edge to specify, but the meaning of pass-band ripple and stop-band attenuation is the same for all filter types. You can start with an LPF design by clicking on the Optimal button. Try the following filter specifications:
