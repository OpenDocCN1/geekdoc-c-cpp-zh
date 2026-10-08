# # "ModulationMatrix.h"

```
#define OSC_FO_MOD_RANGE 2      //2 semitone default
#define OSC_HARD_SYNC_RATIO_RANGE 4  //4
#define OSC_PITCHBEND_MOD_RANGE 12  //12 semitone default
#define OSC_FC_MIN 20                //20 Hz
#define OSC_FC_MAX 20480             //20.480 kHz - 10 octaves up from 20 Hz
#define OSC_PULSEWIDTH_MIN 2         //2%
#define OSC_PULSEWIDTH_MAX 98         //98%
```

```
class COscillator {
public:
    COscillator(void);
    virtual ~COscillator(void);

    // -- Modulation Matrix --
    //
    // the shared modulation matrix
    CModulationMatrix* m_pModulationMatrix; // the matrix

    // sources that we read from
    // indexes in m_pModulationMatrix->Sources[]
    UINT m_uModSourceFo;
    UINT m_uModSourcePulseWidth;
    UINT m_uModSourceAmp;

    // -- destinations that we write to
    // indexes in m_pModulationMatrix->Destinations[]
    UINT m_uModDestOutput1;
    UINT m_uModDestOutput2;
    //
```

```
    // -- oscillator run flag
bool m_bNoteOn;
```

update() function so that it picks up the modulation values from the matrix. Notice how the Amp Mod value is inverted:

# Oscillator.cpp

You initialize the variables in the constructor. The modulation matrix pointer is NULL and is always optional in our