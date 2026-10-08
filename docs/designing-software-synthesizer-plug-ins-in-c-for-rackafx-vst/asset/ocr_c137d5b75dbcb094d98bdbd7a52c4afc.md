- Indicates the user has moved the built-in vector joystick which we use in VectorSynth
AniSynth

```
<SNIP SNIP SNIP> -- you can skip functions 8 and 9
virtual bool __stdcall midiNoteOn(UINT uchannel,
                               UINT uMIDINote,
                               UINT velocity);
```

- called for each MIDI note event delivering channel, note number and velocity

```
virtual bool __stdcall midiNoteOff(UINT uchannel, UINT uMIDINote,
                                      UINT velocity, bool bAllNotesOff);
```

- called for each MIDI note off event
- also called for all notes off panic message

```
virtual bool __stdcall midiModWheel(UINT uchannel, UINT uModValue);
- function to handle changes to the Mod Wheel (found on most synth controllers)
```

```
virtual bool __stdcall midiPitchBend(UINT uchannel,
                                       int nActualPitchValue,
                                       float nNormalizedPitchBendValue);
```

- specialized function for the pitch bend wheel/joystick

```
<SNIP SNIP SNIP> -- we won't be implementing MIDI clock in the book projects
virtual bool __stdcall midiMessage(unsigned char cchannel,
                                     unsigned char cStatus,
                                     unsigned char cData,
                                     unsigned char cData2);
```

- all the rest of the MIDI messages including continuous controllers

The last part of the MiniSynth.h file consist of a few member variables. For the MiniSynth these are:

```
CMiniSynth* m_pVoiceArray[MAX_VOICES];
void incrementVoiceTimestamps;
CMiniSynth* getOldVoice();
CMiniSynth* getOldVoiceWithNote(UINT uMIDINote);
```

```
// --- updates all voices at once
void update();
```

```
// --- for portamento
double m_dLastNoteFrequency;
```

```
// --- our receive channel
UINT m_uMidiRxChannel;
```