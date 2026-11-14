![](bbox=[0.25, 0.01, 0.75, 0.2])

# Figure 7.8: The delayed sample plus feedback is written into the current write location.

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

# 7.2 Digital Delay with Wet/Dry Mix

Although there may be some instances where you don't need a wet/dry mix, in general when you make a delay plug-in, you still want to hear your unaffected signal. This can be done by using the plug-in as an Auxiliary (AUX) Send effect rather than an insert effect. But, to provide both capabilities, you need to provide the user with a wet/dry ratio control. The block diagram is slightly modified as shown in Figure 7.9.

The difference equation is as follows:

```
y(n) = dry*x(n) + wet*[x(n-D) + fb*y(n-D)] ....................................................(7.2)
```

# 7.2.1 Frequency and Impulse Responses

Consider the basic delay with no feedback applied and with the wet/dry ratio at 1:1. The block diagram and difference equation would then reduce down to Figure 7.10.

The difference equation is as follows:

```
y(n) = x(n) + x(n-D) ............................................................................................(7.3)
```

To find the frequency response, first take the z transform of the difference equation and form the