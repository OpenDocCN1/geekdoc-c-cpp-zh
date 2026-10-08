
necessary information to process one source into one destination.

The operations are:

- clear the destinations

```cpp
if(!m_ppMatrixCore) return false;

for(int i=0; i<m_nSize; i++) {
    modMatrixRow* pRow = m_ppMatrixCore[i];

    // find matching source/destination pairs
    if(pRow->uSourceIndex == uSourceIndex && pRow->uDestinationIndex == uDestinationIndex) {
        if (pRow->bEnable == bEnable) {
            return true; // found it
        }
    }
}
return false;
```

- loop through the matrix rows and:
  - get the matrix row pointer
  - check to see if row is enabled
  - check to make sure this is the proper destination to process (layer)
  - get the source value from the array
  - apply a transform if there is one
  - check the destination; if one of the Universal "ALL" types, process into all of them (notice that it also writes the value into the ALL slot as well), or just do a single source->destination if not

Notice the processing function is identical for all rows accumulating the scaled sources into the destinations:

The ModulationMatrix.cpp file houses the very simple constructor and destructor. Notice that the constructor allocates the matrix core, and the destructor does nothing—since the core will be shared it will be up to the global owner to delete the core.

## 8.3 Using and Programming the Modulation Matrix:

In all of our synths, the modulation matrix is a shared object; there is only one matrix per device. In NanoSynth, the plug-in object uses the modulation matrix programs by creating and filling its rows, then gives a pointer to the mod matrix object to each of the system components in the design. This will change slightly when we introduce

```cpp
inline bool checkDestinationLayer(UINT uLayer, modMatrixRow* pRow)
{
    bool bLayer0 = false;
    if(pRow->uDestinationIndex >= DEST_LF01_FO &&
        pRow->uDestinationIndex <= DEST_ALL_EG_SUSTAIN_OVERRIDE)
        bLayer0 = true;

    if(uLayer == 0)
        return bLayer0;

    if(uLayer == 1)
        return !bLayer0;

    return false;
}

destination += source*intensity*range
inline void doModulationMatrix(UINT uModLayer)
{
    if(!m_ppMatrixCore) return;

    // clear dest registers
    clearDestinations();

    for (int i=0; i<m_nSize; i++)
    {
        // get the row
        modMatrixRow* pRow = m_pModMatrix[i];

        // --- this should never happen
        if(!p) continue;

        // --- if disabled, skip row
```cpp
if(! pRow->bEnable) continue;
```

```cpp
// --- check the mod layer
if(!checkDestinationLayer(uModLayer, pRow)) continue;
```

```cpp
// get the source value
double dSource = m_dSources[pRow->uSourceIndex];
```

```cpp
switch(pRow->uSourceTransform) {
    case TRANSFORM_UNIPOLAR_TO_BIPOLAR:
        dSource = unipolarToBipolar(dSource);
        break;

case TRANSFORM_BIPOLAR_TO_UNIPOLAR:
        dSource = bipolarToUnipolar(dSource);
        break;

    <SNIP SNIP SNIP>
    default:
        break;
}
```

```cpp
// destination += source*intensity*range
//
```

```cpp
double dModValue = dSource*(pRow->pModIntensity)
    *(pRow->pModRange);
```

```cpp
// first check DEST_ALL types
switch(pRow->uDestinationIndex);
```

polyphony. Figure 8.9 shows a simplified connection diagram for NanoSynth, and a conceptual diagram showing the single modulation matrix and each component owning a pointer to it.

The matrix is programmed in two steps; first, each object must be told where in the Sources or Destinations array or write its modulation values. Then, the matrix rows are dynamically allocated and added to the matrix, then sets the

```cpp
case DEST_ALL_OSC_FO:
    m_dDestinations[DEST_OSC1_FO] += dModValue;
    m_dDestinations[DEST_OSC2_FO] += dModValue;
    m_dDestinations[DEST_OSC3_FO] += dModValue;
    m_dDestinations[DEST_OSC4_FO] += dModValue;
    m_dDestinations[DEST_ALL_OSC_FO] += dModValue;
    break;
```

<SNIP SNIP SNIP>

```cpp
// for all "single" source/dest, this is the modulation
default:

m_dDestinations[pRow->uDestinationIndex]
    += dModValue;
```

```cpp
CModulationMatrix::CModulationMatrix(void)
```

```cpp
// --- dynamic allocation of matrix core
m_ppMatrixCore = new modMatrixRow*[MAX_SOURCES*MAX_DESTINATIONS];
    memset(m_ppMatrixCore, 0, MAX_SOURCES*MAX_DESTINATIONS*
        sizeof(modMatrixRow));
```

```cpp
m_nSize = 0;
clearMatrix(); // fill with NULL

clearSources();
clearDestinations();
```

```cpp
CModulationMatrix::~CModulationMatrix(void)
```

![](img/b42d0dca53f4a889d8162d55f7c8c05d_478_0.png)

- amplitude (for Amplitude Modulation or AM)

Destinations (where we write our outputs):

- output 1 (for LFO this is the normal output; for pitched oscillators, it is the left output

- output 2 (for LFO this is the quad phase output; for pitched oscillators, it is the right output)

## "ModulationMatrix.h"

```cpp
#define OSC_FO_MOD_RANGE 2      //2 semitone default
#define OSC_HARD_SYNC_RATIO_RANGE 4  //4
#define OSC_PITCHBEND_MOD_RANGE 12 //12 Hz-wait, 12 semitone
#define OSC_FC_MIN 20                //20 Hz
#define OSC_FC_MAX 20480             //2048 kHz
#define OSC_ULSEWIDTH_MIN 2         //2%
#define OSC_ULSEWIDTH_MAX 98        //98%
```

```cpp
class CModulationMatrix {
public:
    CModulationMatrix(void);
    virtual ~CModulationMatrix(void);

    // shared matrix core
    modMatrixRow** m_ppMatrixCore;
    int m_nSize;

    void clearMatrix();
    void clearSources();
    void clearDestinations();
};
```

```cpp
class COscillator {
public:
    COscillator(void);
    virtual ~COscillator();

    // modulation matrix
    CModulationMatrix* m_pModMatrix;

    // sources we read from
    UINT m_uSourceFo;
    UINT m_uSourceWidth;
    UINT m_uSourceAmp;

    // destinations that we write to
    UINT m_uDestOutput1;
    UINT m_uDestOutput2;

    // oscillator run flag
    bool m_bNoteOn;

    virtual void updateOscillator();
};
```

Oscillator.cpp

You initialize the variables in the constructor. The modulation matrix pointer is NULL and is always optional in our objects. We know the matrix is used if this pointer is non-NULL.

## COscillator Derived Classes

```cpp
inline void updateOscillator()
{
    // --- ignore LFO mode for noise sources
    if(m_uWaveform == rsh || m_uWaveform == qrsh)
        m_uLFMode = free;
    
    // --- Modulation Matrix
    // --- get from matrix
    if (m_pModulationMatrix) {
        // --- zero for these
        m_dFMod = m_pModulationMatrix->m_Destinations[m_uSourceFo];
        m_dPWMod = m_pModulationMatrix->m_Destinations[m_uSourceWidth];
        // --- amp mod is 0->1
        // --- invert for oscillator output
        m_dAmpMod = m_pModulationMatrix->m_Destinations[m_uSourceAmp];
        m_dAmpMod = 1.0 - m_dAmpMod;
    }
}
```

```cpp
// --- do the complete frequency mod
m_dFo = m_d0scFo*m_dFoRatio*pitchShiftMultiplier(m_dFoMod +
    m_dPitchMod +
    m_noctave*12.0 +
    m_nSemitones +
    m_nC/100.0);
```

etc...

functionality. For the LFO, the destination outputs are normal and quad phase while the pitched oscillators write their outputs as left right pairs.

```cpp
COscillator::COscillator(void)
{
    // --- initialize variables
    m_dSampleRate = 44100;

    <SNIP SNIP SNIP>

    // --- for hard sync
    m_pBuddyOscillator = NULL;
    m_bMasterOsc = false;

    // --- default modulation matrix inits
    m_pModulationMatrix = NULL;

    // --- everything is disconnected unless you use mod matrix
    m_uSourceFo = DEST_NONE;
}
```

doOscillate() function to write outputs to the matrix Sources array:

m_uSourcePulseWidth = DEST_NONE;
m_uSourceAmp = DEST_NONE;
m_uDestOutput1 = SOURCE_NONE;
m_uDestOutput2 = SOURCE_NONE;
