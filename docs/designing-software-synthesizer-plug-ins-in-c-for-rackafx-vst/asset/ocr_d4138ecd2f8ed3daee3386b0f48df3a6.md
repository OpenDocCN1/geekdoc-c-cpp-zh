```
// --- one complete voice
struct nanoSynthVoice
{
    CQBLimitedOscillator m_Oscl;
    CQBLimitedOscillator m_Osc2;
```

```
CLFO m_LF01;
CEnvelopeGenerator m_EG1;
MoogLadderFilter m_Filter1;
CDCA m_DCA;
CModulationMatrix m_ModulationMatrix;
;
```

```
#define MAX_VOICES 2
```

```
class AUsynth : public AUInstrumentBase
(
```

```
<SNIP SNIP SNIP>

// Add your code here: ----------------/
// --- the Modulation Matrix
CModulationMatrix m_GlobalModMatrix;
```

```
nanoSynthVoice m_Voices[MAX_VOICES];
int m_nPendingMIDINote[MAX_VOICES];           // if -1 no pending note
int m_nPendingMIDIVelocity[MAX_VOICES];      // if -1 no pending velocity
```

```
void startNote(int nIndex, UINT uMIDINote, UINT uMIDIVelocity);
void stealNote(int nIndex, UINT uPendingMIDINote,
    uPendingVelocity);
```

```
etc...

```