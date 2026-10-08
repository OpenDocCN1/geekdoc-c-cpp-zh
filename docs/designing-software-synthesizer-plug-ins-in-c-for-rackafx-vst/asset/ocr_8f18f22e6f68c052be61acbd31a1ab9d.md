is unacceptable.

# doSquare ()

```
*pQuadPhaseOutput = 0.0;
```

```
return 0.0;
```

+   • use the sum-of-saws method; this requires some trickery
we—temporarily set our waveform variable to SAW1(the pure saw) and doSaawtooth() twice
• the first call is normal, then we modify the module counter by offsetting it based on the pulse width; notice how we check the phase increment value for positive (normal) or negative frequency operation—the wrapping operation also works in both forward and reverse
• we can call the sawtooth function twice safely since the module counter is not incremented until after the square wave function ends

```
// for QP output
// advance modulo by 0.25 = 90 degrees
double dQuadModulo = m_dModulo + 0.25;
// check and wrap
if(dQuadModulo >= 1.0)
dQuadModulo == 1.0;
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
dPQOut = parabolicSine(-dAngle);
break;
case usaw:
case dsaw:
// --- one shot is unipolar for saw
if(m_uLFOMode == shot)
// unipolar to bipolar
dOut = unipolarToBipolar(m_dModulo);n
```