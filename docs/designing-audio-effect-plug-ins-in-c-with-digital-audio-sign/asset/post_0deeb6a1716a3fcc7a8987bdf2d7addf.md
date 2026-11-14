
a sample count inside the delay). In your code, there are two basic ways to do this:

- 1. Subtract the delay amount (in samples) from your write index, wrapping the pointer backwards if needed, to locate the delayed sample.
- 2. Store a read index and offset the two indices when the user changes the delay amount.

The second option is better because you only have to offset the index values and perform the subtraction/wrap when the user changes the delay value, instead of each time through the processAudioFrame() loop. Suppose the user selects 100 samples of delay time. You have declared two indices, m_nRead and m_nWrite, to use for buffer. During the processAudioFrame() function you will need to do the following five steps.

Step 1: Read out the delayed audio data, d(n–D–100), which is 100 samples behind the current x(n) sample time; this value is y(n), the current output value (Figure 7.7).

```
float yn = pBuffer[m_nRead];
```

Step 2: Form the input combination input + feedback * output:

```
float xn = pInputBuffer[0] + m_fFeedBack*yn;
```

m_fFeedBack is declared in your .h file; this example code is for processing the left channel, pInputBuffer[0].

Step 3: Write the input data into the delay line at the m_nWrite location (Figure 7.8).

Step 4: Increment the read and write pointers by one to set up for the next time through the function; check for wrapping and do that if necessary. Can you think of other ways to do this?

```
// inc/wrap
m_nWrite++;
if(m_nWrite >= m_nBufferLength)
m_nWrite = 0;

m_nRead++;
if(m_nRead >= m_nBufferLength)
m_nRead = 0;
```

![](img/b54974d0a4317ec82d7ae02126d10a6f_208_0.png)

Figure 7.7: The delayed sample is read at location d(n–D–100), 100 samples before the current write location.

![](img/b54974d0a4317ec82d7ae02126d10a6f_209_0.png)

Figure 7.8: The delayed sample plus feedback is written into the current write location.

Notice that we wrap if the incremented index hits nBufferLength because this references the location just one sample outside the delay line.

Step 5: In the event that the user changes the delay time, you need to recalculate the m_nRead index to accommodate it. Note that once set up, the m_nWrite index is never changed except to increment it through the line. In this example, the user has selected nSamples of delay in the plug-in.

```
// user selects mSample delay
// first subtract the index
m_nRead = m_nWrite - nSamples;

//the check and wrap BACKWARDS if the index is negative
if (m_nRead < 0)
    m_nRead += nBufferLength; // amount of wrap is Read + Length
```

## 7.2 Digital Delay with Wet/Dry Mix

Although there may be some instances where you don't need a wet/dry mix, in general when you make a delay plug-in, you still want to hear your unaffected signal. This can be done by using the plug-in as an Auxiliary (AUX) Send effect rather than an insert effect. But, to provide both capabilities, you need to provide the user with a wet/dry ratio control. The block diagram is slightly modified as shown in Figure 7.9.

The difference equation is as follows:

```
y(n) = dry*x(n) + wet*[x(n-D) + fb*y(n-D)] ....................................................(7.2)
```

### 7.2.1 Frequency and Impulse Responses

Consider the basic delay with no feedback applied and with the wet/dry ratio at 1:1. The block diagram and difference equation would then reduce down to Figure 7.10.

The difference equation is as follows:

```
y(n) = x(n) + x(n-D) ............................................................................................(7.3)
```

To find the frequency response, first take the z transform of the difference equation and form the transfer function:

y(n) = x(n) + x(n-D)
Y(z) = X(z) + X(z)z^{-D}
= X(z)(1+z^{-D})
H(z) = \frac{Y(z)}{X(z)} = 1+z^{-D}

![](img/b54974d0a4317ec82d7ae02126d10a6f_210_0.png)

Figure 7.9: A more useful digital delay incorporates wet and dry controls.

![](img/b54974d0a4317ec82d7ae02126d10a6f_210_1.png)

Figure 7.10: The simplified DDL of D samples delay.

Next, calculate the poles and zeros of the transfer function. We can see that this is a pure feed-forward filter in its current state so there are only zeros. We need to find the roots of the equation for H (z):

0 = 1 + z^{-D}
= z^{D} + 1
z^{D} = -1
Let z = e^{j\omega}
e^{jD\omega} = -1

Apply Euler
cos(D\omega) + j sin(D\omega) = -1

The roots (zeros) of the function lie wherever D\omega causes the equation to evaluate to -1 +j0, and we know this will happen when Equation 7.6 holds true.

cos(\theta) + j sin(\theta) = -1 + j0
if
\theta = \pm \pi, \pm 3\pi, \pm 5\pi, etc...

Notice that both \pm \pi produce the desired result of -1 + j0 as well as all the odd multiples of \pi: \pm 3\pi,

\(\pm 5\pi\), and so on. So the actual solution to find the roots becomes Equation 7.7:

```
cos(Dw) + j sin(Dw) = -1 + j0
if
Dw = \(\pm \pi, \pm 3\pi, \pm 5\pi, ... \pm N\pi\)
until
N > D-1
or
zeros at w = \(\pm \frac{k\pi}{D} k = 1, 3, 5, ..., D\)
```

After N > D - 1, the whole mathematical sequence repeats again, cycling through odd multiples of π. This means that there are D zeros spread equally around the unit circle. This makes sense—the fundamental theorem of algebra predicts D roots for a polynomial of order D. Now consider the simple case of D = 2 samples; we get Equation 7.8:

```
cos(2w) + j sin(2w) = -1
if
w = \(\pm \frac{k\pi}{D} k = 1, 3, 5, ..., D\)
w = \(\pm \frac{\pi}{2}\)
```

There are two zeros, one at +\(\pi\)/2 and the other at -\(\pi\)/2. Plot those on the unit circle in the z-plane and you can see what the frequency response will be, shown in Figure 7.11. You can see from Figure 7.11 that the zeros produce a notch (zero of transmission) at \(\pm\pi\)/2. In fact, when the delay time is very small, your ears hear the effect as a frequency response change; your ears cannot discriminate two samples that are only 23 µs apart as separate echoes. Now consider what would happen if we increase the delay amount to four samples, as in Figure 7.12. Finally, what would happen if the delay is an odd value, like D = 5 (Figure 7.13)?

```
cos(Dw) + j sin(Dw) = -1 + j0
cos(4w) + j sin(4w) = -1 + j0
w = \(\pm \frac{\pi k}{D} k = 1, 3, 5, ..., D\)
w = \(\pm \frac{\pi}{4}, \pm \frac{3\pi}{4}\)
```

![](img/b54974d0a4317ec82d7ae02126d10a6f_211_0.png)

Figure 7.11: The z-plane pole/zero plot and resulting frequency response.

![](img/b54974d0a4317ec82d7ae02126d10a6f_212_0.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_212_1.png)

```
cos(Dω₀) + j sin(Dω₀) = -1 + j0
cos(5ω₀) + j sin(5ω₀) = -1 + j0
ω = ± kπ/5   k = 1, 3, 5, ..., D-1
ω = ± π/5, ± 3π/5, ± 5π/5
ω = ± π/5, ± 3π/5, ± π
```

This kind of frequency response in Figure 7.13 is called inverse comb filtering. As we add more and more samples of delay, we add more and more notches to the response. You can use the built-in module in RackAFX to experiment. Figures 7.14 and 7.15 show the frequency response for 32 samples of delay—it’s an inverse comb filter with 16 zeros in the positive frequency domain.

### 7.2.2 The Effect of Feedback

When you add feedback to the delay, two things happen: first, for long delays your ear will hear discrete repeating echoes that decay away after the signal is removed. As the delay time gets shorter and shorter, the echoes merge, begin to ping, and then the actual filtering (which has been going on all the time) now dominates what you hear.

In Figure 7.16, you can see the effect of feedback on the impulse response. The initial impulse is the one through the dry path, and the next identical-sized one is the first output of the delay line. The echoes decay, being reduced 90% on each trip through the filter. To understand the effect on frequency response, write the transfer function and take the z transform. To make it easier to find the pole frequencies, let the feedback value become 100% or 1.0, as shown in the block diagram in Figure 7.17; even though we know this would result in oscillation, it will make calculating the frequencies easier.
