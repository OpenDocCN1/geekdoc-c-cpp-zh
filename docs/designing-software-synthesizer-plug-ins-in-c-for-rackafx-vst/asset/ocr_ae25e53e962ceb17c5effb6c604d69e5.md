userInterfaceChange() you normally first decode the control's index (passed via the nControlIndex argument) and then call the appropriate updating function or calculation based on that. In our RackAFX synth projects (as well as the VST3 and AU versions), we will be a brute-force update of all variables if only one of them has changed. This is mainly due to greatly simplify the code. After characterization testing, we found that the added overhead of the full update did not appreciably affect the CPU load; the updating function turns out to be quite inexpensive compared to the actual audio synthesis itself. However, you are encouraged to change this paradigm and decode each control individually after you have completed the sync up running. To facilitate decoding, RackAFX leaves a comment above the userInterfaceChange function to remind you of the index mapping.

```
/* ADDED BY RACKAFX -- DO NOT EDIT THIS CODE!!! /
**--0x2983--**

Variable Name Index
m_uVoiceMode 0
m_dDetune_cents 1
m_dFcControl 2
m_dLF01Rate 3

etc...
**--0xFFDD--**
n// ... */
// Add your UI Handler code here
//
bool _stdcall CMiniSynth::userInterfaceChange(int nControlIndex)
{
    // --- just update all, ignoring the index value
    update();
    return true;
}
```

# MIDI Message Functions and Helpers

The last block of functions all concern MIDI messages. The nice thing is that with the exception of the type of voice pointer our array holds, all the MIDI functions for all the synth projects are identical, so once you've grasped it you can copy and paste for the rest.

# MIDI Note Timestamp Functions

There are three functions to help with polyphony.

```
void CMiniSynth::incrementVoiceTimestamps()
```