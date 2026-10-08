
ParameterInfo() is called once for each parameter, and here is where the aforementioned helper function comes into play. After checking to make sure you are initializing Global parameters, you decode the ParameterID (index) and call the helper function to complete the operation. If the result is not found, you return an error code.

```
ComponentResult AUSynth::GetParameterInfo(AudioUnitScope inScope,
AudioUnitParameterID inParameterID,
AudioUnitParameterInfo& outParameterInfo)
// --- we only handle Global params
if (inScope != kAudioUnitScope_Global)
return kAudioUnitErr_InvalidScope;
//setUPParameterInfo(outParameterInfo, CFSTR("Noise Osc"),
CFSTR("dB"), MIN_NOISE_OSC_AMP_DB,
MAX_NOISE_OSC_AMP_DB,
DEFAULT_NOISE_OSC_AMP_DB);
return noErr;
break;
case PULSE_WIDTH_PCT:
setUPParameterInfo(outParameterInfo, CFSTR("Pulse Width"),
CFSTR("%%"), MIN_PULSE_WIDTH_PCT,
MAX_PULSE_WIDTH_PCT,
DEFAULT_PULSE_WIDTH_PCT);
return noErr;
```

## SetAUParameterStringList()

Another helper function is used to facilitate setting the string list controls. This function is called SetAUParameterStringList() and simply creates an array from a comma-delimited string.

```
break;

etc...

return kAudioUnitErr_InvalidParameter;

void AUSynth::setAUParameterStringList(CFStringRef stringList
```

## GetParameterValueStrings()

In GetParameterValueStrings(), you declare the sets of strings that will populate the control using the helper function. After checking the scope, you declare the ParameterID and set the string list. Notice the last cluster of parameters, which are all ON/OFF 2-state switch variables.

## update()

In the update(), we loop through the voices and update all parameters at once. Unless we override SetParameter() functions, we won't know which (if) changed from one buffer to the next, so a brute update is done; this also matches the other synths. The updates require surprisingly little overhead, but you can always make this more efficient if you use. Notice how you retrieve your parameter using Globals()->Get() passing the index as argument.

## Render()

The all-important Render() function does three things:

- 1. broadcasts received MIDI events
- 2. updates the synth voices
- 3. synthesizes the audio

The MIDI events are updated using a base class function PerformEvents(), and then an update of the synth voices AU uses buffer processing. In the render operation here, you follow a similar strategy as VST3, which is to update the synth voices only once during the whole processing block. As a Challenge, you may try to interleave controls into the buffer processing. You retrieve your buffers by accessing the output buffer of the plug-in (Scope = output, Element = 0) and getting its buffer-list. This is an array of pointers to buffers. The first pointer is for the first channel and the second is for the right. We only support mono or stereo, so we first check the number of buffers. pointers to your buffers are at:

```
ComponentResult AUSynth::GetParameterStrings(AudioUnitScope inscope)
AudioUnitParameterID
inParameterID,
CFArrArrayRef* outStrings)
```

```
{
  if(inscope == kAudioUnitScope_Global)
  {
    if (outStrings == NULL)
      return noErr;
    // --- decode the ID value and set the string list:
    switch(inParameterID)
      {
        case VOICE_MODE:
          setParameterStringList(CFSTR("3Saw,3Sqr,2Sqr,2TriSaw,2TriSqr"), outStrings);
          return noErr;
          break;
      }
  }
  etc...
  // --- all are OFF,ON 2-state switches
```

bufferList.mBuffers[0].mData However, the mData member is actually void, so you have to cast it to a float to use it. The rest of the operation is straightforward: you loop through the number of frames (samples in each buffer) and accumulate the voices. Then, you write the result into the output buffers. We will discuss the doVoice() loop in Chapter 8.

```
OSStatus AUSynth::Render(AudioUnitRenderActionFlags& ioActionFlags, const
AudioTimeStamp& inTimestamp, UInt32 inNumberFrames)
```

First, broadcast MIDI events and then a synth voice update.

```
// --- broadcast MIDI
events PerformEvents(inTimestamp)
// --- do the mass update for this frame
update();
```

Next, get

```
case RESET_TO_ZERO:
case FILTER_KEYTRACK:
case VELOCITY_TO_ATTACK:
case NOTE_NUM_TO_DECAY:
{
    setAParameterStringList(CFSTR("OFF,ON"),
    outStrings);
    return noErr;
    break;
}

return kAudioUnitErr_InvalidParameter;
```

pointers to the buffers and setup the processing loop. This is the

```
// --- get the number of channels
AudioBufferList& bufferList = GetOutput(0)->GetBufferList();
Uint32 numChans = bufferList.mNumberBuffers;
```

```
// --- we only support mono/stereo
if(numChans > 2) return kAudioUnitErr_FormatNotSupported;
```

```
// --- get pointers to the buffers
float* left = (float*)bufferList.mBuffers[0].mData;
float* right = numChans > 1 ? (float*)bufferList.mBuffers[1].mData : NULL;
```

However, the mData member is actually void, so you have to cast it to a float to use it. The rest of the operation is straightforward: you loop through the number of frames (samples in each buffer) and accumulate the voices. Then, you write the result into the output buffers. We will discuss the doVoice() loop in Chapter 8.

```
// --- the processing loop
for (Uint32 frame = 0; frame < inNumberFrames; frame++)
{
    float sample = 0;
    // ... accumulate voices ...
    if(left) left[frame] = sample;
    if(right) right[frame] = sample;
}
```

The MIDI events are updated using a base class function PerformEvents(), and then an update of the synth voices AU uses buffer processing. In the render operation here, you follow a similar strategy as VST3, which is to update the synth voices only once during the whole processing block. As a Challenge, you may try to interleave controls into the buffer processing.

```
// The mPitch variable is a floating-point number. Normally it will be integer in nature. If it has a fractional portion, this will represent a global tuning offset, so mPitch =60.75 would be MIDI note 60 (middle C) + 75 cents.
```

The MIDI events are updated using a base class function PerformEvents(), and then an update of the synth voices AU uses buffer processing. In the render operation here, you follow a similar strategy as VST3, which is to update the synth voices only once during the whole processing block.
