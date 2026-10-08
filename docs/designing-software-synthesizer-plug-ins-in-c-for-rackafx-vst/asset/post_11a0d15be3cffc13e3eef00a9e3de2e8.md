
```cpp
// --- PORTAMENTO BLOCK -- //
if(m_dPortamentoInc > 0.0 && m_p0sc1->m_d0scFo = m_d0scPitch)
{
    // --- modulo wrapped, portamento is done
    if(m_dModuloPortamento >= 1.0)
    {
      // --- reset
      m_dModuloPortamento = 0.0;

      // target pitch has now been hit
      if(m_p0sc1) m_p0sc1->m_d0scFo = m_d0scPitch;
      if(m_p0sc2) m_p0sc2->m_d0scFo = m_d0scPitch;
      if(m_p0sc3) m_p0sc3->m_d0scFo = m_d0scPitch;
      if(m_p0sc4) m_p0sc4->m_d0scFo = m_d0scPitch;
    }
}
else
{
    // --- calculate current glide pitch
    double dPortamentoStart*PitchShiftMultiplier,
          (m_dModuloPortamento*m_dPortamentoSemitones);

    // --- set in oscillators
    if(m_p0sc1) m_p0sc1->m_d0scFo = dPortamentoPitch;
    if(m_p0sc2) m_p0sc2->m_d0scFo = dPortamentoPitch;
    if(m_p0sc3) m_p0sc3->m_d0scFo = dPortamentoPitch;
    if(m_p0sc4) m_p0sc4->m_d0scFo = dPortamentoPitch;

    // --- inc the portamento modulo
    m_dModuloPortamento += m_dPortamentoInc;

    }
}
    // --- if we make it here, we are rendering
    return true;
}
```

especially if you remove the intensity controls to make room for others.

# MiniSynth Modulation Matrix

| Source | Destination/Intensity | Transform/Range | enabled |
| --- | --- | --- | --- |
| SOURCE_LFO1 | DEST_ALL_OSC_FO<br>dLFO10OscModulation | TRANSFORM_NONE<br>dOscFoModRange | TRUE |
| SOURCE_BIASED_EG1 | DEST_ALL_FILTER_FC<br>dEG1FilterModulation | TRANSFORM_NONE<br>dFilterRange | TRUE |
| SOURCE_EG1 | DEST_DCA_EG<br>dEG10OscModulation | TRANSFORM_NONE<br>m_dVarModRange | TRUE |
| SOURCE_BIASED_EG1 | DEST_ALL_OSC_FO<br>dEG10OscModulation | TRANSFORM_NONE<br>dOscFoModRange | TRUE |
| SOURCE_LFO1 | DEST_ALL_FILTER_FC<br>dLFO1FilterModulation | TRANSFORM_NONE<br>dFilterModRange | TRUE |
| SOURCE_LFO1 | DEST_ALL_OSC_PULSEWIDTH<br>m_dDefaultModulation | TRANSFORM_NONE<br>m_dDefaultModRange | TRUE |
| SOURCE_L1 | DEST_DCA_AMP<br>dLFO1DCampModulation | TRANSFORM_BIPO-<br>LAR_TO_UNIPOLAR<br>dAmpModRange | TRUE |
| SOURCE_LFO1 | DEST_DCA_PAN<br>dLFO1DCampModulation | TRANSFORM_NONE<br>m_dDefaultModRange | TRUE |

# MiniSynth Continuous Parameters

| Control Name (units) | Type | Variable Name (VST3, RAFX) | Low/Hi/Default * | VST3/AU Index |
| --- | --- | --- | --- | --- |
| Noise Osc (db) | double | m_NoiseOsc_dB | -96 / 0 | NOISE_AMP_DB |
| Sub Osc (db) | double | m_SubOsc_dB | -96 / 0 | SUB_OSC_AMP |
| Pulse Width (%) | double | m_PulseWidth_Pct | 1 / 99 | PULSE_WIDTH_PCT |
| Osc EG Int | double | m_dEG1Intensity | -1 / 0 / 1 | EG1_TO_OSC_INTENSITY |
| Filter Fc (Hz) | double | m_dfFcControl | 80 / 16000 | FILTER_FC |
| Filter Q | double | m_dQControl | 1 / 10 | FILTER_Q |
| Filter EG Int | double | m_dEG1FilterIntensity | -1 / 0 | EG1_FILTER_INTENSITY |
| Key Track Int | double | m_dFilterKeyTrackInintensity | 0.5 / 1 / 10 | EG1_KEYTRACK_INTENSITY |
| Attack (ms) | double | m_attackTime_ms | 0 / 5000 / 100 | EG1_ATTACK_MSE |
| Decay/ Release (ms) | double | m_dDecayReleaseTime_ms | 1 / 1000 | EG1_DECAY_RELEASE_MSE |
| Sustain | double | m_dSustainLevel | 0 / 0.1 / 707 | EG1_SUSTAIN_LEVEL |
| LFO Rate | double | m_dLFO1Rate | 0.0 / 20 / 0.5 | LFO_RATE |
| LFO Depth | double | m_dLFO1Amplitude | -1 / 1 / 0 | LFO_AMPLITUDE |
| LFO Cutoff Int | double | m_dLFO1FilterIntensity | -1 / 1 / 0 | LFO_TO_FILTER_INTENSITY |
| LFO Pitch Int | double | m_dLFO1OscIntensity | -1 / 1 / 0 | LFO1_TO_OSC_INTENSITY |
| LFO Amp Int | double | m_dLFO1Amplintensity | 0 / 1 / 0 | LFO1_TO_DCA_INTENSITY |

```
initializeModMatrix()
```

In this function, you program the modulation using Table 9 to create the rows which you always call the base class.

LFO Pan Int double m_LFOPanintensity 0 / 1 / 0 | LFO_TO_PAN_INTENSITY
Volume double m_Volume_DB -96 / 20 | OUTPUT_AMPLITUDE
DCA EG Int double m_dEG1DCAIntensity -1 / 1 / 1 | EG1_TO_DCA_INTENSITY
Detune double m_Detune_counts -100 / 100 / 0 | DETUNE_COUNTS
Portamento double m_dPortamentoTime_Msec 0 / 5000 / 0 | PORTAMENTO_TIME_MSE
Octave double m_Octave -4 / 4 / 0 | OCTAVE
PBendRange double m_PBendRange 0 / 12 / 0 | PITCHBEND_RANGE

Low, high and default values are defined for VST and AU in SynthParam.h for each project.

# MiniSynth Enumerated Strings (UINT)

| Control Name | Variable Name | enum String | VST3/AU Index |
| --- | --- | --- | --- |
| LFO Waveform | m_LFOWaveform | sine, saw, square, expo, rush | LFO_WAVEFORM |
| Voice Mode | m_uVoiceMode | Saw3, Saw2sq, Tr2Saw, Tr2sq | VOICE_MODE |
| Vel+Att Scale | m_uVelocityToAttack | OFF | VELOCITY_TO_ATTACK |
| Note+Dec Scale | m_uNumberToDecScale | OFF | NOTE_TO_DECA |
| Reset to Zero | m_uResetToZero | OFF | RESET_TO_ZERO |
| Filter Key | m_uFilterKey | OFF | FILTER_KEY |
| Legato Mode | m_uLegatoMode | OFF | LEGATO_MODE |

# setSampleRate()

Just call the base class implementation.

# prepareForPlay()

In prepareForPlay() you just call the base class then reset.

# update()

The update() function is important for MiniSynth because this is where you configure the oscillators based on the voice mode. Notice the voice mode is saved before calling the base class function that will overwrite it (this is the only time that happens in any of the objects). If the voice mode has changed, you configure the oscillator types. After configuring, you call reset() on the oscillators; we must preserve the phase relationship between different waveforms, and that is done in reset(). How do you use the global parameters to update the oscillator waveforms.

# MiniSynthVoice::MiniSynthVoice(void)

```cpp
// 1) -- declare your oscillators and filters
// oscillators
m_posc1 = &m_osc1;
m_posc2 = &m_osc2;
m_posc3 = &m_osc3;
m_posc4 = &m_osc4;
```

| Oscillators | Voice | Filter | EG | Mod |
| --- | --- | --- | --- | --- |
| Noise Osc LFO Waveform | Volume | Attack LFO Cutoff | | |
| | | -6 to 0 db | 1/8 | |
| | | 12.34 | 12.34 | |
| Pulse Width LFO Rate | Detune | | | |
| | | 12.34 | 12.34 | |
| Sub Osc LFO Depth | Portamento | Filter C | Filter EG Int | |
| | | 12.34 | 12.34 | 12.34 | 12.34 |
| Pitch EG Octave | | Sustain | EG LFO Oct | |
| | | 12.34 | 12.34 | 12.34 | 12.34 |
| | | will.pirinkle.com | LFO Pan Int | |
| | | 12.34 | 12.34 | |

# reset()

reset() you just call the base class first, then configure the oscillator types and zero the portamento time.

# doVoice()

This is the most important function of all since it implements the rendering, and it is nearly identical to NanoSynth's rendering code. The modulation layers are the same, the only difference is in the wiring of the audio engine. Notice the call to the base class and the scale-before-summing on the pitched oscillators in the audio engine. The articulation block is nearly identical to NanoSynth because the programming is done in the modulation matrix. The only difference is the call to voice object's update after modulation Layer 1, but before updating the rest of the components.
