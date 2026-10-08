```
for(int i=0; i<MAX_VOICES; i++)
  {
    m_pVoiceArray[i]->m_ModulationMatrix.m_dSources
    [SOURCE_MODWHEEL] = (UINT)inValue;
  }
break;
```

```
case SUSTAIN_PEDAL:
  for(int i=0; i<MAX_VOICES; i++)
  {
    m_pVoiceArray[i]->m_ModulationMatrix.m_dSources [SOURCE_SUSTAIN_PEDAL]
    (UINT)inValue;
  }
break;
```

```
case ALL_NOTES_OFF:
  // --- NOTE: some clients may trap this
  for(int i=0; i<MAX_VOICES; i++)
  {
    m_pVoiceArray[i]->noteOff(m_pVoiceArray[i]->m_uMIDINotenNumber);
  }
break;
```

etc..