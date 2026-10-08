```
CVAOnepoleFilter::doFilter(double xn)
{
```

```
// --- return xn if filter not supported
if(m_uFilterType != LPF1 && m_uFilterType != LPF1)
  return xn;
```

```
// --- see diode filter structure
```

xn = xn*m_dGamma + m_dFeedback + m_dEpsilon*getFeedbackOutput();

# Constructor:

```
// --- calculate v(n)
```

+   * initialize all variables
* initialize filter type to LPF2
* set the Aux Control to 0.5, which centers the control for the BSF-output
* call reset() to flush storage registers

```
double vn = (m_da0*xn - m_dZ1)*m_dAlpha;
```

```
// form LP output
```

```
double lpf = vn + m_dZ1;
```

Figure 7.49: The CSEMFilter class diagram.

```
// --- update memory
```

```
m_dZ1 = vn + lpf;
```

```
// do the HPF
```

```
double lpf = xn - lpf;
```

# reset()

```
// --- select output
```

This simple function just clears the storage registers.

```
if(m_uFilterType == LPF1)
```

```
  return lpf;
```

```
else if(m_uFilterType == HPF1)
```

```
  return hpf;
```

```
return xn; // should never get here
```

```
}
```

```
virtual void reset (m_dZ11 = 0; m_dZ12 = 0.0);
```

# setQControl()

The Q control on the GUI is always labeled 1 to 10 or range of [1..10], and this needs to be remapped to a meaningful value for each filter. We will let the filter's actual Q vary from 0.5 to 25 over this range. The mapping function is straightforward.