Sources: double CWToscillator::dooscillate(double* pAuxOutput)

+   - filter fc
- filter control (for Filter Key Track, where the fc control value is

```
if(Im_bNoteOn) {
    if(pAuxOutput)
        *pAuxOutput = 0.0;
    return 0.0;
}

// SNIP SNIP SNIP

// get first output
double dOutSample = doWaveTable(m_dReadIndex, m_dWT_inc);

if(m_pModulationMatrix) {
    // write our outputs into their destinations
m_pModulationMatrix->m_dS[m_uModDestOutput1] = dOutSample*m_dAmplitude*m_dAmpMod;

    // add quad phase/stereo output (QBL is mono)
m_pModulationMatrix->m_dS[m_uModDestOutput2] = dOutSample*m_dAmplitude*m_dAmpMod;

    // mono oscillator
    if(pAuxOutput)
        *pAuxOutput = dOutSample*m_dAmplitude*m_dAmpMod;

    return dOutSample*m_dAmplitude*m_dAmpMod;
}
```

overwritten with the MIDI note pitch)
Destinations: