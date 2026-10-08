
# << ** Code Listing 8.15: Note On ** >>

```cpp
// --- call the helper function
if(m_Voices[0].m_Osc1.m_bNoteOn)
    startNote(0, uMIDINote, uVelocity);
else if(m_Voices[1].m_Osc1.m_bNoteOn)
    startNote(1, uMIDINote, uVelocity);
else
{
    // voice steal: NanoSynth heuristic is
    // --- if new note is lower than both, steal the lower of the two
    // otherwise steal the higher one
    //
    // --- test note
    UINT uNote0 = m_Voices[0].m_Osc1.m_uMIDINoteNumber;
    UINT uNote1 = m_Voices[1].m_Osc1.m_uMIDINoteNumber;

    // --- if new note is lower than both, steal the lower of the two
    if(uMIDINote < uNote0 && uMIDINote < uNote1)
    {
        if(uNote0 < uNote1)
            stealNote(0, uMIDINote, uVelocity);
        else
            stealNote(1, uMIDINote, uVelocity);
    } else // --- steal the higher one
        if(uNote0 > uNote1)
            stealNote(0, uMIDINote, uVelocity);
        else
            stealNote(1, uMIDINote, uVelocity);
}
```

# << ** END Code Listing 8.15: Note On ** END >>

etc...

```cpp
bool __stdcall CNanoSynth::midiNoteOff(UINT uChannel, UINT uMIDINote,
UINT uVelocity, bool bAllNotesOff)
{
  <SNIP SNIP SNIP>
```

```cpp
// --- turn off IF this is the proper note (last note played)
if(bAllNotesOff)
{
  m_Voices[0].m_EG1.noteoff();
  m_Voices[1].m_EG1.noteoff();
}
  return true;
}
```

** Code Listing 8.16: Note Off ** >>

```cpp
// --- test by MIDI Note number
if(uMIDINote == m_Voices[0].m_Oscl1.m_uMIDINoteNumber)
  m_Voices[0].m_EG1.noteoff();
if(uMIDINote == m_Voices[1].m_Oscl1.m_uMIDINoteNumber)
  m_Voices[1].m_EG1.noteoff();
```

** END Code Listing 8.16: Note Off END >>

etc...

interconnections with a modulation matrix. Global parameters make the synth updates more efficient. Believe it or not, adding this finishing touch to NanoSynth refreshingly easy and consists of four steps; most of the work is done in the synth objects during the initialization and update functions.

- modify the oscillator, filter, envelope generator and DCA classes as shown previously (or download them from my website)
- add a global parameter declaration to the plugin's .h file
- call the global parameter initialization on each voice sub-component
- remove the for() loop in the plugin's update() function and replace the loop with a single set of global parameter adjustments

Initializing the sub-components is done in the constructor where you set the matrix routing information on the voice components. In this code, the variable m_GlobalSynthParams is the plugin's global parameter structure. Updating the global parameters is easy once you decode the structure of the code. You have to match your GUI controls with each of the voice's components.

In preparePlay(), setActive(), there is one detail to deal with. Oscillator number 2 is detected by 2.5 cents, however this is now a global parameter. So, we need to replace the voice initialization with a global parameter initialization to:

```cpp
m_Voices[i].m_Osc2.m_nCents = 2.5;
```

becomes

```cpp
m_GlobalSynthParams.osc2Params.nCents = 2.5;
```

and since it is a global variable, you only need to set it.

# 8.21 Final NanoSynth: Rack

# NanoSynth.h

The final NanoSynth starts with the plugin's .h file for the global parameter declaration.

# NanoSynth.cpp

Modify the voice setup in the constructor.

# preparePlay()

![](img/b42d0ca53f4a88d162d555.png)

preparePlay() replace the old initialization code with the slightly altered version that places the detuning in a global:

```cpp
m_Voices[i].m_0sc2.m_uMIDINoteNumber = m_nPendingINote[i];
m_Voices[i].m_0sc2.m_d0scFo = midiFreqTable[m_nPendingINote[i]];
```

```cpp
m_Voices[i].m_0sc1.updateOscillator();
m_Voices[i].m_0sc2.updateOscillator();
```

```cpp
// --- crank the EG up
m_Voices[i].m_EG1.startEG();
```

```cpp
// --- set the note # velocity of newest note
m_Voices[i].m_ModulationMatrix.m_dSources[SOURCE_MIDI_NOTE] = m_nPendingINote[i];
m_Voices[i].m_ModulationMatrix.m_dSources[SOURCE_VELOCITY] = m_nPendingMIDIVocity[i];
```

```cpp
// --- reset
m_nPendingINote[i] = -1;
m_nPendingMIDIVocity[i] = -1;
```

```cpp
else
{
  m_Voices[i].m_0sc1.stopOscillator();
  m_Voices[i].m_0sc2.stopOscillator();
  m_Voices[i].m_LF01.stopOscillator();
  m_Voices[i].m_EG1.stopEG();
}
```

parameter.update()

Finally, knock out the update() function and replace the for() loop. Make sure to leave the modulation matrix code alone.

# 8.22 Final NanoSynth: VST

# VSTSynthProcessor.h

The final NanoSynth starts with the plugin's .h file for the global parameter declaration.

```cpp
// --- one complete voice
struct nanoSynthVoice{}
```

# VSTSynthProcessor.cpp

# setActive()

In setActive() add the global initialization calls to the voice objects inside the same for() loop where you setup the sample rates, and at the same time, move the detuning outside the loop and into the global parameter.

```cpp
COBLimitedOscillator m_0sc1;
COBLimitedOscillator m_0sc2;
CLFO m_lFO1;
CEnvelopeGenerator m_EG1;
CMoLadderFilter m_Filter1;
CDCA m_DCA;
CModulationMatrix m_ModulationMatrix;
```

# update()

```cpp
#define MAX_VOICES 2
```

Finally, knock out

```cpp
<SNIP SNIP SNIP>
```

```cpp
// Add your code here: 
// --- the Modulation Matrix
CModulationMatrix m_GlobalModMatrix;
```

```cpp
nanoSynthVoice m_Voices[MAX_VOICES];
int m_nPendingINote[MAX_VOICES]; // if -1 no pending note
int m_nPendingMIDIVelo[MAX_VOICES]; // if -1 no velocity
```

```cpp
void startNote(int nIndex, UINT uMIDINote, UINT uMIDIVelo);
void stealNote(int nIndex, UINT uPendingMIDINote, UINT uPendingVelocity);
```

```cpp
etc...
}
```

update() function and replace the for() loop. Make sure to leave the modulation matrix code alone.

# 8.23 Final

CNanoSynth::CNanoSynth()
{

```cpp
<SNIP SNIP SNIP>
```

```cpp
m_d0scPitchBendModRange = OSC_PITCHBEND_MOD_RANGE;
m_dAmpModRange = AMP_MOD_RANGE;
```

```cpp
<< INSERT ** Code Listing 8.9: Global Parameter Init I ** HERE >>
}
```

# NanoSynth: AU

CNanoSynth::CNanoSynth(void)
{

# AUSynth.h

The final NanoSynth starts with the plugin.h file for the global parameter declaration.

```cpp
// --- delete on master
m_GlobalModMatrix.deleteModMatrix();
}
```

# AUSynth.cpp

```cpp
bool __stdcall CNanoSynth::preparePlay()
{
```

```cpp
<< INSERT ** Code Listing 8.10: Global Parameter Init II ** HERE >>

update();

return true;
}
```

```cpp
void CNanoSynth::update()
{
```

```cpp
<< INSERT ** Code Listing 8.11: Global Parameter Update I ** >>

// --- mod matrix stuff
if(m_uFilterTrack == 1)

etc...
}
```

# Constructor

```cpp
bool __stdcall CNanoSynth::processAudioFrame(float* pInputBuffer,
float* pOutputBuffer,
UINT uNumInputChannels,
UINT uNumOutputChannels
```

```cpp
double dOutL = 0.0;
double dOutR = 0.0;
double dAccumOutL = 0.0;
double dAccumOutR = 0.0;
```

<< INSERT ** Code Listing 8.12: Mod Matrix Render II ** >>

pOutputBuffer[0] = dAccumOutL;

```cpp
// Mono-In, Stereo-Out (AUX Effect)
if(uNumInputChannels == 1 && uNumInputChannels == 2)
pOutputBuffer[1] = dAccumOutL;

```

```cpp
// Mono-In, Stereo-Out (INSERT Effect)
if(uNumInputChannels == 2 && uNumInputChannels == 2)
pOutputBuffer[1] = dAccumOutR;

```

<< INSERT ** Code Listing 8.13: Start Note ** HERE >>

<< INSERT ** Code Listing 8.14: Steal Note ** HERE >>
