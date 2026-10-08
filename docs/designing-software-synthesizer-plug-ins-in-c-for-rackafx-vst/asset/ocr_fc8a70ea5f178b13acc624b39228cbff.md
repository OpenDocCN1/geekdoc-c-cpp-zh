double n = double(g);

```
pSawTable[i] += pow((float)-1.0,(float(g+1))*(1.0/n)
*sigma*sin(2.0*pi*i/WT_LENGTH);
```

```
// triangle: += (-1)g(1/(2g+1^2)sin(w(2n+1)T)
// NOTE: the limit is nHalfHarms here because of the way
//
// the sum is constructed (look at the (2n+1))
// components
for(int g = 0; g <= nHalfHarms; g++)
```

```
else {
double n = double(g);
priTable[i] += pow((float)-1.0,(float)n)
(1.0/pow((float))
(2*n + 1),(float)2.0))*sin(2.0*pi)
2.0*n + 1)*i/WT_LENGTH;
}
```

```
// store the max values
if(i - 0) {
dMaxSaw = pSawTable[i];
dMaxTri = pTriTable[i];
}
```

oscillator pitch
using the MIDI
note number to
the frequency
lookup table that
is declared in
synthfunctions.h
- update the
illator to
calculate the new
oscillator
frequency
variables

```
if(pSawTable[i] > dMaxSaw)
dMaxSaw = pSawTable[i];
if(pTriTable[i] > dMaxTri)
dMaxTri = pTriTable[i];
```

```
// normalize
for(int i - 0; i < WT_LENGTH; i++) {
  // normalize
```