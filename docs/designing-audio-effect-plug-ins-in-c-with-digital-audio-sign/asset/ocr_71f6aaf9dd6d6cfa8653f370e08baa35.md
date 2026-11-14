we locate the read index to be two samples before the write pointer because we cast the value to an integer, stripping out the fractional part. The actual delay we really want is 0.4 samples between the current sample and the one before it. In other words, x (n – 2.4) rather than x (n – 2). You can see that we need a sample that is between x (n – 2) and x (n – 3); in Figure 7.28 it happens to be a distance of 0.4 between them.

We need to modify our code as follows:

+   - We are already calculating and updating the first sample that we need to interpolate; it is located with the index value at m_nReadIndex, so there is nothing to change in the cooking function.
+   - In the processAudioFrame() function, we need to interpolate between our current read location m_nReadIndex and the location just *before* it in the buffer, m_nReadIndex-1.
+   - Since we are only focused on a single pair of samples at any time and we know they are one sample apart, we can use the values 0 and 1 for the interpolation function as x1 = 0, x2 = 1; then we interpolate the fractional distance between them. You can use m_nReadIndex but you will get in trouble when you are interpolating across the wrap boundary of the buffer.
+   - We will need to check for a wrap condition backward if m_nReadIndex–1 takes us outside the top of the buffer.

We can get the fractional value from our m_fDelayInSamples in several ways; here is one of them:

```
float fFracDelay = m_fDelayInSamples – (int)m_fDelayInSamples
```

![](bbox=[0.38, 0.47, 0.62, 0.68])

# Figure 7.28: Fractional interpolation.

It really only comes down to locating the sample 1 behind our current read index, then using the linear interpolation code to get the fractional value. There are two extreme conditions to consider:

+   - At the maximum delay time, the read and write indices will be equal and the fractional part of the delay in samples will be 0 so no interpolation will occur—this is OK.
+   - If the delay in samples is less than 1, the read and write indices will also be equal, but this will be a problem. In this case, we need to interpolate between the current x(n) and the sample at x(n – 1), one sample behind the read location. Branching will be necessary to catch this event and handle it.

# 7.5.1 DDLModule.cpp File