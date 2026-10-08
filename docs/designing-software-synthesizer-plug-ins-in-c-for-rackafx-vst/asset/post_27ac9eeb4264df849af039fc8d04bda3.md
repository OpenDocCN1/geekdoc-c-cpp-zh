
# MIDI Note On

During the note on event, you first try to find a free voice; if a free voice can be found, you increment the timestamps then call the voice's noteOn() function. If no free voices are found, you set the bStealNote flag for the next if(). You use the helper function to find the proper note to steal, then follow the procedure; you increment the timestamps then call the voice's noteOn() function. The MIDI logging is optional. Notice how the note is saved as m_dLastNoteFrequency and used in the voice's noteOn() call for portamento.

# MIDI Note Off/All Notes Off

The note off events are easy to handle. For the all notes off event, you just loop through the voices and force each one off by using its own MIDI note number in the noteOff() argument. For the single note off, you use the helper function to find the oldest note with a matching note number so that notes are turned off in succession.

```cpp
CMiniSynthVoice::reset();
CVoice::reset();
m_dPortamentoInc = 0.0;
m_Osc1.m_uWaveform = SAW1;
m_Osc2.m_uWaveform = SAW1;
m_Osc3.m_uWaveform = SAW1;
m_Osc4.m_uWaveform = NOISE;
```

# All

```cpp
inline virtual bool doVoice(double& dLeftOutput, double& dRightOutput)
{
    // this does basic on/off work zero impact on speed
    if(!CVice::doVoice(dLeftOutput, dRightOutput))
        return false;

    // --- ARTICULATION BLOCK -- /
    // --- layer 0 modulators: velocity->attack
    //                               note number->decay
    m_ModulationMatrix.doModulationMatrix(0);

    // --- update layer 1 modulators
    m_EG1.update();
    m_LF01.update();

    // --- do layer 1 modulators
    m_EG1.doEnvelope();
    m_LF01.doOscillate();

    // --- modulation matrix Layer 1
    m_ModulationMatrix.doModulationMatrix(1);

    // --- update Voice. DCA and Filter
    this->update();
    m_DCA.update();
    m_MoogLadderFilter.update();

    // --- update oscillators
    m_0sc1.update();
    m_0sc2.update();
    m_0sc3.update();
    m_0sc4.update();
}
```

Other MIDI events

The rest of the MIDI events that we support are simple to implement. You just loop through the voices and set the sources on each modulation matrix. Globalization of MIDI messages is left as a Chapter Challenge for you. Since these are slightly different for each API, they are shown below in the full implementation.

# 9.7 MiniSynth Files

MiniSynth uses the following files that you will need to add into your compiler's project in the usual manner. You may also

```cpp
// --- DIGITAL AUDIO ENGINE BLOCK ---
double d0scMix = 0.333*m_0sc1.dooscillate() +
                 0.333*m_0sc2.dooscillate() +
                 0.333*m_0sc3.dooscillate() +
                 m_0sc4.dooscillate();
```

```cpp
// --- apply the filter
double LPFOut = m_MoogLadderFilter.doFilter(d0scMix);
```

```cpp
// --- apply the DCA
m_DCA.doCA(dLPFOut, dLPFOut, dLeftOutput, dRightOutput);
```

```cpp
return true;
```

download the complete project code from

<< ** Code Listing 9.1: Declarations ** >>

```cpp
MiniSynthVoice* m_pVoiceArray[MAX_VOICES];
```

```cpp
// -- MmM
ModulationMatrix m_GlobalModMatrix;
```

```cpp
// --- global params
globalSynthParams m_GlobalSynthParams;
```

```cpp
// -- helper functions for note on/off/voice steal
void incrementVoiceTimestamps();
MiniSynthVoice* getOldestVoice();
MiniSynthVoice* getOldestVoiceWithNote(UINT uMIDInNote);
```

http://www.willpirkle.com/synth/. The MiniSynth core consists of:

For VST3 and AU, you also need to add the file SynthParamLimits.h, which is in the MiniSynth sample code—remember that this file is slightly different for each synth because it contains the GUI control index enumeration.

# 9.8 MiniSynth: RackAFX

Create a new project named MiniSynth and setup the GUI using Table 9.5.

MiniSynth.h

Add the declarations for the voice array, helper functions and last-note and MIDI receive variables:

```cpp
// updates all voices at once
void update();
```

# MiniSynth.cpp

```cpp
// for portamento
double m_dLastNoteFrequency;
```

# Constructor

- create and initialize voices
- synchronize all mod matrix cores

```cpp
// our receive channel
UINT m_uMidiRxChannel;
```

> << END ** Code Listing 9.1: Declarations ** >>

# Destructor

- destroy global mod matrix
- destroy voices

# prepareForPlay()

- set sample rate and call prepareForPlay() on voices
- mass update
- init last note frequency

# update()

Insert this function, which is listed in its entirety above.

# processAudioFrame()

- insert the rendering code to do the render loop
- write out the accumulated values.

```cpp
// --- increment the timestamp for new events
void CMiniSynth::incrementVoiceTimestamps() // RAFX
void Processor::incrementVoiceTimestamps() // VST3
void AUSynth::incrementVoiceTimestamps() // AU
(
    for(int i=0; i<MAX_VOICES; i++)
    {
        CMiniSynth* pVoice = m_pVoiceArray[i];

        // if on, increment
        if(pVoice->m_bNoteOn)
            pVoice->m_uTimestamp++;
    }
)
// --- get oldest note
void CMiniSynth::getOldestVoice() // RAFX
void Processor::getOldestVoice() // VST3
void AUSynth::getOldestVoice() // AU
(
    int nTimeStamp = -1;
    CMiniSynth* pfoundVoice = NULL;
    for(int i=0; i<MAX_VOICES; i++)
    {
        CMiniSynth* pVoice = m_pVoiceArray[i];

        // --- if on and older, save
        // highest timestamp is oldest
        if(pVoice->m_bNoteOn && (int)pVoice->m_uTimestamp > nTimeStamp)
        {
            pfoundVoice = pVoice;
            nTimeStamp = (int)pVoice->m_uTimestamp;
        }
    }
    return pfoundVoice;
)

incrementVoiceTimestamps();
getOldestVoice();
getOldestVoiceWithNote();
```

```cpp
// --- get oldest voice with a MIDI note also
void CMiniSynth::getOldestVoiceNote(UINT uMIDInNote) // RAFX
void Processor::getOldestVoiceNote(UINT uMIDInNote) // VST3
void ASUSynth::getOldestVoiceNote(UINT uMIDInNote) // AU
{
  int nTimestamp = -1;
  CMiniSynth* pFoundVoice = NULL;
  for(int i=0; i<MAX_VOICES; i++) {
    CMiniSynth* pVoice = m_pVoiceArray[i];

    // --- if on and older, save
    // highest timestamp is oldest
    if(pVoice->m_bNoteOn && (int)pVoice->m_uTimestamp > nTimeStamp) {
      pFoundVoice = pVoice;
      nTimestamp = (int)pVoice->m_uTimestamp;
    }
  }
  return pFoundVoice;
}
```

These functions are listed in their entirety above: just insert them into the .cpp.

# midiNoteOn()

- Use the on code to complete the function
- Note: this function will be identical for the rest of the synth projects, and so it will not be shown.

# midiNoteOff()

- Use the off code to complete the function
- Note: this function will be identical for the rest of the synth projects, and so it will not be shown.

<< ** Code Listing 9.2: Init Voices **

```cpp
// Finish initializations here
m_dLastNoteFrequency = -1.0;
```

```cpp
// receive all channels
m_uMidiRxChannel = MIDI_ALL;
```

```cpp
// load up voices
for(int i=0; i<MAX_VOICES; i++)
{
    // --- create voice
    m_pVoiceArray[i] = new MiniSynthVoice;

    // // should never happen
    if(!m_pVoiceArray[i]) return;
}
```

```cpp
// --- global params (MUST BE DONE before setting up matrix!)
m_pVoiceArray[i]->initGlobalParameters(&m_GlobalSynthParams);
```

```cpp
// --- use the first voice to setup the matrix
m_pVoiceArray[0]->initializeModMatrix(&m_GlobalModMatrix);
```

```cpp
// then set the matrix cores on the rest of the voices
for(int i=0; i<MAX_VOICES; i++)
{
    // --- all matrices share a common core of matrix rows
    m_pVoiceArray[i]->setMatrixCore(m_GlobalModMatrix.getMatrixCore());
}
```

<< END ** Code Listing 9.2: Init Voices **

midiModWheel()

midiPitchBend()

- loop through voices and set appropriate value in mod matrix
- Note: these functions will be identical for the rest of the synth projects, and so they will not be shown.

# midiMessage()

- decode the message
- loop through the voices and set appropriate value in mod matrix for:
- Volume
- Pan
- Expression

```cpp
// -- delete on master ONLY
m_GlobalModMatrix.deleteMatrix();

// --- delete voices
for(int i=0; i<MAX_VOICES; i++) {
    delete m_pVoiceArray[i];
}
```

Sustain Pedal

- Note: this function will be identical for the rest of the synth projects, and so it will not be shown.

# 9.9 MiniSynth: VST3

VST3:

Create a new project with the namespace MiniSynth and setup the GUI using Table 9.5.

Replace (double)m_nSampleRate with (double)processSetup.sampleRate

AU:

# << ** Code Listing 9.4: One Time Init ** >>

```cpp
for(int i=0; i<MAX_VOICES; i++) {
```

# VSTSynthProcessor.h

Add the declarations for the voice array, helper functions and last-note and MIDI receive variables:
