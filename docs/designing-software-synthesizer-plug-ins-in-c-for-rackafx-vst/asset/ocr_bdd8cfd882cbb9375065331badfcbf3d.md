# Table 8.1 is

```
CEnvelopeGenerator::CEnvelopeGenerator(void)
{
m_nSamplesRate = 44100;

<SNIP SNIP SNIP>

m_bResetToZero = false;
m_bLegatoMode = false;

// --- default modulation matrix inits
m_pModulationMatrix = NULL;

// -- everything is disconnected unless you use mod matrix
m_uModSourceEGAttackScaling = DEST_NONE;
m_uModSourceEGDecayScaling = DEST_NONE;
m_uModDestEGOutput = SOURCE_NONE;
m_uModDestBiasedEGOutput = SOURCE_NONE;
}
```

```
#include "ModulationMatrix.h"
```

```
#define AMP_MOD_RANGE -96 // -96 dB
```

class CDCA

```
{
public:
CDCA(void);
~CDCA(void);
```

```
// --- ATTRIBUTES
// --- PUBLIC: these variables may be get/set
// you may make get/set functions for them
// if you like, but will add function call layer
//
```