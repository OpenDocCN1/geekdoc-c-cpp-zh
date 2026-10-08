```
// --- Voice params
m_pGlobalVoiceParams = &pGlobal->voiceParams;
m_pGlobalVoiceParams->uVoiceMode = m_uVoiceMode;
m_pGlobalVoiceParams->dHSRatio = m_dHSRatio;
m_pGlobalVoiceParams->dPortamentoTime_mSec = =
m_dPortamentoTime_mSec;
```

```
// --- Range Variables
m_pGlobalVoiceParams->dOscFoPitchBendRange = OSC_PITCHB_END_MOD_RANGE;
m_pGlobalVoiceParams->dOscFcoModRange = OSC_FO_MOD_RANGE;
m_pGlobalVoiceParams->dOscHardSyncModRange = OSC_HARD_SYNC_RANGE;
m_pGlobalVoiceParams->dFilterModRange = FILTER_FC_MOD_RANGE;
m_pGlobalVoiceParams->dAmpModRange = AMP_MOD_RANGE;
```

```
// --- Intensity variables
m_pGlobalVoiceParams->dFilterKeyTrackIntensity = 1.0;

// --- init sub-components
if(m_p0sc1)m_p0sc1->initGlobalParameters(&m_pGlobalSynthParams->-osc1Params);
if(m_p0sc2)m_p0sc2->initGlobalParameters(&m_pGlobalSynthParams->-osc2Params);
if(m_p0sc3)m_p0sc3->initGlobalParameters(&m_pGlobalSynthParams->-osc3Params);
if(m_p0sc4)m_p0sc4->initGlobalParameters(&m_pGlobalSynthParams->-osc4Params);
```

etc. ..

```
void setModMatrixCore(modMatrixRow** pModMatrix)
{
    _ModulationMatrix.setModMatrixCore(pModMatrix);
}
```

articulation and audio engine implementations.

# 9.4 MiniSynth Specifications

The CMiniSynth derived class won't make sense until you understand the deeper specifications for MiniSynth. Specifically, we need to address the voice modes of MiniSynth. You will remember from the block diagram in Figure 9.1 that there are four oscillators. One oscillator always plays the sub-octave (OSC 3) while another is a noise oscillator (OSC4). However, there are multiple waveform modes of operation. This idea was taken from Volka Keys; it cleverly uses UI controls by presenting the user with a pre-set list