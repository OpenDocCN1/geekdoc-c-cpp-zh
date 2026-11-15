# ## 6.21.5 Conversion functions

Functions are provided for converting one datatype to another. These all have the prefix ajCvt. To interconvert polar and cartesian coordinates, to convert radians to degrees or return a probability given a Gaussian distribution use:

```
float ajCvtDegToRad (float degrees);
void ajCvtPolToRec (float radius, float angle, float* Px, float* Py);
float ajCvtRadToDeg (float radians);
void ajCvtRecToPol (float x, float y, float* Pradius, float* Pangle);
double ajCvtGaussToProb (float mean, float sd, float score);
```

Sequence positions are often specified by the user on the command line. EMBOSS supports negative values for sequence positions which are interpreted as an offset from the _end_ of the sequence. Two functions are provided to convert an EMBOSS sequence position to a true position which, for instance, could be used to index into the sequence itself. The functions return an integer between 0 (the start of the sequence) and the length of the sequence minus 1:

```
ajint ajCvtSposToPos (ajint len, ajint ipos);
ajint ajCvtSposToPosStart (ajint len, ajint imin, ajint ipos);
```

In both cases, len is the length of the sequence and ipos is the position. A value of 0 means the start of the sequence whereas negative numbers indicate an offset from the end of the sequence. A minimum relative position (imin) can be specified.

# ## 6.21.6 Random number functions

There are three functions for random number generation. These are based on dprand and sdprand and used with the permission of N. M. Maclaren (Copyright, The University of Cambridge). ajRandomSeed initialises random number generation and must be called before ajRandomNumber (returns a random integer between 0 and 32767) and ajRandomDouble (returns a random double-precision value between 0.0 and 1.0):

```
void ajRandomSeed (void);
double ajRandomNumber (void);
double ajRandomDouble (void);
```

# ## 6.21.7 Rounding

Two functions are for rounding off numbers, either a float to an int or a float to a float with a specified number of bits left for cumulative addition:

```
ajint ajRound (ajint i, ajint round);
float ajRoundFloat (float f, ajint nbits);
```