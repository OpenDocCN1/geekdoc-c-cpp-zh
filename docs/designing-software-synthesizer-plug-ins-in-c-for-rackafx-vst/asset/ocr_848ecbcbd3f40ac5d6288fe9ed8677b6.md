# recalculate release
time (explained)
Chapter 8

```
CEnvelopeGenerator::CEnvelopeGenerator(void)
// defaults
m_dSampleRate = 44100;
m_dAttackTime_mSec = EG_DEFAULT_STATE_TIME;
m_dDecayTime_mSec = EG_DEFAULT_STATE_TIME;
m_dReleaseTime_mSec = EG_DEFAULT_STATE_TIME;
m_dSustainLevel = 1.0;
m_dEnvelopeOutput = 0.0;
m_dIncShutdown = 0.0;

// -- user normally not allowed to set the time
d_dShutdownTime_mSec = 10.0; // mSec
```

if reset to zero is
enabled, clear the
out variable

# calculateAttackTime()

+   - calculate the iterative
exponential variables
for exponential attack
output

# calculateDecayTime()

+   - calculate the iterative
exponential variables
for exponential decay
output

```
// -- states and flags
m_uState = off;
m_bOutputEG = false;
m_uEGMode = analog;
setEGMode(m_uEGMode);
m_bResetToZero = false;
m_bLegatoMode = false;
```

# calculateReleaseTime()

+   - calculate the iterative exponential variables for exponential release output

# noteOff ()

+   - MIDI note events will trigger the output EGs to go into note off mode; this means jumping directly to the
release state as Figure 6.27

# shutDown()

+   - if the sustain level was set to 0.0 and had reached that point, just go to shut off state

+   - ignore in legato
mode; we want the
EG to stay in its state