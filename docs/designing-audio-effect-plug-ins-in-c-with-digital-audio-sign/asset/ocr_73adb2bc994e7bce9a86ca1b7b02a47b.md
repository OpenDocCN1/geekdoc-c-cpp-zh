![](bbox=[0.21, 0.01, 0.79, 0.34])

# Figure 12.14: The flowchart for the left channel of the envelope follower (right channel is same).

```
// do the BiQuads
pOutputBuffer[0] = m_LeftLPF.doBiQuad(pInputBuffer[0]);

// detect the other channel
float fDetectRight = m_RightDetector.detect(fGain*pInputBuffer[1]);

// set mod freq to minimum (un-triggered)
float fModFreqRight = m_fMinCutoffFreq;

// if threshold triggered, calculate new LPF cutoff
if(fDetectRight > m_fThreshhold)
{
    fModFreqRight = calculateCutoffFreq(fDetectRight);
}

// use the mod freq and user supplied-0 to calc the fc
calculateLPFCoeffs(fModFreqRight, m_f0, &m_RightLPF);

// Mono-In, Stereo-Out (AUX Effect)
if(uNumInputChannels -- 1 && uNumOutputChannels -- 2)
{
    pOutputBuffer[1] = pOutputBuffer[0];
}

// Stereo-In, Stereo-Out (INSERT Effect)
if(uNumInputChannels -- 2 && uNumOutputChannels -- 2)
{
    pOutputBuffer[1] = m_RightLPF.doBiQuad(pInputBuffer[1]);
}

return true;
}
```

Build and test the plug-in. Try all the controls. Note: Beware—because of the high pre-gain values possible combined with high-Q values, you can easily overload the audio. If you hear distortion, adjust the pre-gain value. Test this out with guitar, keyboard, or drum loops. Ideas for more plug-ins include:

+   * Change the filter type (high-pass filter, band-stop filter, band-pass filter).
+   * Modulate the Q in the same direction, or opposite direction, as the $f_c$.