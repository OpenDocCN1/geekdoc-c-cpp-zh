get to use them.

```
void WT0oscillator::createWaveTables()
```

# Note On

For the note
on event, we
eed to:

```
// create the tables
//
// SINE: only need one table
for(int i = 0; i < WT_LENGTH; i++)
{
// sample the sinusoid, WT_LENGTH points
// sin(wNT) = sin(2*pi*i/WT_LENGTH)\mdDSineTable[i] = sin((double)i/WT_LENGTH)*(2*pi));
}
```

+   - set the

```
// SAW, TRIANGLE: need 10 tables
double dSeedFreq = 27.5; // Note A0, bottom of piano
for(int j = 0; j < NUM_TABLES; j++)

double* pSawTable = new double[WT_LENGTH];
memset(pSawTable, 0, WT_LENGTH*sizeof(double));
```

```
double* pTTable = new double[WT_LENGTH];
memset(pTTable, 0, WT_LENGTH*sizeof(double));
```

```
int nHarms = (int)(m_dSampleRate/2.0/dSeedFreq) - 1.0;
int nHalfHarms = (int)((float)nHarms/2.0);

double dMaxSaw = 0;
double dMaxTri = 0;
```

```
for(int i = 0; i < WT_LENGTH; i++)
{
// sawtooth += (-1)^g+1(1/g)sin(wNT)
for(int g = 1; g <= nHarms; g++)
{
// Lanczos Sigma Factor
double x = g*pi/nHarms;
double sigma = sin(x)/x;

// only apply to partials above fundamental
if(g - 1)
sigma = 1 0;
```