The synthesizer's polyphony is accomplished by maintaining an array of voice object pointers. This array is named m_pVoiceArray for all the syns. The difference is in the kind of pointers they hold; in this case the array holds CMiniSynth pointers. The three functions below definition are for handling the time ordering of voices. The update() function is for updating all of the synth variables. We will get into the details of the remaining variables as the Chapters progresses.

```
CMiniSynth* m_pVoiceArray[MAX_VOICES];
void incrementVoiceTimestamps();
CMiniSynth* getDestVoice();
CMiniSynth* getDestVoiceWithNote(UINT uMIDNote);
// --- updates all voices at once
void update();

// --- for portamento
double m_dLastNoteFrequency;

// --- our receive channel
UINT m_uMidiRxChannel;
```

# 2.40 Implementing the AUSynth Object

Open the AUSynth.cpp file and examine its contents. This file is nearly identical for each synth. At the very top of the file, you see the definition of the preset names. We will use this to tell the host about our preset names during the function call GetPresets();

The code that follows is crucial to the plug-in's operation:

```
static const int numPresets = 1;
static AUSPreset presetNames[numPresets] = {

// --- (index, Preset Name)
// add more with commas

// (0, CFSTR("Factory Preset")),
// (1, CFSTR("Another Preset")) //<-- no more comma
(0, CFSTR("Factory Preset"))
};
```

AUDCOMPONENT_ENTRY (AUMusicDeviceFactory, AUSynth)

This is the entry-point into the dynamic-linked library. This line of code is the same for all synths. The syntax is:

AUDCOMPONENT_ENTRY (AUMusicDeviceFactory, ).