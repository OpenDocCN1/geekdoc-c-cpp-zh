Notice that everything except the envelope detectors is straight from your last project.

# 12.5.4 EnvelopeFollower.cpp File

# Constructor

+   • Initialize the rate min and max values. The member-objects are self initializing upon creation.

```
CEnvelopeFollower::CEnvelopeFollower()
{
    <SNIP SNIP SNIP>
    // Finish initializations here
    // set our Min and Max Modulation points
    m_fMinCutoffFreq = 100.0;
    m_fMaxCutoffFreq = 5000.0;
}
```

Write the calculateCutoffFrequency() function. It is similar to the previous modulation functions except that we will allow both up and down directions of modulation. Can you figure out how the code works?

```
float CEnvelopeFollower::calculateCutoffFreq(float fEnvelopeSample)
{
    // modulate from min upwards
    if(m_uDirection == UP)
        return fEnvelopeSample*(m_fMaxCutoffFreq - m_fMinCutoffFreq) +
               m_fMinCutoffFreq;
    else // modulate from max downwards
        return m_fMaxCutoffFreq - fEnvelopeSample*(m_fMaxCutoffFreq -
               m_fMinCutoffFreq);
    return m_fMinCutoffFreq;
}
```

Write the cooking functions for the LPFs to set the new coefficients for a given $f_c$ and $Q$ value. This is identical to the ModFilter project.

```
void CEnvelopeFollower::calculateLPFCoeffs(float fCutoffFreq, float fQ, CBiquad*
    pFilter)
{
    /* use same code as the Mod Filter */
}
```

# prepareForPlay()

+   • Flush delays in LPFs.
+   • Initialize the detector objects.