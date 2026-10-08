
![](img/b42d0dca53f4a889d8162d55f7c8c05d_602_0.png)

Figure 9.5: The Sequential Circuits Prophet VS voice architecture—this is the basis for Chapter 11’s VectorSynth, where we will discuss its unique Vector Mix Envelope Generator.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_602_1.png)

Figure 9.6: The Korg H.I. voice architecture from the Triton and Karma; here Korg calls a sub-voice “OSC,” which consists of oscillators, filter, LFOs, EGs, and DCA—two OSCs make up a single voice.

## CVoice Sub-Components

![](img/b42d0dca53f4a889d8162d55f7c8c05d_603_0.png)

Figure 9.7: CVoice is a collection of synth objects that you connect to make a voice; patch programming is done via the modulation matrix, and the object uses global parameters for adjusting component attributes.

```cpp
class CVoice {
public:
    CVoice(void);
    virtual ~CVoice(void);

    // NOTE: public; this is shared by sources and destinations
    CModulationMatrix m_ModulationMatrix;

protected:
    // --- 4 oscillators
    COscillator* m_p0sc1;
    COscillator* m_p0sc2;
    COscillator* m_p0sc3;
    COscillator* m_p0sc4;

    // --- 2 filters; 2 mono or 1 stereo
    CFilter* m_pFilter1;
    CFilter* m_pFilter2;

    // --- 4 EGs
    CEnvelopeGenerator m_EG1;
    CEnvelopeGenerator m_EG2;
    CEnvelopeGenerator m_EG3;
    CEnvelopeGenerator m_EG4;

    // --- 2 LFOs
    CLFO m_LF01;
    CLFO m_LF02;

    // --- 1 DCA (can be mono or stereo)
    CDCA m_DCA;
};
```

The LFOs, EGs and DCA are simply static declarations since they don't vary. In the Constructor, all pointers (oscillators, filters and global parameters) are nul out, which disables them. Deriving new classes and setting up their components is up to you.

// --- global parameters
```cpp
globalVoiceParams* m_pGlobalVoiceParams;
globalSynthParams* m_pGlobalSynthParams;
```

declare the oscillators and filters that are specific to the new voice and initialize the pointers in the derived class Constructor. Since MiniSynth [is an] analog modeling, we use the following components:

- Oscillators: Quasi-bandlimited (COBLimitedOscillator)
- Filter: Moog ladder filter in fourth order LPF configuration (CMoodLadderFilter)

Therefore, the declaration for the MiniSynthVoice object looks like this:

The objects are connected to the pointers in the constructor:

```cpp
class MiniSynthVoice : public CVoice {
    public:
        CMiniSynthVoice(void);
        ~CMiniSynthVoice(void);
```

The CVoice object will test the oscillator and filter before using them, so setting the second filter pointer to NULL disables it. If you decided later to change the oscillators to CWaveTable and the filter to CDiodelFilter, you just change the declarations in the .h file and everything else is done automatically. Notice that the filter is named m_LadderFilter as a reminder of its type, however you might choose m_Filter1 or like to make switching objects easier in your designs.

The CVoice object contains all necessary member variables and functions for basic voice operation. Table 9.1 lists the member variables and functions. Don't be intimidated by the number of variables—the derived classes, where you do most of the coding, are simple in comparison. Notice that the CVoice base class is set up for hard sync operation with the addition of a single parameter m_dRatio—this was a challenge from Chapter 5. If you are experimenting with hard sync, you can use this built-in variable; it is not used in the MiniSynth project.

```cpp
// Four oscillators
COBLimitedOscillator m_0sc1;
COBLimitedOscillator m_0sc2;
COBLimitedOscillator m_0sc3; // sub-osc
COBLimitedOscillator m_0sc4; // noise
```

Table 9.1: CVoice member variables and functions.

```cpp
// --- 1 filter
MoogLadderFilter m_MoogLadderFilter;
CMiniSynthVoice::CMiniSynthVoice(void) {
    // --- oscillators
    m_0sc1 = &m_0sc1;
    m_0sc2 = &m_0sc2;
    m_0sc3 = &m_0sc3;
    m_0sc4 = &m_0sc4;
```

Many of the variables and functions should be familiar to you, having worked through in the chapters. You can use some duplications for the sub-components and some initialization functions that are self-explanatory. The CVoice object points to the global synth parameter, which is a generalized version of the globalNanoSynthParams that you saw in the last chapter. You can see that.

```cpp
// --- filters
m_pFilter1 = &m_MoogLadderFilter;
m_pFilter2 = NULL;
```

The CVoice object will test the oscillator and filter before using them, so setting the second filter pointer to NULL disables it. If you decided later to change the oscillators to CWaveTable and the filter to CDiodelFilter, you just change the declarations in the .h file and everything else is done automatically. (Repeated context context)

![](img/b42d0dca53f4a889d8162d55f7c8c05d_605.png)

## CVoice Member Variables

| Type | Variable Name | Description |
| :--- | :--- | :--- |
| COscillator* | m_p0sc1 | oscillator1 |
| COscillator* | m_p0sc2 | oscillator2 |
| COscillator* | m_p0sc3 | sub-osc |
| COscillator* | m_p0sc4 | noise |
| CFilter* | m_pFilter1 | filter1 |
| CFilter* | m_pFilter2 | filter2 |
| CEnvelopeGenerator | m_EG1 | EG1 |
| CEnvelopeGenerator | m_EG2 | EG2 |
| CEnvelopeGenerator | m_EG3 | EG3 |
| CEnvelopeGenerator | m_EG4 | EG4 |
| CLFO | m_LF01 | LFO1 |
| CLFO | m_LF02 | LFO2 |
| CDCA | m_DCA | DCA |
| CModulationMatrix | m_ModulationMatrix | modulation matrix |
| globalVoiceParams* | m_pGlobalVoiceParams | global voice params |
| globalSynthParams* | m_pGlobalSynthParams | global synth params |
| float | m_dRatio | hard sync ratio |

## CVoice Member Functions

| Function Name | Description |
| :--- | :--- |
| clearDestinations | clears the mod destination array |
| isVoiceDone | returns true if output EGFs are in the off state |
| InlegatoMode | returns true if output EGFs are in legato mode |
| setSampleRate | distributes sample rate to all sub-components |
| prepareForPlay | one-time initialization; occurs after sub-component construction |
| enableModMatrix | enables or disables an existing routing for flexible routing |
| update | update new voice parameters |
| reset | reset all sub-components |
| noteOn | forms basic note on operations |
| noteOff | forms basic note off operations |
| doVoice | forms basic rendering, including voice stealing |

## CVoice Initialization

NanoSynth was fairly straightforward to put together

```cpp
struct globalSynthParams {
    glVoiceParams voiceParams;
    globalOscillatorParams osc1Params;
    globalOscillatorParams osc2Params;
    globalOscillatorParams osc3Params;
    globalOscillatorParams osc4Params;
    globalOscillatorParams l1foParams;
    globalOscillatorParams l2foParams;
    globalFilterParams filter1Params;
    globalFilterParams filter2Params;
    globalEGParams eg1Params;
    globalEGParams eg2Params;
    globalEGParams eg3Params;
    globalEGParams eg4Params;
    globalDCAPar dcaParams;
}
```

In .cpp file, you can see that the constructor just initializes the member variables and nulls out all pointers. Notice the family setup on the default initialization and range variables. The oscillator are declared in oscillator.h.
