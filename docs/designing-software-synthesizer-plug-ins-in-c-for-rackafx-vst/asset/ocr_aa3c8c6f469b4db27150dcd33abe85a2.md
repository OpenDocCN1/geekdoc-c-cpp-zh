Finally, knock out the

```
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

```
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