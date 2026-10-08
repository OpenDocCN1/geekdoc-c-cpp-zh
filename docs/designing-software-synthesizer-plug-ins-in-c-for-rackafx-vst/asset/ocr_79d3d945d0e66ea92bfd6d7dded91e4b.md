# CminiSynthMember Variables

| Type | Variable Name | Description |
| --- | --- | --- |
| QBLimitedOscillator | m_Osc1 | Oscillator 1 |
| QBLimitedOscillator | m_Osc2 | Oscillator 2 |
| QBLimitedOscillator | m_Osc3 | Oscillator 3 (sub) |
| QBLimitedOscillator | m_Osc4 | Oscillator 4 (noise) |
| CMogLadderFilter | m_MoogLadderFilter | Low Pass Filter |
| UINT | m_uOscForRatio | hard sync; ratio index in mod matrix |
| enum | Saw3,Sqr3,Saw2,Sqr2,TriSaw,Tri2 | voice mode strings repeated here for easier coding |

# CminiSynthVoiceMember Functions

| Function Name | Description |
| --- | --- |
| initGlobalParameters | sets all sub-components with their global parameter structures |
| initializeModMatrix | sets all voice modulation routines |
| setSampleRate | distributes sample rate to all sub-components |
| prepareForPlay | one-time initialization; occurs after sub-component pointers have been set (i.e., post construction of derived classes) |
| update | update new voice parameters |
| reset | reset all sub-components |
| doVoice | performs MiniSynth specific rendering |

```
// --- filters
m_pFilter1 = &m_MoogLadderFilter;
m_pFilter2 = NULL;

// --- experiment with NLP
m_MoogLadderFilter.m_uUNLP = OFF;
// --- for passband gain comp in MoOG; can make user adjustable
m_MoogLadderFilter.m_dAuxControl = 0.75;

// --- voice mode 0
m_osc1.m_Uwaveform = SAW1;
m_osc2.m_Uwaveform = SAW1;
m_osc3.m_Uwaveform = SAW1;
m_osc4.m_Uwaveform = NOISE;

// 2) --- set any component specific stuff
m_EG1.setEGMode(analog);
m_EG1.m_bOutputEG = true; // --- our DCA EG

// --- DCA Setup: set the source EG here
m_DCA.m_uModSourceEG = DEST_DCA_EG;
```

+   * when a note is turned on, the voice object sets m_uTimeStamp to zero