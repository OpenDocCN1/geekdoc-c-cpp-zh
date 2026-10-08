```
if(bAllNotesOff)
{
  << INSERT ** Code Listing 9.7: All Notes Off ** >>
  return true;
}
```

```
<< INSERT ** Code Listing 9.8: Note Off ** >>
  return true;
}
bool _std_call CMiniSynth::midiModWheel(args. . .)
{
  // test channel/ignore
  if(m_uMiDiRxChannel != MIDI_CH_ALL && uChannel != m_uMiDiRxChannel)
  return false;
  for(int i=0; i<MAX_VOICES; i++)
{
    m_pValueArray[i]->m_ModulationMatrix.m_dSources[SOURCE_MODWHEEL] = uModValue;
  }
  return true;
}
```

```
bool _std_call CMiniSynth::midiPitchBend(args. . .)
{
  // test channel/ignore
  if(m_uMiDiRxChannel != MIDI_CH_ALL && uChannel != m_uMiDiRxChannel)
  return false;
  for(int i=0; i<MAX_VOICES; i++)
{
    // send to matrix
    m_pValueArray[i]->m_ModulationMatrix.
    m_dSources[SOURCE_PITCHB] = fNormalizedPitchBendValue;
  }
  return true;
}
```

```
bool _std_call CMiniSynth::midiMessage(args. . .)
{
  // test channel/ignore
  if(m_uMiDiRxChannel != MIDI_CH_ALL && (UINT)cChannel !==
  m_uMiDiRxChannel
```