
Download the files for the NanoSynth: Oscillators project. You need to add the following files if you are creating the synth from scratch:

- Oscillator.h
- Oscillator.cpp
- synthfunctions.h
- SynthParamLimits.h (VST3 and AU only)

Figure 5.46: Class diagram for the LFO object.

Now we are ready to implement the pitched and LFO oscillators.

## 5.31 The CLFO Object

Let's start by creating and implementing the LFO object. Add a new class to your project named CLFO and make sure to set its base class to COscillator. Figure 5.46 shows the class diagram. Refer to the code listing for the LFO file below and copy it into your file (or alternatively you can download the sample code). Figure 5.46: class diagram for CLFO.

## CLFO Member Variables

There are no members to declare; they are all in the base class.

## CLFO Member Methods

We only need to override a few virtual functions because much functionality is built into the base class.

### LFO.cpp

Implement the following methods to fill out the rest of the object.

### Constructor

- initialize the LFO variable to sync; the waveform is initialized to sine in the base class—you may change the default here

### reset ()

- call the base class method for base reset

![](img/b42d0dca53f4a889d8162d55f7c8c05d_290_0.png)
![](img/b42d0dca53f4a889d8162d55f7c8c05d_290_1.png)
![](img/b42d0dca53f4a889d8162d55f7c8c05d_290_2.png)
![](img/b42d0dca53f4a889d8162d55f7c8c05d_290_3.png)

### startOscillator ()

- if not in free run mode, call reset
- set the note on flag

### stopOscillator ()

- clear the note on flag

### doOscillator ()

This is the most important function on the object. It will use the algorithms and code snippets from Sections 5.x and 5.y to implement the trivial waveforms and noise oscillators. The function doOscillator() has the following prototype:

![](img/b42d0dca53f4a889d8162d55f7c8c05d_291_0.png)

```
inline virtual double doOscillator(double* pQuadPhaseOutput = NULL)
```

The argument is an optional parameter to a variable to receive the phase output. If the receiving object does not need this output, the function can be called without the argument. The function implements the following sequences:

- first, check to make sure the oscillator is running by checking the note on flag
- call checkWrapModulo() to check and wrap it if needed
- for one-shot LFO, if we just wrapped the modulo, we are done and return 0.0 and turn note off
- create a temporary quad phase modulo counter and add 0.25 to it; check for wrap
- follow the algorithms in the chapter, and if there is a quad phase variable, calculate this secondary output as
- sine uses a parabolic approximation
- saw (up and down) are extracted directly from modulo counter
- triangle and square are mathematically calculated via modulo counter
- exponentials uses the built-in convexInvertedFunction()
- the noise oscillators call a function in synthfunctions.h and then perform the hold using a counter to count sample periods of hold time

### LFO.h

```
class CLFO : public COscillator {
public:
    CLFO(void);
    CLFO(void);
```

```
// virtual overrides
void reset();
virtual void startOscillator();
virtual double doOscillate();
virtual void stopOscillator();
```

- for ramp and triangle, check the LFO mode and make unipolar for one-shot
- increment the modulo and return the amplitude-scaled output
- calculate normal and quad phase outputs by multiplying the output and amp values

## 5.32 The CQLimitedOscillator Object

Add new class to your project named CQLimitedOscillator and make sure to set its base class to Oscillator. Refer to the code listing below and copy it into your file (or, alternatively you can download the sample code). Figure 5.47 shows the class diagram for CQLimitedOscillator.

```
CLFO::CLFO(void) {
    m_uLFOMode = sync;
}
```

```
void CLFO::reset() {
    // --- call base class
    COscillator::reset();
}
```

### CQLimitedOscillator Member Variables

There are no extra members to declare; they are all in the base class.

### CQLimitedOscillator Member Methods

Aside from the class overrides (reset), startOscillator() and stopOscillator() are sub-functions to handle each oscillator type. The function doOscillate() will call these sub-functions for sawtooth and triangle and directly calculate other waveforms.

### Constructor

- there is nothing to do here because it is all done in base class

### reset ()

- always call base method first
- adjust the starting phase of modulo counter for sawtooth and triangle

Figure 5.47: Class diagram for CQLimitedOscillator object.

### startOscillator ()

- call reset()
- set the note on flag

### stopOscillator ()

- clear the note on flag

### doSquare ()

- use the sum-of-saws method; this requires some trickery
- temporarily set our waveform variable to SAW1 (the pure saw) and doSawtooth twice
- the first call is normal, then we modify the modulo counter by offsetting it based on the pulse width; notice how we check the phase increment value for positive (normal) or negative frequency operation—the wrapping operation also works in both forward and reverse
- we can call the sawtooth function twice safely since the module counter is not incremented until after the square wave ends

```
// for QP output
// advance modulo by 0.25 = 90 degrees
double dQuadModulo = m_dModulo + 0.25;
// check and wrap
if(dQuadModulo >= 1.0)
    dQuadModulo = 1.0;
// decode and calculate
switch(m_uWaveform)
{
case sine:
// calculate angle
double dAngle = m_dModulo*2.0*pi - pi;
// call the parabolicSine approximator
dOut = parabolicSine(-dAngle);
// use second modulo for quad phase
dAngle = dQuadModulo*2.0*pi - pi;
dQPOut = parabolicSine(-dAngle);
break;
case usaw:
case dsaw:
// --- one shot is unipolar for saw
if(m_uLFOMode == shot)
// unipolar to bipolar
dOut = unipolarToBipolar(m_dModulo);
// (see)
dQPOut = unipolarToBipolar(dQuadModulo);

}else
{
  dOut = m_dModulo - 1.0;
  dQPOut = dQuadModulo - 1.0;
}

// invert for down-saw
if(m_uWaveform == dsaw)
{
  dOut *= -1.0;
  dQPOut *= -1.0;
}

break;

case square:
{
// check pulse width and output either +1 or -1
dOut = m_dModulo > m_PulseWidth/100.0 ? -1.0 : +1.0;
dQPOut = dQuadModulo > m_PulseWidth/100.0 ? -1.0 : +1.0;

break;

case tri:
{
// triv saw
dOut = unipolarToBipolar(m_dModulo);

// bipolar triangle
dOut = 2.0*fabs(dOut) - 1.0;

if(m_uLFOMode == shot)
  // convert to unipolar
  dOut = bipolarToUnipolar(dOut);
break;
}
}
```

```
inline virtual double doOscillate(double* pQuadPhaseOutput = NULL)
```

The argument is an optional parameter to a variable to receive the phase output. If the receiving object does not need this output, the function can be called without the argument. The function implements the following sequences:

- first, check to make sure the oscillator is running by checking the note on flag
- call checkWrapModulo() to check and wrap it if needed
- for one-shot LFO, if we just wrapped the modulo, we are done and return 0.0 and turn note off
- create a temporary quad phase modulo counter and add 0.25 to it; check for wrap
- follow the algorithms in the chapter, and if there is a quad phase variable, calculate this secondary output as
- sine uses a parabolic approximation
- saw (up and down) are extracted directly from modulo counter
- triangle and square are mathematically calculated via modulo counter
- exponentials uses the built-in convexInvertedFunction()
- the noise oscillators call a function in synthfunctions.h and then perform the hold using a counter to count sample periods of hold time
- for ramp and triangle, check the LFO mode and make unipolar for one-shot
- increment the modulo and return the amplitude-scaled output
- calculate normal and quad phase outputs by multiplying the output and amp values
```

If using eight-point BLEP:
Notice that eight-point BLEP can be easily used if the frequency is less than 1/4 Nyquist, where you have more than eight points per cycle (four points of discontinuity); above this value switch to two-point BLEP in the commented code.

If you want to use the eight-point BLEP algorithm across the spectrum, you will need to deal with overlapping BLEP regions, and you will need to do some buffering and mixing in order to perform the proper corrections. You will also need to call the BLEP function more than once sample period. Failure to do this will result in output signal that is unacceptable.

```
// // output
double dOut = 0.0;
double dPOut = 0.0;
// // always first
bool bWrap = checkModulo();
// // one shot LFO?
if(m_uLFOMode == shot && bWrap)
    m_bNoteOn = false;

if(pQuadPhaseOutput)
    *pQuadPhaseOutput = 0.0;

return 0.0;
```

```
void LFO::startOscillator() {
    // if one shot or sync'd LFO, reset
    reset();
    // -- set flag
    m_bNoteOn = true;
    // call the BLEP (or polyBLEP) method to generate a residual and add to the output; the default is two-point BLEP, but you can un-comment the other portions to implement two-point BLEP or eight-point BLEP
}
```

```
void LFO::stopOscillator() {
    // --- clear flag
    m_bNoteOn = false;
}
```

```
inline virtual double doOscillate(double* pQuadPhaseOutput = NULL) {
    if(!m_bNoteOn)
        if(pQuadPhaseOutput)
            *pQuadPhaseOutput = 0.0;

    return 0.0;
}
```
