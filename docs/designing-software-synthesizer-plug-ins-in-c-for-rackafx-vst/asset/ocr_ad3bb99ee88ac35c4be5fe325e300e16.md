```
break:
)
// --- NOTE OFF
case Event::kNoteOffEvent:
|
  // --- get the channel/note/vel
  UINT uMIDiChannel = (UINT)vEvent.noteoff.channel;
  UINT uMIDiNote = (UINT)vEvent.noteoff.pitch;
  UINT uMIDiVelocity = (UINT)(127.0*vEvent.noteoff.velocity); // not used

  // --- test channel/ignore
  if(m_uMidiRxChannel != MIDI_CH_ALL && uMIDiChannel !=n    m_uMidiRxChannel)
    return false;

  // --- event occurred
  noteEvent = true;

  // --- fix noteID as per SDK
  if(vEvent.noteoff.noteID == -1)
    vEvent.noteoff.noteID = uMIDiNote;

  #if(LOG_MIDI && _DEBUG)
  FDebugPrint("-- Note Ch:%d Note:%d Vel:%d \n");
```