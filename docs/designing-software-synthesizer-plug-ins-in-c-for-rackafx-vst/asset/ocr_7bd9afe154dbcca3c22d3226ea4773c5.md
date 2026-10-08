```
// pre-warp for BZT
double wd = 2*pi*m_dFc;
double T = 1/m_dSampleRate;
double wa = (2/T)*tan(wd*T/2);
double g = wa*T/2;
```

+   * main filter coefficients and SG values
* set the VA one-pole coefficients according to the equations
* you can get the full derivation of these equations from

```
// G - the feedforward coeff in the VA One Pole //
// same for LPF, HPF
double G = g/(1.0 + g);
```

```
// set alphas; same for LPF, HPF
m_LPF1.m_dAlpha = G;
m_LPF2.m_dAlpha = G;
m_HPF1.m_dAlpha = G;
m_HPF2.m_dAlpha = G;
```

```
// set m_dAlpha0 variable: same for LPF, HPF
m_dAlpha0 = 1.0/(1.0 - m_dK*G + m_dK*G*G);
```

```
if(m_uFilterType == LPF2)
    m_LPF2.m_dBeta = (m_dK - m_dK*G)/(1.0 + g);
    m_HPF1.m_dBeta = -1.0/(1.0 + g);
```

```
else // HPF
    m_HPF2.m_dBeta = -1.0*G/(1.0 + g);
    m_LPF1.m_dBeta = 1.0/(1.0 + g);
```

http://www.willpinkle.com/synthbook/

doFilter()