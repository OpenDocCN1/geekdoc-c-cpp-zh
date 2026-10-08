```
virtual inline double doOscillate(double* pAuxOutput = NULL)
(
    if(!m_bNoteOn)
        return 0.0;
)
```

```
double dOut = 0.0;
```

```
// always first
bool bWrap = checkWrapModulo();
```

```
// added for PHASE MODULATION
double dCalcModulo = m_dModulo + m_dPhaseMod;
checkWrapIndex(dCalcModulo);
```

```
switch(m_uWaveform)
(
    case SINE: // same as LFO

    case SAW1:
    case SAW2:
    case SAW3:
        dOut = doSawtooth(dCalcModulo, m_dInc);
```

```
// for square wave
double
dsoSquareWave();
```

We also need functions to create and destroy the tables, as well as choose the proper table based on current oscillator frequency.

```
// find the table with the proper number of harmonics for our
pitch
```

```
int
getTableIndex();

void
selectTable();
```

```
// create an destroy
tables
```

```
void
createWaveTables();

void
destroyWaveTables();
```

Lastly, we need to override the typical base class virtual functions plus the one for altering the sample rate, in which