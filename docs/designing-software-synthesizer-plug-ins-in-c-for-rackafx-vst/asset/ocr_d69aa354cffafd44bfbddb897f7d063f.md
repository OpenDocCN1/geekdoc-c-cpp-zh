These functions decode the oscillator index the same way you saw in OscSineCycleSample, then call member functions or get member values directly.

| Oscillators | LFO | Voice | DigiSynth | EG | Mod |
| --- | --- | --- | --- | --- | --- |
| Osc1 Out | LFO Waveform | Volume | | Attack | LFO Cutoff |
| | | -6.00 dB | | | 7/8 |
| 12.34 | saw | | | | |
| Osc2 Out | LFO Rate | Detune | | | | LFO Pitch In |
| 12.34 | 12.34 | 12.34 | Filter | Filter EG Int |
| Pitch EG Int | | | | | |
| 12.34 | | 12.34 | 12.34 | 12.34 | 12.34 | 12.34 |
| | Octave | | | | DCA EG Int | LFO Pan In |
| sustain | | | | | | |
| loop oneShot | | | 12.34 | 12.34 | 12.34 | 12.34 | www.willpirkle.com

| Oscillators | Filter | EG | LFO | Mod | DCA | Voice |
| --- | --- | --- | --- | --- | --- | --- |
| Osc1 Out | Filter Fc | Attack | LFO Waveform | LFO Cutoff | OSC Mode | Detune | Portamento |
| | | | | | | | Loop Mode |
| 12.34 | 12.34 | 12.34 | | | 12.34 | 12.34 | 12.34 |
| Osc2 Out | Filter Q | DryRelease | LFO Rate | LFO Pitch In | DCA EG Int | |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | | |
| Pitch EG Int | Sustain | LFO Depth | DCA EG Int | | Global |
| | | | | | Vel | Reset Zero | Legato Mode | PBlend Range |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | Note-Day | Filter Key Track | 12.34 |
| Pitch EG Int | | | | | OFF OFF 0.5 |
| 12.34 | | | | | LFO Pan In |

CDiSynthVoiceWithwww.willpirkle.com

# CDiSynthVoice Member Functions

| Function Name | Description |
| --- | --- |
| initGlobalParameters | initialize the globals |
| initializeModMatrix | initialize the modulation matrix |
| setSample | set rate on sub-components |
| prepareForPlay | prepareFor sub-components, one time it |
| update | update voice variables |
| reset | reset voice variables |
| inOscSplitRange | given an oscillator index (0,1,2,3), determine if MIDI note is in its split range |
| inOscVelocityRange | given an oscillator index (0,1,2,3), determine if MIDI velocity is in its velocity range |
| inOscSineCycle | given an oscillator index (0,1,2,3), returns if the oscillator is a single-cycle sample loaded |
| getOscWaveData | given an oscillator index (0,1,2,3), returns the pointer to m_pWaveobject |
| getOscWaveSamplePtr | given an oscillator index (0,1,2,3), returns the pointer to that oscillator's m_pWaveArray object |
| initOscWithPathPath | initialize a CSampleOscillator with a single file |
| initWithFolderPath | initialize a CSampleOscillator with a multi-sample set from a folder |
| initAllWithSynthVoice | shares oscillator wave data pointers with a CDiSynthVoice object |
| doVoice | render the audio

initAllOscWithSynthVoice()

This function clones the wave data from one CDiSynthVoice object into the current object. You copy all pointers