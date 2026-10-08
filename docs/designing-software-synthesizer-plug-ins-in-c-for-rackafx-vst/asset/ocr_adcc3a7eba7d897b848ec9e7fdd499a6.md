If the note is not stolen, we just use the same code as before to stop the note, but this time applied to the

```
// --- send to matrix
_uMIDiPanCC10 = unipolarToMIDI(value);
m_GlobalModMatrix.m_dSources[SOURCE_MIDI_PAN_CC10] = m_uMIDiPanCC10;
break;
}
case MIDI_SUSTAIN_PEDAL: // want 0 to 1
{
    // LOG MIDI
    // --- send to matrix
m_GlobalModMatrix.m_dSources[SOURCE_SUSTAIN_PEDAL] = unipolarToMIDI(value);
    break;
}
void Processor::update()
{
    <SNIP SNIP SNIP SNIP>
    // --- mod matrixKeyTrack
    if(mUFilterKeyTrack == 1)
        m_GlobalModMatrix.enableModMatrixRow(SOURCE_MIDI_NOTE_NUM, DEST_ALL_FILTER_KEYTRACK, true);
    else
        m_GlobalModMatrix.enableModMatrixRow(SOURCE_MIDI_NOTE_NUM, DEST_ALL_FILTER_KEYTRACK, false);
}
// INSERT ** Code Listing 8.6: Mod Matrix Update I ** HERE >>
etc...
```

individual voice.

That takes care of our first attempt at polyphony. Now, start your compilers and add the functionality for Poly NanoSynth.

# 8.17 Poly NanoSynth: RackAFX

There are no added GUI controls, so we can go directly to the NanoSynth.h file and add the new declarations.