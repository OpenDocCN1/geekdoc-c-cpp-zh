- for pitched oscillators, we implement the phase modulation in the doOscillate() function by adjusting the current module counter value based on the phase modulation then checking for wrap—we will discuss this in Chapter 12

- the sinusoidal approximation is identical to the LFO

- notice pass-by-pointer mechanism for triangle so the DPW z -1 register is updated (see algorithm)

- the triangle wave has to handle the module incremented twice (see algorithm)

- as with the LFO, the output value is based on the current amplitude and amp modulation values

- for doOscillate() on pitched oscillators, the prototype is:

| COscillator | Abstract Base Class |
|---|---|
| CQBLimitedOscillator COscillator | Class |
| Methods | Variables |
| CQBLimitedOscillator - CQBLimitedOscillator | |
| doSawtooth | |
| doSquare | |
| doTriangle | |
| reset | |
| startOscillator | |
| stopOscillator | |
| doOscillate |

```
void CQBLimitedOscillator::reset() {
// --- saw/tri starts at 0.5
if(m_uWaveform == SAW1 || m_uWaveform == SAW2 ||
    m_uWaveform == SAW3 || m_uWaveform == TRI)
{
    m_dModulo = 0.5;
}
```

```
void CQBLimitedOscillator::startOscillator() {
    reset();
    m_bNoteOn = true;
}
```

```
void CQBLimitedOscillator::stopOscillator() {
    m_bNoteOn = false;
}
```

virtual inline double doOscillate(double* pAuxOutput = NULL