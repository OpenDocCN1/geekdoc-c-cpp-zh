```
A bool __stdcall cNanoSynth::prepareForPlay()

```

```
<SNIP SNIP SNIP>
```

```
update();
```

```
// --- default turn on volume and center the pan
m_GlobalModMatrix.m_dSources[SOURCE_MIDI_VOLUME_CC07] = 127;
m_GlobalModMatrix.m_dSources[SOURCE_MIDI_PAN_CC10] = 64;
```

```
return true;
```

```
bool __stdcall cNanoSynth::midiNoteOn(UINT uChannel, UINT uMIDINote,
uuVelocity)
```

```
// test channel/ignore
if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
return false;
```

```
<SNIP SNIP SNIP>
```

```
// --- set the note number in the mod matrix for filter key track
m_ModulationMatrix.m_dSources[SOURCE_MIDI_NOTE_NUM] = uMIDINote;
```

```
// --- velocity routing
m_GlobalModMatrix.m_dSources[SOURCE_VELOCITY] = uVelocity;
```

```
return true;
```

```
bool __stdcall cNanoSynth::midiPitchBend(UINT uChannel,
intActualPitchBendValue,
float fNormalizedPitchBendValue
```

```
<SNIP SNIP SNIP>
```