# #define WT_LENGTH 512
#define NUM_TABLES 9

+   - use one
index for the
normal
sawtooth
and the
other for the

CWTOscillator::CWTOscillator(void)

```
// --- clear arrays

memset(m_psawTables, 0, NUM_TABLES*sizeof(double)*);
memset(m_pTriangleTables, 0, NUM_TABLES*sizeof(double)*);
```

```
// --- init variables
m_dReadIndex = 0.0;
d_dWT_inc = 0.0;
m_nCurrentTableIndex = 0.0;
```

```
// --- setup correction factors (empirical)
d_dSquareFactor[0] = 0.5;
d_dSquareFactor[1] = 0.5;
d_dSquareFactor[2] = 0.5;
d_dSquareFactor[3] = 0.49;
d_dSquareFactor[4] = 0.48;
```

```
m_dSquareFactor[5] = 0.468;
m_dSquareFactor[6] = 0.43;
d_dSquareFactor[7] = 0.34;
d_dSquareFactor[8] = 0.25;
```

inverted/shifted one

+   - use the square correction factor
- use the normal DC offset correction
- you can see that this function follows the same outline as the CQLimitedOscillator's square wave but uses the doWaveTable() helper function instead of doSawtooth

# doOscillator

+   - if square wave, can scale output amplitude
- if others, use doWaveTable() method

+   - output is monophonic so to copy any output if
needed
- uses same amplitude and amp mod scaling as all other oscillators

```
// --- SINE
m_nCurrentTable = &m_dSineTable[0];
```

CWTOscillator::CWTOscillator(void)

```
// --- destroy
destroyWaveTables();
```

# 5.34 NanoSynth Oscillators: Processing Code

The NanoSynth plug-in object will possess member variables and functions to implement the synth processing. All objects will define the:

```
// --- two
oscillators
```