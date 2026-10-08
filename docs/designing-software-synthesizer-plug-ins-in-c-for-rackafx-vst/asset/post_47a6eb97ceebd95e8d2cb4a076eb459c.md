
![](img/b42d0dca53f4a889d8162d55f7c8c05d_419_0.png)

![](img/b42d0dca53f4a889d8162d55f7c8c05d_419_1.png)

```cpp
void setFeedback(double fb) { m_dFeedback = fb; }

// provide access to our feedback
output
```

```cpp
void CVAOnePoleFilter::update()
{
    // base class does modulation, changes m_ffC
    CFilter::update();

    double wd = 2*pi*m_dFc;
    double T = 1/m_dSampleRate;
    double wa = (2/T)*tan(wd*T/2);
    double g = wa*T/2;

    m_dAlpha = g/(1.0 + g);
}
```

```cpp
// m_dFeedback & m_dDelta = 0 for non-Diode

double getFeedbackOutput() { return m_dBeta*(m_dZ1 + m_dFeedback*m_dDelta); }

// flush storage and clear
feedback

virtual void reset() { m_dZ1 = 0; m_dFeedback = 0; }
```

## doFilter()

The sequence of calculations for the trapezoidal integrator LPF and HPF consist of:

- calculate the intermediate variable v(n)
- form the output by adding the storage value
- update the storage location with new value
- form the HPF output
- return the proper output

This function also implements the added code for the diode ladder structure.

## 7.15 The CSEM Filter Object

The SEM based model is the only one that does not use the VA one-pole filters we coded; it has its own architecture. We will be implementing the block diagram from Figure 7.6, so you need to be familiar with it. Figure 7.4 shows the diagram for the object.

Like the CVAOnePoleFilter, this object's member variables are self-explanatory when referring to the block diagram and equations. The methods are all base class overrides, so let's step through them.

```cpp
CVAOnepoleFilter::doFilter(double xn)
{
// --- return xn if filter not supported
if(m_uFilterType != LPF1 && m_uFilterType != LPF1)
  return xn;

// --- see diode filter structure

xn = xn*m_dGamma + m_dFeedback + m_dEpsilon*getFeedbackOutput();
```

## Constructor:

```cpp
// --- calculate v(n)
- initialize all variables
- initialize filter type to LPF2
- set the Aux Control to 0.5, which centers the control for the BSF-output
- call reset() to flush storage registers

double vn = (m_da0*xn - m_dZ1)*m_dAlpha;

// form LP output
double lpf = vn + m_dZ1;
```

Figure 7.49: The CSEMFilter class diagram.

```cpp
// --- update memory
m_dZ1 = vn + lpf;

// do the HPF
double lpf = xn - lpf;
```

## reset()

```cpp
// --- select output
This simple function just clears the storage registers.

if(m_uFilterType == LPF1)
  return lpf;
else if(m_uFilterType == HPF1)
  return hpf;

return xn; // should never get here

}

virtual void reset (m_dZ1 = 0; m_dZ12 = 0.0);
```

## setQControl()

The Q control on the GUI is always labeled 1 to 10 or range of [1..10], and this needs to be remapped to a meaningful value for each filter. We will let the filter's actual Q vary from 0.5 to 25 over this range. The mapping function is straightforward.

## filter()

This function recalculates the filter parameters from the current cutoff and Q values. It uses the equations in Section 7.2 for the parameter calculations.

- always call base class first in the update method
- as with bilinear filters we need to pre-warp the cutoff frequency

![](img/b42d0dca53f4a889d8162d55f7c8c05d_422_0.png)

## doFilter()

The doFilter() function performs the processing. Its code is extracted directly from the filter block diagram. It calculates all outputs and returns the appropriate output. As all other filters, you must first check to make sure the filter is supported (this makes it easier to implement multiple filter selection in your plug-in).

- check to make sure filter is supported, otherwise return the input value
- calculate the HPF output (which is u, the input to the first block)
- process to get the BPF
- saturate the integrator, if NLP is ON
- process the BSF with the Aux Control
- update the filter
- decide on what output

![](img/b42d0dca53f4a889d8162d55f7c8c05d_422_1.png)

## 7.16 The CKFiveFilter Object

The object will design both the low and highpass filters using the Sallen-Key filter. The model uses VA-pole filter objects we already designed. They do the processing, so the filter object needs to handle the calculating and updating of these blocks and the final processing. The same CFilter overrides will be implemented Figure 7.50 shows the class diagram for CKFiveFilter.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_422_2.png)

## CKFiveFilter Member Variables

Refer to 7.19 to see that there are three-filters: LPF1, LPF2 and HP1, as well as two coefficients, the Q value and f0. These will make up the member variables of object. To make LPF, we need first order LPFs and first order HPF. To make HPF, we need two order HPFs and one first order LPF. Therefore, we need two of each type for implementation. These are declared member objects of type VAPoleFilter and named m_LPF1, m_LPF2, m_HPF1 and m_HPF2.

```cpp
// --- init
m_dAlpha0 = 1.0;
m_dAlpha = 1.0;
m_dRho = 1.0;
m_dAuxControl = 0.5; // for BSF

// --- default filter
m_uFilterType = LPF2;

// --- flush registers
reset();
```

```cpp
void CSEMFilter::setQControl(double dQControl)
{
  // this maps dQControl = 1->10 to Q = 0.5->25
  m_dQ = (25.0 - 0.5)*(dQControl - 1.0)/(10.0 - 1.0) + 0.5;
}

void CSEMFilter::update()
{
  // base class does modulation
  CFilter::update();

  // pre-warp the cutoff- these are bilinear filters
  double wd = 2*pi*m_dFC;
  double T = 1/m_dSampleRate;
  double wa = (2/T)*tan(wd*T/2);
  double g = wa*T/2;

// note R is traditional analog damping factor
double R = 1.0/(2.0*m_dQ);
```

## CKFiveFilter Member Methods

Constructor:

- initialize the member variables
- set default type to second order LPF
- reset to flush storage

```cpp
// set the coeffs
_dAlpha0 = 1.0/(1.0 + 2.0*R*g + g*g);
_dAlpha = g;
_dRho = 2.0*R + g;
```

Figure 7.50: The class diagram for CKFiveFilter.

## reset()

- call reset() on the member objects; nothing for us to reset in the main object

## setQControl()

- map the Q control on the GUI (1 to 10) to a range of Q values 0.01 to 2 (self-oscillation)
- use the same simple equation to map ranges

```cpp
double CSEMFilter::doFilter(double xn)
{
    // return xn if filter supported
    if(m_uFilterType != LPF2 && m_uFilterType != HPF2 &&
        m_uFilterType != BPF2 && m_uFilterType != BSF2)
        return xn;

    // form the HP output first
    double hpf = m_dAlpha0*(xn - m_dRho*m_dZ11 - m_dZ12);

    // BPF Out
    double bpf = m_dAlpha*hpf + m_dZ11;

    // for nonlinear proc
    if(m_uNLP == ON)
        bpf = tanh(m_dSaturation*bpf);

    // LPF Out
    double lpf = m_dAlpha*bpf + m_dZ12;

    // note R is the traditional analog damping factor
    double R = 1.0/(2.0*m_dQ);

    // BSF Out
    double bsf = xn - 2.0*R*bpf;

    // SEM BPF Out
    // using m_dAuxControl for this one-off control
    double semBSF = m_dAuxControl*hpf + (1.0 - m_dAuxControl)*lpf;

    // update memory
    m_dZ11 = m_dAlpha*hpf + bpf;
    m_dZ12 = m_dAlpha*bpf + lpf;
}
```

update()

- always call the base class method first
- pre-warp the cutoff and set the a value on each member object
- calculate the beta feedback values
- set coefficients according to the equations

```cpp
// return our selected type
if(m_uFilterType == LPF2)
    return lpf;
else if(m_uFilterType == HPF2)
    return hpf;
else if(m_uFilterType == BPF2)
    return bpf;
else if(m_uFilterType == BSF2)
    return semBSF;
```

## doFilter()

- check to make sure filter is supported, otherwise return the input value
- both filters follow the same sequences (refer to text above)
- process input through the input filter (LPF or HPF)
- form the feedback term S35 here
- calculate u, the input to the next filter
- add NLP if desired
- feed the output filter in the feedback loop (HPF or BPF)
- normalize the output by 1/K

## 7.17 The CMogLadderFilter Object

This object implements the normal fourth order Moog filter plus the Oberheim variations in Table 7.1. The model uses four one-pole filter objects to implement the four filtering stages. The same CFilter overrides will also be implemented. Figure 7.51 shows the class diagram for the CMogLadderFilter.

## CMogLadderFilter Member Variables

Refer to Figures 7.27 and 7.28 to see that there are four sub-filters (LPF1, LPF2, LPF3, LPF4) several coefficients, the K and f0 and all the Oberheim variation coefficients. These will make up the member variables of the object. Its filters
