# << << ** Code Listing 10.1: Declarations ** >>

MIDI Manufacturers Association. 1999. Downloadable Sounds Level 2, v1.0.

```
// --- our array of voices
CDigiSynthVoice* m_pVoiceArray[MAX_VOICES];
```

MIDI Manufacturers Association. 2006. Downloadable Sounds Level 2, Amendment 2.

```
// --- MMM
CModulationMatrix m_globalModMatrix;
```

sonicspot.com. n.d. "Wave File Format." Accessed June 2014,

```
// --- global params
globalSynthParams m_globalSynthParams;
```

```
// --- helper functions for note on/off/voice steal
void incrementVoiceTimestamps();
CDigiSynthVoice* getOldestVoice();
CDigiSynthVoice* getOldestVoiceWithNote(UINT uMIDINote););
```

```
// -- load sample sets
bool loadSamples();
```

```
// updates all voices at once
void update();
```

```
// // for portamento
double m_dLastNoteFrequency;
```

```
// our recieve channel
UINT m_uMidiRxChannel;
```

# << << END ** Code Listing 10.1: Declarations ** END >>

http://www.sonicspot.com/guide/wavefiles.html