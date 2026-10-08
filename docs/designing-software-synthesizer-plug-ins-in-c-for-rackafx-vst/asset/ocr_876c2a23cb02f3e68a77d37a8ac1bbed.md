```
#if(LOG_MIDI && _DEBUG)
```

```
#endif
```

```
// test channel/ignore
```

```
if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
    return false;
```

```
bool Processor::doEvent(Event&
```

```
    bool noteEvent = false;
```

```
    // --- process Note On or Note Off messages here
    switch(vstevent.type)
```

```
        // --- NOTE ON
        case Event::kNoteEvent:
```

```
        {\n        // --- get the channel/note/vel
        UINT uMIDiChannel = (UINT)vstevent.noteon.channel;
        UINT uMIDiNote = (UINT)vstevent.noteon.pitch;
        UINT uMIDiVelocity = (UINT)
```

```
        (127.0)*vstevent.noteon.velocity);
```

```
        // --- channel/ignore
        if(m_uMidiRxChannel != MIDI_CH_ALL && uMIDiChannel != 
            m_uMidiRxChannel)
```

```
            return false;
```

```
        // --- event occurred
        noteEvent = true;
```

```
        // --- fix noteid as per SDK
        if(vstevent.noteon.noteid == -1)
            vstevent.noteon.noteid = uMIDiNote;
```

```
#if(LOG_MIDI && _DEBUG)
DebugPrint("-- Note On Ch:%d Note:%d Vel:%d \n",
    uMIDiChannel, uMIDiNote, uMIDiVelocity);
```

```
#endif
```