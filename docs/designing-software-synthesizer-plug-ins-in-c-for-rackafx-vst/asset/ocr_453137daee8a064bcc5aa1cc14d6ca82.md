```
{
  m_voiceArray[i]->m_ModulationMatrix;
  m_dSources[SOURCE_MIDI_VOLUME_CC07] = m_uMIDIVolumeCC77;
}
break;
case MIDI_PAN_CC10: // want 0 to 127
{
  m_uMIDIPanCC10 = unipolarToMIDI(value);
  for (int i=0; i<MAX_VOICES; i++) {
    m_voiceArray[i]->m_ModulationMatrix;
    m_dSources[SOURCE_MIDI_PAN_CC10] = m_uMIDIPanCC10;
  }
}
break;
case MIDI_EXPRESSION_CC11: // want 0 to 127
{
  m_uMIDIExpressionCC11 = unipolarToMIDI(value);
  for (int i=0; i<MAX_VOICES; i++) {
    m_voiceArray[i]->m_ModulationMatrix;
    m_dSources[SOURCE_MIDI_EXPRESSION_CC11] = m_uMIDIExpressionCC11;
  }
}
break;
case MIDI_SUSTAIN_PEDAL: // want 0 to 1
{
  UINT uMIDI = value > 0.5 ? 127 : 0;
  for (int i=0; i<MAX_VOICES; i++) {
    m_voiceArray[i]->m_ModulationMatrix;
    m_dSources[SOURCE_SUSTAIN_PEDAL] = uMIDI;
  }
}
break;
```