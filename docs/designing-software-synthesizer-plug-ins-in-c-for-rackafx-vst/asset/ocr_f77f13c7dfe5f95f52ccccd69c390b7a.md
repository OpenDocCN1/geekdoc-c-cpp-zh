# 11.21 AniSynth,

RackAFX, VST3, and AU Create the AniSynth project using VectorSynth as a starting point—the GUI controls are identical. Substitute the new loadSamples() function for the original function and change all references to

```
bool AniSynth::createOscillatorArray(int nCellsPerSide) {
    // --- delete if existing
    if(m_ppOscArray) {
        // --- size
        int nArraySize = pow(m_nCellsPerSide + 1.0, 2.0);
        for(int i=0; i<nArraySize; i++)
            delete m_ppOscArray[i];
    }

    // --- size (use argument)
    int nArraySize = pow(nCellsPerSide + 1.0, 2.0);

    // --- create new array of pointers
    m_ppOscArray = new CSampleOscillator[nArraySize];

    // --- validate
    if(!m_ppOscArray)return false;

    // --- load up with new oscillator pointers
    for (int i=0; i<nArraySize; i++)
        m_ppOscArray[i] = new CSampleOscillator();

    // --- store for later
    m_nCellsPerSide = nCellsPerSide;
    m_nCells = pow(m_nCellsPerSide, 2.0);

    return true;
}
```

CVectorSynthVoice to CAniSynthVoice in the plug-in object. Do not delete or modify CSynthVoice since