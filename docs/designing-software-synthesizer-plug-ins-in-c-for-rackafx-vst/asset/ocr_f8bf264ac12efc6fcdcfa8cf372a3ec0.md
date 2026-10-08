```
void CDelayLine::cookVariables()
{
    // --- calculate fractional delay
    m_dDelayInSamples = m_dDelay_ms*((double)m_nSampleRate/1000.0);

    // --- subtract to read index
    m_nReadIndex = m_nWriteIndex - (int)m_dDelayInSamples;

    // --- the check and wrap BACKWARDS if the index is negative
    if(m_nReadIndex < 0)
        m_nReadIndex += m_nBufferSize; // amount of wrap is Read + Delay
}
```

# readDelay()

This function finds the two samples that surround the interpolated value we desire based on the fractional delay in samples. Then, the two samples are fetched and the interpolation is applied following Figure 13.4. Notice how the fractional component is extracted from the total delay value by subtracting ofthe integer part.

```
double CDelayLine::readDelay()
{
    // -- Read the output of the delay at m_nReadIndex
    double yn = m_pBuffer[m_nReadIndex];

    // -- Read the location ONE BEHIND at y(n-1)
    int nReadIndex_1 = m_nReadIndex - 1;
    if(nReadIndex_1 < 0)
        nReadIndex_1 = m_nBufferSize-1;

    // -- get y(n-1)
    double yn_1 = m_pBuffer[nReadIndex_1];

    // -- get fractional component
    double dFracDelay = m_dDelayInSamples - (int)m_dDelayInSamples;

    // -- interpolate: (0, yn) and (1, yn_1) by FracDelay
    return dLInterp(0, 1, yn, yn_1, dFracDelay);
}
```

# readDelayAt()

Similar to readDelay(), but reads from any arbitrary location in the buffer. It must calculate its own read index values