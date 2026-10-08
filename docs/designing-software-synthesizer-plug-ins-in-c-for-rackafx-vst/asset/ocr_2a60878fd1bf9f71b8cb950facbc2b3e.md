Next, open the NanoSynth files and modify the following to implement the rest of the synth.

# NanoSynth.h

In the .h file, we need to #include the member objects and declare them. We'll start with the QBLLimitedOscillators first.

```
if(m_uWaveform == SINE)
  return -1;

double dSeedFreq = 27.5; // Note A0, bottom of the page
for(int j = 0; j < NUM_TABLES; j++) {
  if(m_dFo <= dSeedFreq) {
    return j;
  }
```

# NanoSynth.cpp

Start at the top of the file and work your way through the RackAFX functions:

```
dSeedFreq *= 2.0;
  return -1;
```

# Constructor:

+   - set the flag to void CWTOscillator::selectTable()

```
m_nCurrentTableIndex = getTableIndex();

// if the frequency is high enough, the sine table will be returned
// even for non-sinusoidal waves; anything about 10548 Hz is one
// harmonic harmonic only (sine)
if(m_nCurrentTableIndex < 0) {
  m_pCurrentTable = &m_dSTable[0];
  return;
}
```

+   - choose table
if(m_uWaveform == SAW1 || m_uWaveform == SAW2 || m_uWaveform == SAW3 || m_uWaveform == SQUARE)
  m_pCurrentTable = m_pSawTables[m_nCurrentTableIndex];
else if(m_uWaveform == TRI)
  m_pCurrentTable = m_pTriangleTables[m_nCurrentTableIndex];

+   - capture all MIDI and set the MIDI channel (which has changed since the last NanoSynth, so there is nothing to do here)

```
inline void checkWrapIndex(double& dIndex) {
  while(dIndex < 0.0)
    dIndex += WT_LENGTH;
```

# prepareForPlay()

Implement the one time initialization code to: