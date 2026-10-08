```
inline doubleEnvelope(double* p8iasedOutput = NULL)
{
  // --- decode the state
  switch(m_uState)
  {
    <SNIP SNIP SNIP>
    case release:
      // --- if sustain pedal is down, override and return
      if(m_bSustainOverride)
      {
        m_dEnvelopeOutput = m_dSustainLevel;
        break;
      }
      else
        // --- render value
        m_dEnvelopeOutput = m_dReleaseOffset +
        m_dEnvelopeOutput*m_dReleaseCoeff;

        // --- check go to next state
        if(m_dEnvelopeOutput <= 0.0 || m_dReleaseTime_mSec <= 0.0)
        {
          m_dEnvelopeOutput = 0.0;
          m_uState = off; // go to next state
          break;
        }
  }
}
etc...
```

# StartNote()

+   - Velocity
- (already have MIDI note number from previous project)

# HandlePitchWheel()

+   - Pitch Bend

# HandleControlChange()