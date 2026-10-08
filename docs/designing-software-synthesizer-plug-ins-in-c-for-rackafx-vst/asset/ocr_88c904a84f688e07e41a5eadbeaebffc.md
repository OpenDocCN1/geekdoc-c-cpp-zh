```
tresult PLUGIN_API process(ProcessData&
data);
```

+   - the audio rendering function

+   - also processes MIDI events and control changes

```
static FUnknown* createInstance(void*) { return (IAudioProcessor*)new Processor ();
}
```

+   - the COM creation function

```
static FUID
cid;
```

+   - the globally unique identifier for this object

In addition to these methods, we will also be declaring variables for each control on the GUI that will alter the synth's output. When we handle change controls, we will change the values of these variables accordingly, and then call an update method to set the variables in the synth object. If you look in the MiniSynth project's VSTSynth.h file, you can see the additional declarations. Don't worry about the first part involving the poly array; we will get to that in Chapter 8 when we use polyphony. We will discuss the doControlUpdate() and doProcessEvent() functions when we discuss the process() function.

The important part of the code for this section is the list of variables known as synth parameters or parameters. These are the variables that will directly affect the synth operation.

You need to declare a variable for each parameter setup in the Controller's initialize() method. Variables are named and listed in the GUI design table for each synth. You add those variables to Project object's .h file for each project. Then, only add variables that correspond to the dummy MIDI controls you set up in the Controller's initialize() method.

After these, you will set the dummy MIDI controller variables. The log filter is going to require some conversion when we are decoding control changes during the process() function. For this, we will create a special helper object, a Parameter that is the same way as the filter parameter you set in the Controller. It is named m_pFilterLogParam.

# Other Functions and Variables

The following functions are used to aid in polyphony. We will discuss these in detail in Chapter 8. They are used to implement dynamic voice allocation or voice-stealing. For now you can skip over them.

```
void
incrementVoiceTimestamps()
```

```
CMiniSynthVoice*
getOldestVoice()
```

```
CMiniSynthVoice* getOldestVoiceWithNote(UINT\uMIDINote)
```

```
bool doControlUpdate(ProcessData&
data);
```

+   - helper function for dealing with GUI control changes