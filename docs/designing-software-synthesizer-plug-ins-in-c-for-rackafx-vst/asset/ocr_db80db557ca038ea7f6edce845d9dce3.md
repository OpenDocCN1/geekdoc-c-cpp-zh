prepareForPlay() replace the old initialization code with the slightly altered version that places the detuning in a global

```
m_Voices[i].m_0sc2.m_uMIDINoteNumber = m_nPendingMIDINote[i];
m_Voices[i].m_0sc2.m_d0scFo = midifreqTable[m_nPendingMIDINote[i]];
```

```
m_Voices[i].m_0sc1.updateOscillator();
m_Voices[i].m_0sc2.updateOscillator();
```

```
// --- crank the EG up again
m_Voices[i].m_EG1.startEG();
```

```
// --- set the note # and velocity of newest note
m_Voices[i].m_ModulationMatrix.m_dSources
[SOURCE_MIDI_NOTE_NUM] = m_nPendingMIDINote[i];
m_Voices[i].m_ModulationMatrix.m_dSources
[SOURCE_VELOCITY] = m_nPendingMIDIVelocity[i];
```

```
// --- reset
m_nPendingMIDINote[i] = -1;
m_nPendingMIDIVelocity[i] = -1;
```

```
}
else{
m_Voices[i].m_0sc1.stopOscillator();
m_Voices[i].m_0sc2.stopOscillator();
m_Voices[i].m_LF01.stopOscillator();
m_Voices[i].m_EG1.stopEG();
}
```

parameter.
update()

Finally, knock out the update() function and replace the for() loop. Make sure to leave the modulation matrix code alone.

# 8.22 Final NanoSynth: VST3