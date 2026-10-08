```
ComponentResult AUSynth::Initialize()
{
    // --- init the base class
    AUInstrumentBase::Initialize();

    // --- inits
    m_Osc1.setSampleRate(GetOutput(0)->GetStreamFormat().mSampleRate);
    m_Osc2.setSampleRate(GetOutput(0)->GetStreamFormat().mSampleRate);
    m_Osc2.m_nCents = 2.5; // +2.5 cents detuned

    m_LF01.setSampleRate(GetOutput(0)->GetStreamFormat().mSampleRate);

    // --- init the synth
    update();

    return noErr;
}

void AUSynth::update()
{
    // --- oscillators
    m_Osc1.m_uWaveform = Globals()->GetParameter(OSC_WAVEFORM);
    m_Osc2.m_uWaveform = Globals()->GetParameter(OSC_WAVEFORM);
    m_Osc1.update();
    m_Osc2.update();

    // --- LFO
    m_LF01.m_uWaveform = Globals()->GetParameter(LF01_WAVEFORM);
    m_LF01.m_dAmplitude = Globals()->GetParameter(LF01_AMPLITUDE);
    m_LF01.m_dOscFo = Globals()->GetParameter(LF01_RATE);
    m_LF01.m_uFOMode = Globals()->GetParameter(LF01_MODE);
    m_LF01.update();
}
```