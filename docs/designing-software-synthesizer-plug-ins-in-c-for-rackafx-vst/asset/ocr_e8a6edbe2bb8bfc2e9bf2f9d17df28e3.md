Interestingly, the process() method handles MIDI and control changes, in addition to processing. It is the most complicated of the methods and we will handle it. We are going to use a few helper functions to break down the complexity of this function.

```
case kCtrlAllNotesOff:
  id = MIDI_ALL_NOTES_OFF;
  break;
  return id != 0 ? kResultTrue : kResultFalse;
return kResultFalse;
```

# Core Plug-in Functions:

```
Processor();
```

+   - initialize all parameters
- initialize all MIDI controller dummy variables

result PLUGIN_API initialize(FUnknown* context);

+   - declare our input and output ports (audio and MIDI)

result PLUGIN_API setBusArrangements(SpeakerArrangement* inputs, int32 numIns, SpeakerArrangement* outputs, int32 numOuts);

+   - define which output arrangement supports (stereo output for all synths)

result PLUGIN_API processSampleSize(int32 symbolicSampleSize);

+   - declare the audio word-length(s) we support; currently this is 32-only

result PLUGIN_API setActive(TBool state);

+   - this is the on/offunction acts as the per-run initialization function
- set the sample rate on all sub-components
- clear out any per-run variables

result PLUGIN_API setState(IBStream* fileStream);

+   - serialize (read) to load the synth state from a preset file or startup file

result PLUGIN_API getState(IBStream* fileStream);

+   - serialize (write) to write the current synth state into