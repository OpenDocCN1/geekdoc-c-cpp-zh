```
for(int i=0; i<MAX_VOICES; i++)
{
    m_Voices[i].m_ModulationMatrix.m_dSources
    [SOURCE_MIDI_PAN_CC10] = m_uMIDIPanCC10;
}

break;
}
case MIDI_ALL_NOTES_OFF:
{
    for(int i=0; i<MAX_VOICES; i++)
    m_Voices[i].m_EG1.note0ff();

    break;
}
case MIDI_SUSTAIN_PEDAL: // want 0 to 1
{
    bool bSus = value > 0.5 ? true : false;

    // LOG MIDI
// --- send to matrix poly
UINT uMIDI = unipolarToMIDI(value);
for(int i=0; i<MAX_VOICES; i++)
{
    m_Voices[i].m_ModulationMatrix.m_dSources
    [SOURCE_SUSTAIN_PEDAL] = uMIDI;
}

    break;
}
```