```
// --- reset the base class
AUBase::Reset(inscope, inElement);

// --- pFP creates and flushes the delay
m_DelayFX.prepareForPlay(GetOutput(0)->GetStreamFormat().mSampleRate);

for(int i=0; i<MAX_VOICES; i++) {
    CMiniSynthVoice* pVoice = m_pVoiceArray[i];
    pVoice->setSampleRate(GetOutput(0)->GetStreamFormat().mSampleRate);
    pVoice->prepareForPlay();
}

// mass update
update();

// clear
m_dLastNoteFrequency = -1.0;

return noErr;
}

ComponentResult ASynth::Initialize() {
    // --- init the base class
    AUInstrumentBase::Initialize();

    // --- pFP creates and flushes the delay
    m_DelayFX.prepareForPlay(GetOutput(0)->GetStreamFormat().mSampleRate);

    for(int i=0; i<MAX_VOICES; i++) {
        CMiniSynthVoice* pVoice = m_pVoiceArray[i];
        pVoice->setSampleRate(GetOutput(0)->GetStreamFormat().mSampleRate);
        pVoice->prepareForPlay();
    }
}
```