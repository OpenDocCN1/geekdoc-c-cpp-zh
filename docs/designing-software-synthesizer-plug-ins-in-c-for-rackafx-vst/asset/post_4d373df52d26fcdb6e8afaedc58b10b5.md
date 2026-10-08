
The plug-in object will own the master modulation matrix and share it with the synth components. In this version of //

```cpp
// --- default modulation matrix inits
m_pModulationMatrix = NULL;

// --- everything is disconnected unless you use mod matrix
m_uModSourceEG = DEST_NONE;
m_uModSourceAmp_dB = DEST_NONE;
m_uModSourceVelocity = DEST_NONE;
m_uModSourcePan = DEST_NONE;
```

NanoSynth, it shares the object in its entirety— // need these for mod matrix the core, source and destination arrays.
double m_dDefaultModIntensity; // 1.0 polyphonic synths, the plug-in will only share
double m_dDefaultModRange; // 1.0 the matrix core. In all plug-ins, the
double m_d0scFoModRange; // variable modulation is declared and named the same in the object's .h file
m_dFilterModRange; // variable

CModulationMatrix m_GlobalModMatrix;

You program the matrix by creating modulationRows and adding them to the core array. You need to create one row for every source/destination your synth feature; there is enough room in the matrix for every possible connection combination (about 4,000 bytes in total). You decode the rows in the modulation table and convert each one into two lines of C++ code that create the row, and add it to the matrix. Examine Table 8.3 and the code below to make sure you understand how the rows are converted to code.

** Code Listing 8.1: Mod Matrix Routings I **

Table 8.3: NanoSynth mod matrix table

| NanoSynth Modulation Matrix | Destination/Intensity | Transform/Range | enabled |
| --- | --- | --- | --- |
| SOURCE_LFO1 | DEST_ALL_FO | TRANSFORM_NONE | TRUE |
| | | m_dDefaultModIntensity | m_d0scFoModRange | |
| SOURCE_BIASED_EG1 | DEST_ALL_FO | TRANSFORM_NONE | TRUE |
| | | m_dEG1OscIntensity | m_d0scFoModRange | |
| SOURCE_BIASED_EG1 | DEST_ALL_FILTER | TRANSFORM_NONE | TRUE |
| | | m_dDefaultModIntensity | m_dFilterModRange | |
| SOURCE_EG1 | DEST_CA_EG1 | TRANSFORM_NONE | TRUE |
| | | m_dEG1OscIntensity | m_dDefaultModRange | |
| SOURCE_MIDIE_NOTE_NUM | DEST_ALL_FILTER_KEYTRACK | TRANSFORM_NONE | TRUE |
| | | NUMBER_TO_FREQUENCY | m_dFilterKeyTrackintensity |

After loading the core with the matrix rows, you then initialize the range // --- The mod matrix "wiring" for DEFAULTS for all synths * variables and set up the individual synth components with a pointer to the master modulation matrix. Examine Code Listing 8.2 carefully and notice the initialization of the components'

```cpp
// create a row for each source/destination pair
modMatrixRow pRow = NULL;
```

```cpp
// LF01 -> ALL OSC1 FC
pRow = createModMatrixRow(SOURCE_LF01,
  DEST_ALL_OSC_FO,
  &m_DefaultModIntensity,
  &m_d0scFomModRange,
  TRANSFORM_NONE,
  true); // enabled;
```

```cpp
m_GlobalModMatrix.addModMatrixRow(pRow);
```

```cpp
// EG1 -> ALL OSC1 FC
pRow = createModMatrixRow(SOURCE_BIASED_EG1,
  DEST_ALL_OSC_FO,
  &m_dEG1OscIntensity,
  &m_d0scFomModRange,
  TRANSFORM_NONE,
  true); // enabled;
```

```cpp
m_GlobalModMatrix.addModMatrixRow(pRow);
```

```cpp
// EG1 -> FILTER1 FC
pRow = createModMatrixRow(SOURCE_BIASED_EG1,
  DEST_ALL_FILTER_FC,
  &m_DefaultModIntensity,
  &m_dFilterModRange,
  TRANSFORM_NONE,
  true); // enabled!
```

```cpp
m_GlobalModMatrix.addModMatrixRow(pRow);
```

```cpp
// EG1 -> DCA EG
pRow = createModMatrixRow(SOURCE_EG1,
  DEST_DCA_EG,
  &m_dEG1DCAIntensity,
  &m_dDefaultModRange,
  TRANSFORM_NONE,
  true); // enabled

m_GlobalModMatrix.addMatrixRow(pRow);
```

```cpp
// NOTE NUMBER -> FILTER Fc CONTROL
pRow = createModRow(SOURCE_MIDI_NUM,
  DEST_ALL_FILTER_KEYTRACK,
  &m_dFilterKeyTrackIntensity,
  &m_dDefaultModRange,
  TRANSFORM_NOTE_NUMBER_TO_FREQUENCY,
  true); // enabled!

m_GlobalModMatrix.addMatrixRow(pRow);
```

<< END ** Code Listing 8.1: Mod Matrix Routings I ** END >>

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

Study these initializations carefully, and you will see the paradigm here: the "destinations" are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

```cpp
m_Filter1.uModDest =
SOURCE_FO1;
```

# Enabling and Disabling Rows

Enabling and disabling a routing is easy; just notice the matrix-wiring to the matrix. This version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

```cpp
m_Filter1.uModDest =
SOURCE_FO1;
```

# doModulationMatrix() Function

The argument for doModulationMatrix() is the layer index. Even though we have Layer 0 modulators, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

m_PModulationVariable. Then, look at the default source and destinations for each component: these are going to be the same for all synths in the body, so we only examine it in detail here. For this version of NanoSynth, DCA has only one connection to the EG and nothing else. That will change as we develop NanoSynth further in the chapter.

```cpp
m_Filter1.uModDest =
SOURCE_FO1;
```

# NanoSynth MM Part One: RackAFX

Copy the ModulationMatrix.h and .cpp files into your project folder and add them into the Visual Studio project.

```cpp
// -- ARTICULATION BLOCK --
// -- DO layer 0 modulators
m_GlobalModMatrix.doModulationMatrix(0);
```

```cpp
// -- update layer 1 modulators
m_EG1.update();
```
