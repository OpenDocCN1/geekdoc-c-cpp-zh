
together, however before writing to the outputs, we declare accumulator variables as well as the normal voice output variables. two oscillators are mixed with scalar values of 0.5 to try to minimize clipping. We will discuss the code that deals with stealing and turning off the oscillators in the next section so it for now.

## Processor::Processor()

```
// -- initialize mod ranges
nm_dOscFoModRange = OSC_FO_MOD_RANGE;
m_dFilterModRange = FILTER_FC_MOD_RANGE;
m_dOscFoPitchBendModRange = OSC_PITCHBEND_MOD_RANGE;
m_dAmpModRange = AMP_MOD_RANGE;
```

## 8.16 Dynamic Voice Allocation

Voice stealing (also called voice allocation or dynamic voice allocation) is a by-product of polyphony, and it can be tricky and complicated. If the user triggers a new note the supply of voices is exhausted, you need to shut one voice off and steal it for the new note. Deciding on which voice to terminate is up to you, the synth designer. A heuristic is used to decide on the fate of the stolen note. Heuristics trade-offs involve their mechanism; all have their strengths and weaknesses. Some options are:

- steal the oldest note
- steal the oldest note that isn't the lowest pitched note
- steal the note with the lowest velocity
- steal the first note that has already been released
- steal notes that are inside of chord voicings

result PLUGIN_API Processor::setActive(TBool state)

```cpp
if(state){
    <SNIP SNIP SNIP>

    update();

    // --- default turn on volume and center the pan
    m_GlobalModMatrix.m_dSources[SOURCE_MIDI_VOLUME_CC07] = 127;
    m_GlobalModMatrix.m_dSources[SOURCE_MIDI_PAN_CC10] = 64;

    <SNIP SNIP SNIP>

    // NOTE NUMBER -> FILTER Fc Control
    pRow = createMatrixRow(SOURCE_MIDI_NOTE_NUM,
        DEST_ALL_FILTER_KEYTRACK,
        &m_dFilterKeyTrackIntensity,
        &m_dDefaultModRange,
        TRANSFORM_NUMBER_TO_FREQUENCY,
        false); /* DISABLED BY DEFAULT */

    m_GlobalModMatrix.addModMatrixRow(pRow);
```

<< INSERT ** Code Listing 8.4: Mod Matrix Routings II ** HERE >>

<SNIP SNIP SNIP>

```cpp
m_LF01.m_uModDestOutput1 = SOURCE_LF01;
nm_LF01.m_uModDestOutput2 = SOURCE_LF01Q;
```

<< INSERT ** Code Listing 8.5: Mod Matrix Connections II ** HERE >>

- steal notes that are outside of chord voicings
- steal notes that are not part of a melody line
- MIDI channel priority based

The list goes on—see Limberis and Bryan (1993) for an interesting paper on dynamic voice allocation for pure software synthesizers. The last item in the list comes from the MMA DLS specification, in which multi-timbral voices are distributed across the 16 MIDI channels. The channels are prioritized according to number, with channel 1 as the highest priority and 16 as the lowest.
Since our synths are mono-timbral, we will use note-based heuristics.

For this version of NanoSynth, the heuristic is to steal the note that isn't the lowest pitched:

- first try to steal a note with the same note number that happens if the

```cpp
Processor::doProcessEvent(Event& vstEvent)
{
<SNIP SNIP SNIP>
// --- NOTE ON
case Event::kNoteOnEvent:
<SNIP SNIP SNIP>
// --- note number in the mod matrix for filter key track m_GlobalModMatrix.m_dSources[SOURCE_MIDI_NOTE_NUM] = uMIDINote:
// --- for Vel-Att scaling
m_GlobalModMatrix.m_dSources[SOURCE_VELOCITY] = uMIDIVelivery:
}
```

etc...
user releases and then quickly re-strikes the same note

- if the higher note is not already being stolen, steal it
- if the new note is lower than the others, steal the lower of the two currently playing
- if both notes are stolen, arbitrarily steal the second note

To polyphony and note stealing, we need a couple of helper functions declared in the plug-in's :file:

```cpp
void startNote(int nIndex, UINT uMIDINote, UINT uMIDIVelocity)void stealNote(int nIndex, UINT uPendingMIDINote, UINT uPendingVelocity)
```

The implementations are in the .cpp file (RackAFX shown). For the start note event, it's the same as the monophonic version, except we choose a voice from the array. The modulation code moved from handler it is now voice-specific information.

For the steal event, it's fairly simple—you put the EG into shutdown mode. The EG object will handle legacy and return to zero conditions for you. You might also add a TRACE statement so you can watch the steal occur.

The note on and off handlers are the last thing to be changed. In the note handler, first test to see if there is an available note-if so, with a call to startNote(). If not, make the note stealing and call the stealNote() function correctly—it's very basic but preserves the lowest note at all times.

```cpp
bool Processor::doControlUpdate(ProcessData& data)
```

The note off handler is simple. In this case you just find the note with the case

> <SNIP SNIP SNIP Indents Removed>

```cpp
// --- MIDI messages
case MIDI_PITCHBEND: // want -1 to +1

// LOG MIDI
// -- send to matrix
m_dMIDIDIPitchBend = unipolarToBipolar(value);
m_GlobalModMatrix.m_dSources[SOURCE_PITCHBEND]

break;
case MIDI_VOLUME_CC7: // want 0 to 127

// LOG MIDI
// -- send to matrix
m_uMIDIVolumeCC7 = unipolarToMIDI(value);
m_GlobalModMatrix.m_dSources[SOURCE_VOLUME_CC07]

break;
```

m_dMIDIPitchBend:

m_uMIDIVolumeCC7:

matching MIDI note number and send the noteOff() message to the EG, placing it in shutdown mode.

Pitch bend, volume and panning need MIDI message handlers that are platform dependent, so we will look at those.

If the note is not stolen, we use the old code and replace with the polyphonic version; notice this occurs after the global mod matrix has been initialized and the range/intensity variables have been set:

```cpp
double m_dFilterModRange;
```

# Constructor

Remove the original code and replace with polyphonic version; notice this occurs after the global mod matrix has been initialized and the range/intensity variables have been set:

```cpp
<SNIP SNIP SNIP>
```

```
double m_d0scFoPitchBendModRange;
```

```
double m_dAmpModRange;
```

# Destructor

```
etc...

Just delete our master modulation matrix core.

# preparePlay()

Likewise, remove the old code and replace with the polyphonic version:

# update()

Here, polyphone-ize again by setting all the voice parameters on all voices at once; only replace the synth update and not the modulation matrix code.

```cpp
void update()
{
    <SNIP SNIP SNIP>
    // --- mod matrix
    if(mUFilterTrack == 1)
        m_GlobalModMatrix.enableMatrixRow(SOURCE_MIDI_NOTE_NUM, DEST_ALL_FILTER_KEYTRACK, true);
    else
        m_GlobalModMatrix.enableMatrixRow(SOURCE_MIDI_NOTE_NUM, DEST_ALL_FILTER_KEYTRACK, false);
}
```
<< INSERT ** Code Listing 8.6: Mod Matrix Update I HERE >>
etc...
```
individual voice.

That takes care of our first attempt at polyphony. Now, start your compilers and add the functionality for Poly NanoSynth.

## 8.17 Poly NanoSynth: RackAFX

There are no added controls, so we can go directly to the NanoSynth.h and add the new declarations.

# NanoSynth.h

# AUSynth.h

Outside of the object declaration, add the new voice structure and MAX_VOICES definitions and, inside the object, declare the arrays and helper functions. Remove previous object declarations as well.

Add the range variable declarations:

```cpp
class AUSynth : public AUInstrumentBase
```

```cpp
public:
```

# NanoSynth.cpp

We need to alter all the functions we discussed so far plus a few MID-specific ones. Most of the code is just cut-and-paste from the listings.

```cpp
<SNIP SNIP SNIP>
```

```cpp
double m_dFilterModRange;
```

# Constructor

Remove the original code and replace with polyphonic version; notice this occurs after the global mod matrix has been initialized and the range/intensity variables have been set:

```cpp
double m_d0scFoPitchBendModRange;
```

```cpp
double m_dAmpModRange;
```

# Destructor

```cpp
etc...
```

Just delete our master modulation matrix core.

# preparePlay()

Likewise, remove the old code and replace with the polyphonic version:

# update()

Here, polyphone-ize again by setting all the voice parameters on all voices at once; only replace the synth update and not the modulation matrix code.

```cpp
void update()
{
    <SNIP SNIP SNIP>
    // --- mod matrix
    if(mUFilterTrack == 1)
        m_GlobalModMatrix.enableMatrixRow(SOURCE_MIDI_NOTE_NUM, DEST_ALL_FILTER_KEYTRACK, true);
    else
        m_GlobalModMatrix.enableMatrixRow(SOURCE_MIDI_NOTE_NUM, DEST_ALL_FILTER_KEYTRACK, false);
}
```
