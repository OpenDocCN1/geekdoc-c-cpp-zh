```
// --- get
path
char* componentFolder =
getMyComponentDirectory(CFSTR("developer.audiounit.yourname.digisynth"));
char* pPath =
addStrings(componentFolder,"/MultiSamples/Flatty");
```

With the path established, the code is identical in each API to initialize the oscillators:

```
// --- init
pampleOsc->initWithFolderPath(pPath);

// --- delete delete
path
delete []
pPath;
```

# 10.8 DigiSynth Specifications

The architecture for DigiSynth is nearly identical to that of MiniSynth, making it easy for you to re-use your GUI and other coding. The only differences are that DigiSynth uses two oscillators instead of four, each oscillator has an amplitude control, there is no pulse width control, it uses split and layer voice modes and it has a loop mode you can play with. The loop mode allows you to experiment with different looping files. Figure 10.9 shows the simplified block diagram and Figure 10.10 shows the detailed connection graph. One thing is apparent in both is that the oscillators are stereo and require two filters, for each channel. The oscillators and filters chosen for the design are:

Oscillators: two CSampleOscillators
Filters: two CSEMFilters, one for left and another for right, NLP engaged (ON)

# noteRegion

The noteRegion structure contains the note and velocity range information for a note region. DigiSynth needs a note region structure for each oscillator. The default range settings are shown in Figure 10.1. Notice that they overlap both velocity and note ranges.