```
CQBLimitedOscillator m_0sc;
CQBLimitedOscillator m_0sc2;
CLFO m_LFO1;
CEnvelopeGenerator m_EG1;
CMoogLadderFilter m_Filter1;
CDCA m_DCA;
CModulationMatrix m_ModulationMatrix;
```

);

```
#define MAX_VOICES 2
```

class Processor : public AudioEffect

{

```
<SNIP SNIP SNIP>
```

```
// Add your code here: //
// --- the Modulation Matrix
CModulationMatrix m_GlobalModMatrix;
```

nanoSynthVoice m_Voices[MAX_VOICES];

```
int m_nPendingMIDINote[MAX_VOICES]; // if -1 no pending note
int m_nPendingMIDIVel[MAX_VOICES]; // if -1 no pending velocity
```

```
void startNote(int nIndex, UINT uMIDINote, UINT uMIDIVelocity);
void stealNote(int nIndex, UINT uPendingMIDINote,
UINT uPendingVelocity);
```

etc...

}