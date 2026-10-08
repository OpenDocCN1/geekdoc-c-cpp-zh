```
#if(LOG_MIDI && _DEBUG)
    FDebug("-- Pitch Bend: %f\n",
    m_dMIDIPitchBend);
#endif
break;
```

```
}\case MIDI_MODWHEEL: // want 0 to 127
{
    m_uMIDIDModWheel = unipolarToMIDI(value);
    #if(LOG_MIDI && _DEBUG)
        FDebug("-- Mod Wheel: %d\n",
        m_uMIDIDModWheel);
    #endif
    break;
```

```
}\case MIDI_VOLUME_CC7: // want 0 to 127
{
    m_uMIDIVolumeCC7 = unipolarToMIDI(value);
    #if(LOG_MIDI && _DEBUG)
        FDebug("-- Volume: %d\n",
        m_uMIDIVolumeCC7);
    #endif
    break;
```

```
}
case MIDI_PAN_CC10: // want 0 to 127
{
    m_uMIDIPanCC10 = unipolarToMIDI(value);
    #if(LOG_MIDI && _DEBUG)
        FDebug("-- Pan: %d\n",
        m_uMIDIPanCC10);
    #endif
    break;
```

```
case MIDI_EXPRESSION_CC11: // want 0 to 127
{"
```