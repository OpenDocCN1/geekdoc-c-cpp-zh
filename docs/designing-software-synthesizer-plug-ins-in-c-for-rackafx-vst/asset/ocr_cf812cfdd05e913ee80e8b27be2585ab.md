The next three functions are to help with polyph-nony.

```
double dLeftAccum = 0.0;
double dRightAccum = 0.0;
```

```
float fMix = 0.25; // -12db HR per note
```

```
// -- the frame processing loop
(Uint32 frame=0; frame<inNumberFrames; ++frame)
{
// -- zero out for each trip through loop
dLeftAccum = 0.0;
dRightAccum = 0.0;
double dLeft = 0.0;
double dRight = 0.0;
```

```
// -- synthesize and accumulate each note's sample
// detailed in future chapters
```

```
// -- accumulate in output buffers
// -- mono
left[frame] = dLeftAccum;
```

```
// -- stereo
if(right) right[frame] = dRightAccum;
```

```
}
return noErr;
}
```

```
void AUSynth::incrementVoiceTimestamps()
```

```
CMiniSynthVoice*
AUSynth::getOldestVoice()
```

```
CMiniSynthVoice* AUSynth::getOldestVoiceWithNote (UINT\uMIDINote)
```

We will discuss these detail in Chapter 8. They are used to implement dynamic voice allocation or voice-stealing.

# MIDI Note on and off