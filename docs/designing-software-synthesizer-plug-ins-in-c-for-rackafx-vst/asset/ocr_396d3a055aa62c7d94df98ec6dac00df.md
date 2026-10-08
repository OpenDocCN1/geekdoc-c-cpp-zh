+   • none

```
#include "ModulationMatrix.h"

// 46.8817993634 semitones = semitonesBetweenFrequencies(80, 18000.0)/2.0
#define FILTER_FC_MOD_RANGE 46.881799364656880
#define FILTER_FC_MIN 80                   // 80 Hz
#define FILTER_FC_MAX 18000              // 18 kHz

class CFilter{
public:
    CFilter(void);
    ~CFilter(void);

    // --- Modulation Matrix ---
    //
    // -- the shared modulation matrix
    CModulationMatrix* m_pModulationMatrix;

    // -- sources that we read from
    //
    indexes in m_pModulationMatrix->Sources[]
    UINT m_uModSourceFc;

UINT m_uSourceFcControl; // direct control over Fc, for key-track mode
//

    // -- the user's cutoff frequency control position
    double m_dfcControl;

    etc...
```

# Filter.cpp

Like the oscillator, you just initialize the variables in the constructor. The modulation matrix pointer is NULL and is always optional in our objects. The default connections are DEST_NONE.