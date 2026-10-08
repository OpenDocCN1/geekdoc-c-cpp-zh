Here we simply implement the note on the last section. You can keep or delete the MIDI logging code as you wish.

```
double dPWIndex = m_dPulseWidth/100.0;
double dPWIndex = m_dReadIndex + dPW*WT_LENGTH;

// --- render first sawtooth using dReadIndex
double dSawl = doWaveTable(m_dReadIndex, m_dWT_inc);

// --- find the phase shifted output
if(m_dWT_inc >= 0)
{
    if(dPWIndex >= WT_LENGTH)
        dPWIndex = dPWIndex - WT_LENGTH;
}
else
{
    if(dPWIndex < 0)
        dPWIndex = WT_LENGTH + dPWIndex;
}
// --- render second sawtooth using dPWIndex (shifted)
double dSaw2 = doWaveTable(dPWIndex, m_dWT_inc);

// --- find the correction factor from the table
double dSqAmp = m_squareCorrFactor[m_nCurrentTableIndex];

// --- subtract
double dOut = dSqAmp*(dSawl - dSaw2);

// --- calculate the DC correction factor
double dCorr = 1.0/dPW;
if(dPW < 0.5)
    dCorr = 1.0/(1.0-dPW);

// --- apply correction
dOut *= dCorr;

return dOut;
```

midiNoteOff() *