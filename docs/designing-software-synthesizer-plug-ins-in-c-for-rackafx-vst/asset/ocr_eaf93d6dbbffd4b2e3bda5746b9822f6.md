```
// --- synth objects
#include "QBLimitedOscillator.h"
#include "WToscillator.h"
#include "LFO.h"
#include "EnvelopeGenerator.h"
#include "DCA.h"
#include "MoogLadderFilter.h"
```

```
class CNanoSynth : public CPlugIn
{
  public:
```

<SNIP SNIP SNIP>

```
// Add your code here:
CQBLimitedOscillator m_osc1;
CQBLimitedOscillator m_osc2;
CLFO m_LF01;
CEnvelopeGenerator m_EG1;
CDCA m_DCA;
```

```
// --- Moog LPF
CMoogLadderFilter m_Filter1;
```

```
void update();
```

etc...