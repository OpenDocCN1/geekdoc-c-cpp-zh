
![](img/b54974d0a4317ec82d7ae02126d10a6f_83_0.png)

Figure 4.1: The fundamental analysis tool for a DSP filter is its frequency response plot. This graph shows how the filter amplifies or attenuates certain bands of frequencies.

![](img/b54974d0a4317ec82d7ae02126d10a6f_83_1.png)

Figure 4.2: The phase response plot of the analog filter in Figure 4.1 shows how the phase of the output is shifted across frequencies.

We observe several features of the output:

- The composite waveform is smoothed out.
- The amplitude and phase shift of the fundamental are unchanged.
- The three harmonics have decreasing amplitudes and more phase shift as you go higher in frequency.

Figure 4.4 shows the same filter with the information plotted differently; here, the amplitudes and phases are plotted against frequency rather than dealing with a set of time-domain sinusoids. You can see by the output frequency response plot that this filter is a kind of low-pass filter. Its curve is similar to Figure 4.1, the analog equivalent.

![](img/b54974d0a4317ec82d7ae02126d10a6f_84_0.png)

Figure 4.3: A complex waveform is filtered into a smoothed output. The input and output are decomposed into their Fourier-series components.

![](img/b54974d0a4317ec82d7ae02126d10a6f_84_1.png)

Figure 4.4: The same information is plotted as frequency and phase responses.

## 4.1 First-Order Feed-Forward Filter

In order to get a grip on the nature of digital filtering, start with the first-order feed-forward filter shown in a block diagram in Figure 4.5. You've already seen a version of it in the HPF tone control you coded in the last chapter.

The difference equation is as follows:

```
y(n) = a₀x(n) + a₁x(n – 1) (4.1)
```

You can tell why it's called feed forward—the input branches feed forward into the summer. The signal flows from input to output. There is no feedback from the output back to the input. Now, suppose we let the coefficients $a_0$ and $a_1$ both equal 0.5 in Figure 4.6.

In order to analyze this filter we can go the easy but tedious route or the difficult but elegant route. Let's start with the easy way. In order to figure out what this does, you apply the five basic digital test signals you learned in Chapter 1 to the filter and then manually push the values through and see what comes out. You only need a pencil and paper or a simple calculator. The five waveforms we want to test are:

- 1. DC (0 Hz)
- 2. Nyquist
- 3. ½ Nyquist
- 4. ¼ Nyquist
- 5. Impulse

![](img/b54974d0a4317ec82d7ae02126d10a6f_85_0.png)

Figure 4.5: The first-order feed-forward filter.

![](img/b54974d0a4317ec82d7ae02126d10a6f_85_1.png)

Figure 4.6: What kind of filter is this? What are its frequency and phase responses?

For each audio sample that enters there are two phases to the operation:

- 1. Read phase: The sample is read in and the output is formed using the difference equation and the previous sample in the delay register.
- 2. Write phase: The delay element is overwritten with the input value—the sample stored in the single $z^{-1}$ register is effectively lost.

Start with the DC/step input and begin sequentially applying the samples into the filter shown in Figures 4.7 through 4.10.

Now, observe the amplitude and phase shift of the input versus output—the output amplitude eventually settles out to a constant 1.0 or unity gain condition, so at DC or 0 Hz, the output equals the input. However, there is a one sample delay in the response, causing the leading edge of the step-input to be smeared out by one sample interval. This time smearing is a normal consequence of the filtering.

![](img/b54974d0a4317ec82d7ae02126d10a6f_86_0.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_86_1.png)

Figure 4.7: On the first iteration the input sample is used in the difference equation to create the output, x(n) = 0, y(n) = 0 and then the input is shifted into the delay register.

In a feed-forward filter, the amount of time smearing is equal to the maximum delayed path through the feed-forward branches.

![](img/b54974d0a4317ec82d7ae02126d10a6f_86_2.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_86_3.png)

Figure 4.8: The process continues with each sample. Here the input 1.0 is combined with the previous input; the second output y(n) = 0.5.

Next, repeat the process for the Nyquist frequency (DC and Nyquist are the easiest, so we'll do them first). The filter behaves in an entirely different way when presented with Nyquist (Figures 4.11 through 4.14).

Now, make your observations about amplitude and phase. The amplitude at Nyquist eventually becomes zero after the one-sample-delay time. The phase is hard to tell because the signal has vanished. Why did the amplitude drop all the way to zero at Nyquist? The answer is one of the keys to understanding digital filter theory: the one-sample delay introduced exactly 180 degrees of phase shift at the Nyquist frequency and caused it to cancel out when recombined with the input branch through $a_0$.

Delay elements create phase shifts in the signal. The amount of phase shift depends on the amount of delay as well as the frequency in question.

![](img/b54974d0a4317ec82d7ae02126d10a6f_87_0.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_87_1.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_87_2.png)

Figure 4.9: The sequence continues until we observe a repeating pattern; 1.0 is repeating here.

In the case of Nyquist, the one-sample delay is exactly enough to cancel out the original signal when they are added together in equal ratios. What about other frequencies like ½ and ¼ Nyquist? They are a bit more laborious to work through but worth the effort. By now you can see how the data moves through the filter, so let’s use a table (Table 4.1) and move the data through it instead. The ½ Nyquist sequence is x(n) = {..., 0, +1.0, 0.0, -1.0, 0.0, +1.0, 0.0, ...}.

![](img/b54974d0a4317ec82d7ae02126d10a6f_88_0.png)

Figure 4.10: The input and output sequences for the filter in Figure 4.6 at DC or 0 Hz.

![](img/b54974d0a4317ec82d7ae02126d10a6f_88_1.png)

Figure 4.11: The Nyquist sequence is applied to the filter. Notice how the delay element has been zeroed out. The output for the first iteration is y(n) = 0.5.

![](img/b54974d0a4317ec82d7ae02126d10a6f_89_0.png)

Figure 4.12: The second iteration at Nyquist produces an output y(n) = 0.

Table 4.1: The manual labor continues as we work through the ½ Nyquist frequency.

| x(n) | x(n - 1) | y(n) = 0.5x(n) + 0.5x(n - 1) |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 0.5 |
| 0 | 1 | 0.5 |
| -1 | 0 | -0.5 |
| 0 | -1 | -0.5 |
| 1 | 0 | 0.5 |
| 0 | 1 | 0.5 |
| -1 | 0 | -0.5 |
| 0 | -1 | -0.5 |

Can you see how x(n) becomes x(n - 1) for the next row? The x(n - 1) column holds a one-sample-delayed version of the input x(n). The output is y(n) = {0, +0.5, +0.5, -0.5, -0.5, +0.5, +0.5}.

![](img/b54974d0a4317ec82d7ae02126d10a6f_90_0.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_90_1.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_90_2.png)

Figure 4.13: Continuing the operation at Nyquist, we see that eventually the output settles to a repeating 0, 0, 0, 0 sequence.

Next we observe the amplitude and phase relationship from input to output in Figure 4.15. At first it might seem difficult to figure out the sequence {...-0.5, -0.5, +0.5, +0.5, ...}. 1/2 Nyquist is also encoded with a repeating sequence of four values (0, 1, 0, -1).

Work through 1/4 Nyquist the same way (Table 4.2). The 1/4 Nyquist frequency sequence is x(n) = {0, 0.707, 1, 0.707, 0, -0.707, -1, -0.707, 0, ...}.

![](img/b54974d0a4317ec82d7ae02126d10a6f_90_3.png)

Figure 4.14: The input and output sequences for the filter in Figure 4.6 at Nyquist.

Table 4.2: ¼ Nyquist input/output.

| x(n) | x(n - 1) | y(n) = 0.5x(n) + 0.5x(n - 1) |
| :--- | :--- | :--- |
| 0 | 0 | 0 |
| 0.707 | 0 | +0.354 |
| 1 | 0.707 | +0.854 |
| 0.707 | 1 | +0.854 |
| 0 | 0.707 | +0.354 |
| -0.707 | 0 | -0.354 |
| -1 | -0.707 | -0.854 |
| -0.707 | -1 | -0.854 |
| 0 | -0.707 | -0.354 |

The output is y(n) = {...+0.354, +0.854, +0.854, +0.354, -0.354, -0.854, -0.854, -0.354, +0.354, ...}. Analysis of the output sequence reveals the phase-shifted and slightly attenuated output signal at ¼ Nyquist. Both the phase shift and the attenuation are smaller than ½ Nyquist. As you can see in Figure 4.16 there is also one sample of time smearing at the start of the signal.

Finally, apply the impulse sequence and find the impulse response. The impulse response is the third analysis tool. The impulse response defines the filter in the time domain like the frequency response defines it in the frequency domain. The basic idea is that if you know how the filter reacts to a single impulse you can predict how it will react to a series of impulses of varying amplitudes. Take a Fast Fourier Transform (FFT) of the impulse response and you get the frequency response. An inverse FFT converts the frequency response back into the impulse response. For this filter the impulse response is simple (Table 4.3).

![](img/b54974d0a4317ec82d7ae02126d10a6f_91_0.png)
