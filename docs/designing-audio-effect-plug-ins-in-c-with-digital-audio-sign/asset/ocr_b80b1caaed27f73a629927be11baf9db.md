```
bool _stdcall CWTOscillator::userInterfaceChange(int nControlIndex)
{
    // add your code here
    switch(nControlIndex)
    {
    case 0:
        cookFrequency();
        break;

    // note on
    case 50:
        reset();
        cookFrequency();
        m_bNoteOn = true;
        break;

    // note off
    case 51:
        m_bNoteOn = false;
        break;

    default:
        break;
    }
    return true;
}
```

# processAudioFrame()

+   - Implement the table look up.
+   - Notice that as with the delay line, we shift the frame of reference of the interpolated points to be between n = 0 and n = 1, then just use the frac component to find the value between the samples.

```
bool _stdcall CWTOscillator::processAudioFrame(float* pInputBuffer, float* pOutputBuffer, UINT uNumInputChannels, UINT uNumOutputChannels)
{
    // Do LEFT (MONO) Channel
    // if not running, write 0s and bail
    if(!m_bNoteOn)
    {
        pOutputBuffer[0] = 0.0;

        // Mono-In, Stereo-Out (AUX Effect)
        if(uNumInputChannels == 1 && uNumOutputChannels == 2)
            pOutputBuffer[1] = 0.0;

        // Stereo-In, Stereo-Out (INSERT Effect)
        if(uNumInputChannels == 2 && uNumOutputChannels == 2)
            pOutputBuffer[1] = 0.0;

        return true;
    }

    // our output value for this cycle
    float fOutputSample = 0;

    // get INT part
    int nReadIndex = (int)m_fReadIndex;

    // get FRAC part
    float fFrac = m_fReadIndex - nReadIndex;
```