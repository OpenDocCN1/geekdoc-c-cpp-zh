MiniSynth uses the following files that you will need to add into your compiler's project in the usual manner. You may also

```
// --- DIGITAL AUDIO ENGINE BLOCK ---
double d0scMix = 0.333*m_0sc1.dooscillate() +
0.333*m_0sc2.dooscillate() +
0.333*m_0sc3.dooscillate() +
m_0sc4.dooscillate();
```

```
// --- apply the filter
double LPFOut = m_MoogLadderFilter.doFilter(d0scMix);
```

```
// --- apply the DCA
m_DCA.doCA(dLPFOut, dLPFOut, dLeftOutput, dRightOutput);
```

```
return true;
```

download the complete project code from

<< ** Code Listing 9.1: Declarations ** >>

```
MiniSynthVoice* m_pVoiceArray[MAX_VOICES];
```

```
// -- MmM
ModulationMatrix m_GlobalModMatrix;
```

```
// --- global params
globalSynthParams m_GlobalSynthParams;
```

```
// -- helper functions for note on/off/voice steal
void incrementVoiceTimestamps();
MiniSynthVoice* getOldestVoice();
MiniSynthVoice* getOldestVoiceWithNote(UINT uMIDinNote);
```

http://www.willpirkle.com/synth/. The MiniSynth core consists of:

For VST3 and AU, you also need to add the file SynthParamLimits.h, which is in the MiniSynth sample code—remember that this file is slightly different for each synth because it contains the GUI control index enumeration.

# 9.8 MiniSynth: RackAFX

Create a new project named MiniSynth and setup the GUI using Table 9.5.

MiniSynth.h