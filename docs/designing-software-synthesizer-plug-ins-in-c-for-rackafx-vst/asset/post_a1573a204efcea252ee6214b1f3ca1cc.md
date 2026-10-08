
Finally, knock out the

```cpp
bool __stdcall CNanoSynth::midiNoteOn(UINT uChannel, UINT uMIDINote,
    UINT uVelocity)
{
    // test channel/ignore
    if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
        return false;

    << INSERT ** Code Listing 8.15: Note On ** HERE >>

    return true;
}
```

```cpp
bool __stdcall CNanoSynth::midiNoteOff(UINT uChannel, UINT uMIDINote,
    uVelocity, bool bAllNotesOff)
{
    // test channel/ignore
    if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
        return false;

    // --- all notes off!
    if(bAllNotesOff)
    {
        m_Voices[0].m_EG1.noteOff();
        m_Voices[1].m_EG1.noteOff();
    }

    << INSERT ** Code Listing 8.16: Note Off ** HERE >>

    return true;
}
```

update() function and replace the for() loop with the fixed global code. Make sure to leave the modulation matrix code alone.

Build and test your final NanoSynth. In the next chapter, we will start a new synth MiniSynth that will build on everything you've learned so far. We won't have the room to print every line of code for the rest of the projects when it comes to the modulation matrix and global parameters so much of it will be the same or nearly the same as what you've done so far. You may want to bookmark this chapter for future reference.

```cpp
bool __stdcall CNanoSynth::midiPitchBend(UINT uChannel,
               int nActualPitchBendValue,
               float fNormalizedPitchBendValue,
```

```cpp
// test channel/ignore
if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
    return false;
```

```cpp
#ifdef LOG_MIDI
TRACE("-- Pitch Bend Ch:%d int:%d float:%f \n", uChannel,
       nActualPitchBendValue, fNormalizedPitchBendValue);
#endif
```

```cpp
for(int i=0; i<MAX_VOICES; i++)
{
    // -- send to matrix
    m_Voices[i].m_ModulationMatrix.m_dSources[SOURCE_PITCHBEND] =
        fNormalizedPitchBendValue;

return true;
}
```

# Bibliography

- Limmeris, Alex and Bryan, Joe. 1993. "An Architecture for a Multiple Digital Signal Processor Based Music Synthesizers with Dynamic Voice Allocation." Presented at the 95th Audio Engineering Society Convention. New York.

- MIDI Manufacturers Association. 1999. Downloadable Sounds Level 2, vol. 1.0.

- MIDI Manufacturers Association. 2004. Downloadable Sounds Level 1, vol. 1.1b.

- MIDI Manufacturers Association. 2006. Downloadable Sounds Level 2, Amendment 2.

```cpp
bool __stdcall cNanoSynth::midiMessage(unsigned char cChannel,
                              unsigned char cStatus,
                              unsigned char cData,
                              unsigned char cData2)
{
    // test channel/ignore
    if(m_uMidiRxChannel != MIDI_CH_ALL && (UINT)cChannel !=
m_uMidiRxChannel)
        return false;

    switch(cStatus)
    {
        <SNIP SNIP SNIP>

        case CONTROL_CHANGE:
        {
            switch(cData)
            {
                case VOLUME_CC07:
```

```cpp
// --- send to matrix
for(int i=0; i<MAX_VOICES; i++)
(
    m_Voices[i].m_ModulationMatrix.m_dSources
    [SOURCE_MIDI_VOLUME_CC07] = (UINT)cData2;
)
break;
```

```cpp
case PAN_CC10:
{
    // --- send to matrix
    for(int i=0; i<MAX_VOICES; i++)
    (
        m_Voices[i].m_ModulationMatrix.m_dSources
        [SOURCE_MIDI_PAN_CC10] = (UINT)cData2;
    )
    break;
```

```cpp
etc...
```

```cpp
case SUSTAIN_PEDAL:
{
    // indents removed for readability
    for(int i=0; i<MAX_VOICES; i++)
    {
        // ---send to matrix
        m_pVoiceArray[i]->m_ModulationMatrix.m_dSources
        [SOURCE_SUSTAIN_PEDAL] = (UINT)cData2;
    }
    break;
```

```cpp
// --- one complete voice
struct nanoSynthVoice
{
```

```cpp
CQBLimitedOscillator m_0sc;
CQBLimitedOscillator m_0sc2;
CLFO m_LFO1;
CEnvelopeGenerator m_EG1;
CMoogLadderFilter m_Filter1;
CDCA m_DCA;
CModulationMatrix m_ModulationMatrix;
);
```

```cpp
#define MAX_VOICES 2
```

class Processor : public AudioEffect

{

```cpp
<SNIP SNIP SNIP>
```

```cpp
// Add your code here: //
// --- the Modulation Matrix
CModulationMatrix m_GlobalModMatrix;
```

nanoSynthVoice m_Voices[MAX_VOICES];

```cpp
int m_nPendingMIDINote[MAX_VOICES]; // if -1 no pending note
int m_nPendingMIDIVel[MAX_VOICES]; // if -1 no pending velocity
```

```cpp
void startNote(int nIndex, UINT uMIDINote, UINT uMIDIVocity);
void stealNote(int nIndex, UINT uPendingMIDINote,
UINT uPendingVelocity);
```

etc...

}

```cpp
tresult PLUGIN_API Processor::setActive(TBool state)
{
  if(state)
    {
      << INSERT ** Code Listing 8.10: Global Parameter Init II ** HERE
      >>

    update();

    // clear

    m_dLastNoteFrequency = -1.0;

    // -- for individual rows

    modMatrixRow* pRow = NULL;

    <SNIP SNIP SNIP>

    LF01 -> FILTER1 FC
    pRow = createMatrixRow(SOURCE_LF01,

      DEST_ALL_FILTER_FC,
      &m_dDefaultModIntensity,
      &m_dFilterModRange,
      TRANSFORM_NONE,
      false); /* DISABLED BY DEFAULT * /

    m_GlobalModMatrix.addMatrixRow(pRow);

  << INSERT ** Code Listing 8.9: Global Parameter Init I ** HERE >>

etc...
```

```cpp
void Processor::update())
{
  << INSERT ** Code Listing 8.11: Global Parameter Update I ** HERE >>

  // --- mod matrix stuff
  if(m_uFilterKeyTrack == 1)

  etc...
}
tresult PLUG_API Processor::process(ProcessData& data)
{
  <SNIP SNIP SNIP>
  // --- output "accumulator"
  double dOutL = 0.0;
  double dOutR = 0.0;
  double dAccum = 0.0;
  double dOutL = 0.0;

  for(int j=0; j<samplesToProcess;
    // clear accumulators
    dAccumOutL = 0.0;
    dAccumOutR = 0.0;

  for(int j=0; j<samplesToProcess; j++)
    // write to buffer
    buffers[0][j] = dAccumOutL; // left
    buffers[1][j] = dAccumOutR; // right

  // --- update the counter
  for(int i=0; i < OUTPUT_CHELS; i++)
    etc...
```

```cpp
Processor::startNote(int nIndex, UINT uMIDINote, UINT uMIDIVocity)
{
  << INSERT ** Code Listing 8.13: Start Note ** >>
}
```

```cpp
Processor::stealNote(int nIndex, UINT uPendingMIDINote, UINT uPendingVelocity)
{
  << INSERT ** Code Listing 8.14: Steal Note ** >>
}
```

```cpp
bool Processor::doProcessEvent(Event& vstEvent)
{
  bool noteEvent = false;

  // --- Note On or Off messages
  switch(vstEvent.type)
  {
    // --- Note On
    case Event::kNoteEvent:
    {
      <SNIP SNIP SNIP>
      // place after the MIDI
      << INSERT ** Code Listing 8.15: Note On ** >>

    }

    // --- Note Off
    case Event::kOffEvent:
    {
      <SNIP SNIP SNIP>
      // place after the MIDI
      << INSERT ** Code Listing 8.16: Note Off ** >>
    }
  }
}
```

```cpp
bool Processor::doControlUpdate(ProcessData& data)
{
  <SNIP SNIP SNIP>
  // --- MIDI messages
  switch(data.type)
  {
    case MIDI_PITCHEND: // want -1 to +1
    (
        m_dMIDIPitchBend = unipolarToBipolar(value);

        // LOG MIDI
        // --- send to matrix
        for(int i=0; i<MAX_VOICES; i++)
        {
            m_Voices[i].m_ModulationMatrix.m_dSources
            [SOURCE_PITCHBEND] = m_dMIDIPitchBend;
        }
        break;
    )
    case MIDI_VOLUME_CC7: // want 0 to 127
    (
        m_uMIDIVolCC7 = unipolarToMIDI(value);

        // LOG MIDI
        // --- send to matrix
        for(int i=0; i<MAX_VOICES; i++)
        {
            m_Voices[i].m_ModulationMatrix.m_dSources
            [SOURCE_MIDI_VOLUME_CC07] = m_uMIDIVolCC7;
        }
        break;
    )
    case MIDI_PAN_CC10: // want 0 to 127
    {
        m_uMIDIPanCC10 = unipolarToMIDI(value);

        // LOG MIDI
        // --- send to matrix
        for(int i=0; i<MAX_VOICES; i++)
        {
            m_Voices[i].m_ModulationMatrix.m_dSources
            [SOURCE_MIDI_PAN_CC10] = m_uMIDIPanCC10;
        }
        break;
    }
    case MIDI_ALL_NOTES_OFF:
    {
      for(int i=0; i<MAX_VOICES; i++)
        m_Voices[i].m_EG1.noteOff();

      break;
    }
    case MIDI_SUSTAIN_PEDAL: // want 0 to 1
    {
      bool bSus = value > 0.5 ? true : false;

      // LOG MIDI
      // --- send to matrix
      UINT uMIDI = unipolarToMIDI(value);
      for(int i=0; i<MAX_VOICES; i++)
      {
            m_Voices[i].m_ModulationMatrix.m_dSources
            [SOURCE_SUSTAIN_PEDAL] = uMIDI;
      }

      break;
    }
  }
}
```
