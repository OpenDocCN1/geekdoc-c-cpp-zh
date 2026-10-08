```
void CMiniSynthVoice::initializeMatrix(CModulationMatrix* pMatrix)
(
  // --- always first: call base class to create core and
  // // init with basic routings
  CVoice::initializeMatrix(pMatrix);

  if (lpMatrix->getModMatrixCore()) return;
    // --- MiniSynth Specific Routings
    // // create a row for each source/destination pair
    modMatrixRow* pRow = NULL;
```

```
// // LFO01 -> ALL OSC1 FC
pRow = createModMatrixRow(SOURCE_LF01,
  DEST_ALL_OSC_FO,
  &_pGlobalVoiceParams->dLF010scModIntensity,
  &_pGlobalVoiceParams->d0scfModRange,
  true);
```

```
pMatrix->addModMatrixRow(pRow);
etetc..
```

+   - in for(i) loop,
  set each voice's modulation matrix core to the global modulation core using the set() function

```
void CMiniSynthVoice::setSampleRate(double dSampleRate)
  CVoice::setSampleRate(dSampleRate);
```

```
void CMiniSynthVoice::prepareForPlay()
  CVoice::prepareForPlay();
  reset();
```

# Destruction

Destruction is done in the destructor in RackAFX and AU, and in isActive() in VST3.
The code is nearly identical for every synth project; you delete the global modulation matrix,
then delete the voices.

# One Time Plug-in Initialization

The one-time initialization is done in:

+   - RackAFX: preparePlay()
- VST3: setActive()
- AU: Initialize()