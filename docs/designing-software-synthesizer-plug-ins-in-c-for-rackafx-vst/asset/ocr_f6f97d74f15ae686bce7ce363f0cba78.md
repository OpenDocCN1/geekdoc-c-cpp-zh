```
OSStatus AUSynth::StartNote(MusicDeviceInstrumentID inInstrument,
MusicDeviceGroupID inGroupID,
NoteInstanceID *outNoteInstanceID,
UInt32 offsetSampleFrame,
const MusicDeviceNoteParams &inParams)
{
```

```
<SNIP SNIP SNIP>

// --- set the note number in the mod matrix for filter key track
m_GlobalModMatrix.m_dSources[SOURCE_MIDI_NOTE_NUM] = uMIDiNote;

// for Vel-->Att scaling
m_GlobalModMatrix.m_dSources[SOURCE_VELOCITY] = uVelocity;

return noErr;
{
```

```
<SNIP SNIP SNIP>
update()
```

Here, polyphone-ize by setting all the voice parameters on all voices at once; only replace the synth update and not the modulation matrix code.

# process()

Remove the old code and add the new accumulating code with the voice steal code intact. Note that the outputs are now taken from the accumulators.

# startNote() and stealNote()

Implement the startNote() and stealNote() functions using the code listings.