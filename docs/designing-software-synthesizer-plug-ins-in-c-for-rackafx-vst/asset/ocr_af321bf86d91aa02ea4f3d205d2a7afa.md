```
bool Processor ::doProcessEvent(Event& vstEvent)
{
    bool noteEvent = false;

    switch(vstEvent.type)
    {
        // --- NOTE ON
        case Event::*kNoteEvent:
        {
            // --- get the channel/note/vel
            UINT uMIDiChannel = (UINT)vstEvent.noteon.channel;
            UINT uMIDiNote = (UINT)vstEvent.noteon.pitch;
            UINT uVelocity = (UINT)(127.0*vstEvent.noteon.velocity);

            // --- test channel/ignore
            if(m_uMIDiRxChannel != MIDI_CH_ALL && uMIDiChannel =
                m_uMIDiRxChannel)
                return false;

            // --- event occurred
            noteEvent = true;

            // --- fix noteID as per SDK
            if(vstEvent.noteon.noteID == -1)
                vstEvent.noteon.noteID = uMIDiNote;

            << INSERT ** Code Listing 9.6: Note On ** HERE >>

            break;
        }
        // --- NOTE OFF
        case Event::*kNoteOff:
        {
            // --- get the channel/note/vel
            UINT uMIDiChannel = (UINT)vstEvent.noteoff.channel;
            UINT uMIDiNote = (UINT)vstEvent.noteoff.pitch;
            UINT uVelocity = (UINT)(127.0*vstEvent.noteoff.velocity) =
        }
    }
}
```

+   - Mod Wheel
- Volume