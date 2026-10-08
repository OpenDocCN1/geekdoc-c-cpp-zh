The MIDI events function. In this events you decode and modify the voices voicingly. We will discuss the MIDI messages in the next chapter Chapter 8.

```
OSStatus::StartNote(MusicDeviceInstrumentID inInstrument, MusicDeviceGroupID inGroupID, NoteInstance *outNoteInstance, UInt32 inOffsetSampleFrame, const MusicDeviceNoteParams&params)
```

StartNote() is the MIDI note on message handler. The MusicDeviceNoteParams is a structure that holds the MIDI number and velocity of the note.

```
MIDI Note Number =
inParams.mPitch
```

```
MIDI Note On Velocity =
inParams.mVelocity
```

The mPitch variable is a floating-point number. Normally it will be integer in nature. If it has a fractional portion, this will represent a global tuning offset, so mPitch = 60.75 would be MIDI note 60 (middle C) + 75 cents of pitch offset. In the synths that we will be ignoring global tuning, we simply cast this as an unsigned integer. As a challenge, you can implement global tuning in your synths.

```
OSStatus::StopNote(MusicDeviceGroupID inGroupID, NoteInstanceinInstanceID, UInt32 inOffsetSampleFrame)
```

StopNote() is the MIDI note offset handler. The MIDI note of the released note is in the NoteInstanceOf variable, which is an unsigned integer. We use this note to help find the voice to turn off.

# MIDI Pitch Bend

The MIDI Bend messages arrive via the HandlePitchWheel() function. We just decode the value and set it in the synth's voices.

```
OSStatus::HandlePitchWheel(Int8 inChannel, UInt8 inPitch1, UInt8 inPitch2, UInt32 inStartFrame)
```

# MIDI Controller Messages

MIDI Continuous Controller (CC) messages arrive via HandleControlChange() and our synths support many including volume, pan, expression, and wheel sustain pedal.

```
OSStatus::HandleControlChange(UInt8 inChannel, UInt8 inController, UInt8 inValue, UInt32 inStartFrame)
```

# Other MIDI Messages

HandleMidiEvent allows you to receive all the other MIDI messages. We will trap program change, polyphonic and channel after messages in the synths in this book, but you are encouraged to experiment with other MIDI functionality, as master tuning and MIDI clock synchronization.

```
OSStatus::HandleMidiEvent(UInt8 status, UInt8 channel, UInt8 data, data2, UInt32 inStartFrame)
```

GetPropertyInfo is where we answer queries from the host about other non-standard properties we handle. This involves setting the size of the output variable and then calling the base class. For the most part, you can ignore