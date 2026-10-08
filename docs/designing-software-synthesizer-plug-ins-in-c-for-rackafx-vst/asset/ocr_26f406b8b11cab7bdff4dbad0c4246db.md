the tables
must be re-
calculated.
We also
need to
override
update() to
calculate
our read
locations
select
a new table
if the
frequency
has
changed.

```
break;
```

```
case SQUARE:
dOut = doSquare(dCalcModulo, m_dInc);
break;

```

```
case TRI:
{
if(bWrap)
m_dDPWSSquareModulator *= -1.0;
dOut = doTriangle(dCalcModulo, m_dInc,
m_dFo, m_dDPWSSquareModulator,
&m_dDPW_z1);
break;

```

```
case NOISE: // same as LFO
case PNOISE: // same as LFO
default:
break;

```

```
// --- ok to inc modulo now
incModulo();

// --- inc twice for Triangle
if(m_uWaveform --- TRI)
incModulo();

// --- m_dampMod is set in update()
if(pAuxOutput)
*pAuxOutput = dOut*m_dampAmplitude*m_dampMod;

// --- m_dampMod is set in update()
return dOut*m_dAmplitude*m_dampMod;
```