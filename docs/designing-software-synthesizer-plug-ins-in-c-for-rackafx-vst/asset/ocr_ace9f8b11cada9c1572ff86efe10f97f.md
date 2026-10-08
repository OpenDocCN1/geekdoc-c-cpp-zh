```
// --- set public attributes on objects
//
// --- Oscillators
m_Voices[i].m_Osc1.m_uWaveform = m_u0scWaveform;
m_Voices[i].m_Osc2.m_uWaveform = m_u0scWaveform;

// --- Filter
m_Voices[i].m_Filter1.m_dFcControl = m_dFcControl;
m_Voices[i].m_Filter1.m_dQControl = m_dQControl;

// --- LFO
m_Voices[i].m_LF01.m_uWaveform = m_uLF01Waveform;
m_Voices[i].m_LF01.m_dAmplitude = m_dLF01Amplitude;
m_Voices[i].m_LF01.m_d0scFo = m_dSustainLevel;
m_Voices[i].m_LF01.m_uLFOMode = m_uLF01Mode;

// --- EG1
m_Voices[i].m_EG1.setAttackTime_mSec(m_dAttackTime_mSec);
m_Voices[i].m_EG1.setDecayTime_mSec(m_dDecayTime_mSec);
m_Voices[i].m_EG1.setSustainLevel(m_dSustainLevel);
m_Voices[i].m_EG1.setReleaseTime_mSec(m_dReleaseTime_mSec);
m_Voices[i].m_EG1.bResetToZero = (bool)m_uResetToZero;
m_Voices[i].m_EG1.bLegatoMode = (bool)m_uLegatoMode;

// --- DCA
m_Voices[i].m_DCA.setPanControl(m_dPanControl);
m_Voices[i].m_DCA.setAmplitude_dB(m_dVolume_dB);

<< END ** Code Listing 8.11: Global Parameter Update ** << END >>

// --- mod matrix stuff (same as before)
if(m_uFilterKeyTrack == 1)
```