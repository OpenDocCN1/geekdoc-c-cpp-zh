```
void CMiniSynth::update() // RAFX
void Processor::update() // VST3
{
  // -- update global parameters
  /
  // -- Voice:
  m_GlobalSynthParams.voiceParams.uVoiceMode = m_uVoiceMode;
  m_GlobalSynthParams.voiceParams.dPortamentoTime_mSec = -
      m_dPortamentoTime_mSec;

  // -- ranges
  m_GlobalSynthParams.voiceParams.doscFoPitchModRange = -
      m_nPBendRange;

  // -- intensities
  m_GlobalSynthParams.voiceParams.dFilterKeyIntensity = -
      m_dFilterKeyIntensity;
  m_GlobalSynthParams.voiceParams.dLF01FilterIntensity = -
      m_dLF01FcIntensity;
  m_GlobalSynthParams.voiceParams.dLF01scModIntensity = -
      m_dLF01scPitchIntensity;
  m_GlobalSynthParams.voiceParams.dLF01DCAmpIntensity = -
      m_dLF01AmpIntensity;
  m_GlobalSynthParams.voiceParams.dLF01DCAPanModIntensity = -
      m_dLF01PanIntensity;

  m_GlobalSynthParams.voiceParams.dEG10scModIntensity = -
      m_dEG10scIntensity;
  m_GlobalSynthParams.voiceParams.dEG1FilterModIntensity = -
      m_dEG1FilterIntensity;
  m_GlobalSynthParams.voiceParams.dEG1DCAmpIntensity = -
      m_dEG1DCAIntensity;

  // -- Oscillators:
  double dNoiseAmplitude = m_dNoiseOsc_dB == -96.0 ? 0.0 :
      pow(10.0, m_dNoiseOsc_dB/20.0);
```