```
bool __stdcall CDirectOscillator::processAudioFrame(float* pInputBuffer, float*
pOutputBuffer, UINT uNumChannels()
{
    //
    // output - input -- change this for meaningful processing
    //
    // Do LEFT (MONO) Channel
    //
    // if not running, write 0s and bail
    if(!m_bRunOscillator)
    {
        // zero it all out
        pOutputBuffer[0] = 0.0;

        // Mono-In, Stereo-Out (AUX Effect)
        if(uNumInputChannels == 1 && uNumOutputChannels == 2)
            pOutputBuffer[1] = 0.0;

        // Stereo-In, Stereo-Out (INSERT Effect)
        if(uNumInputChannels == 2 && uNumOutputChannels == 2)
            pOutputBuffer[1] = 0.0;

    }
    return true;

    // otherwise, do the oscillator
    // do difference equation y(n) = -b1y(n-2) - b2y(n-2)
    pOutputBuffer[0] = m_f_b1*m_f_y_z1 - m_f_b2*m_f_y_z2;

    // Mono-In, Stereo-Out (AUX Effect)
    if(uNumInputChannels == 1 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pOutputBuffer[0];

    // Stereo-In, Stereo-Out (INSERT Effect)
    if(uNumInputChannels == 2 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pOutputBuffer[0];

    // shuffle memory
    m_f_y_z2 = m_f_y_z1;
    m_f_y_z1 = pOutputBuffer[0];

    return true;
}
```

# userInterfaceChange()

+   - Call the frequency cooking function and implement the start and stop functions.
+   - Make sure your nControlIndex values match your switch/case statement.