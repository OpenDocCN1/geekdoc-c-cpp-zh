
Figure 9.2: Initial conditions that would have produced a sinusoid whose first output sample is 0.0.

![](img/b54974d0a4317ec82d7ae02126d10a6f_278_0.png)

Figure 9.3: The direct form oscillator is really the feedback side of the bi-quad structure.

Specify:

- $f_o$, desired oscillation frequency

The design equations are as follows:

```
\(\theta = \frac{2\pi f_o}{f_s}\)
\(b_1 = -2\cos(\theta)\)
\(b_2 = 1.0\)
(9.3)
```

Initial conditions:

```
y(n - 1) = sin(-10)
y(n - 2) = sin(-20)
```

## 9.2 Design a Direct Form Oscillator Plug-In

In our first version of the direct form oscillator we are going to make it as simple as possible by restarting the oscillator when the user changes the oscillator frequency. This means we are going to recalculate the initial conditions as if the oscillator was starting from a phase of 0 degrees and the first sample out would have a value of 0.0. After we have that up and running, we will modify it to change frequency on the fly, automatically back-calculating the initial conditions for any given output sample. Here are the oscillator's specifications:

- Monophonic sinusoidal oscillator.
- We will need to implement a second-order feedback block.
- We will need a slider for the user to control the oscillation frequency in Hz.
- We will need a cookFrequency() function to calculate our coefficients and reset our initial conditions when the user moves the frequency slider.
- The oscillator's range will be 200 Hz to 6 kHz.
- We need to assign Start and Stop buttons.

### 9.2.1 Project: DirectOscillator

Create a new project in RackAFX. On the new project dialog, make sure you check the box “Output Only Synthesizer Plug-In”—you must select this for any synthesis plug-in; you will not be able to play a wave file through it (Figure 9.4).

### 9.2.2 DirectOscillator GUI

Add a frequency slider (Figure 9.5) to the user interface (UI) with the parameters in Table 9.1. Next, set up the assignable buttons to create start and stop functions. Right-click inside the box labeled “Assignable Buttons” but do not click on a button, only in the area in between. A dialog pops up (Figure 9.6) that lets you set the button names. Choose “Start,” “Stop,” and make the last one blank with “ ” by entering the strings in the edit boxes. The buttons will automatically use the text you enter. Do not check the “Latching” buttons. See the website for notes on how to use latching buttons.

Table 9.1: The GUI control for the DirectOscillator plug-in

| Slider Property | Value |
|---|---|
| Control Name | Frequency |
| Units | Hz |
| Variable Type | float |
| Variable Name | m_fFrequency_Hz |
| Low Limit | 200 |
| High Limit | 6000 |
| Initial Value | 1000 |

![](img/b54974d0a4317ec82d7ae02126d10a6f_280_0.png)

Figure 9.4: Make sure you check the “Output Only Synthesizer Plug-In” box for your oscillators.

![](img/b54974d0a4317ec82d7ae02126d10a6f_280_1.png)

Figure 9.5: The DirectOscillator GUI.

These assignable buttons will trigger your userInterfaceChange() function with their nControlIndex values of 50, 51, and 52. See the userInterfaceChange() function for more details.

![](img/b54974d0a4317ec82d7ae02126d10a6f_281_0.png)

Figure 9.6: The assignable button setup; notice that the last button is blank. RackAFX will hide it when you load the plug-in.

### 9.2.3 DirectOscillator.h File

In the .h file, declare the variables you need to implement the oscillator:

```
// Add your code here: .................................... //
//
// coefficients, 2nd Order FB
float m_f_b1;
float m_f_b2;

// delay elements, 2nd Order FB
float m_f_y_z1;
float m_f_y_z2;

// flag to start/stop oscillator
bool m_bRunOscillator;

// function to cook the Frequency and set initial conditions
void cookFrequency();
//
// END OF USER CODE ....................................... //
```

### 9.2.4 DirectOscillator.cpp File

### Constructor

- Turn off the oscillator by setting the flag you declared in the .h file. You will need to do these two steps any time you make an oscillator or other output-only plug-in.

```
CDirectOscillator::CDirectOscillator()
{
    <SNIP SNIP SNIP>
    // Finish initializations here
    // turn off
    m_bRunOscillator = false;
    // set 0
    m_f_b1 = 0;
    m_f_b2 = 0;
    // flush memory
    m_f_y_z1 = 0;
    m_f_y_z2 = 0;
    // call the cooking function to calc coeffs
    // and set initial states
    cookFrequency();
}
```

Implement the cooking function according to the design equations:

```
void CDirectOscillator::cookFrequency()
{
    // Oscillation Rate = theta = wT = w/fs
    float f_wT = (2.0f*pi*m_fFrequency_Hz)/(float)m_nSampleRate;
    // coefficients according to design equations
    m_f_b1 = -2.0f*cos(f_wT);
    m_f_b2 = 1.0;
    // set initial conditions so that first sample out is 0.0
    m_f_y_z1 = sin(-1.0f*f_wT); // sin(wmT) = sin(w*(1-1)T)
    m_f_y_z2 = sin(-2.0f*f_wT); // sin(wmT) = sin(w*(2-2)T)
}
```

### prepareForPlay()

Call the cooking functions to initialize the oscillator:

```
bool __stdcall CDirectOscillator::prepareForPlay()
{
    // Add your code here:
    // calc coeffs and initial conditions
    cookFrequency();
    return true;
}
```

### processAudioFrame()

- Implement the second-order feedback filter.
- Check the oscillator flag. If the oscillator is not running you must send 0.0 samples to the output stream and then return without further processing. This is done at the very beginning of the function.

```
bool __stdcall CDirectOscillator::processAudioFrame(float* pInputBuffer, float* pOutputBuffer, UINT uNumInputChannels, UINT uNumOutputChannels)
{
    //
    // output - input -- change this for meaningful processing
    //
    // Do LEFT (MONO) Channel
    //
    // if not running, write 0s and bail
    if(!m_bRunOscillator)
    {
        // zero it all out
        pOutputBuffer[0] = 0.0;

        // Mono-In, Stereo-Out (AUX Effect)
        if(uNumInputChannels == 1 && uNumOutputChannels == 2)
            pOutputBuffer[1] = 0.0;

        // Stereo-In, Stereo-Out (INSERT Effect)
        if(uNumInputChannels == 2 && uNumOutputChannels == 2)
            pOutputBuffer[1] = 0.0;

    }
    return true;

    // otherwise, do the oscillator
    // do difference equation y(n) = -b1y(n-2) - b2y(n-2)
    pOutputBuffer[0] = m_f_b1*m_f_y_z1 - m_f_b2*m_f_y_z2;

    // Mono-In, Stereo-Out (AUX Effect)
    if(uNumInputChannels == 1 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pOutputBuffer[0];

    // Stereo-In, Stereo-Out (INSERT Effect)
    if(uNumInputChannels == 2 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pOutputBuffer[0];

    // shuffle memory
    m_f_y_z2 = m_f_y_z1;
    m_f_y_z1 = pOutputBuffer[0];

    return true;
}
```

### userInterfaceChange()

- Call the frequency cooking function and implement the start and stop functions.
- Make sure your nControlIndex values match your switch/case statement.

```
bool __stdcall CDirectOscillator::userInterfaceChange(int nControlIndex)
{
    // cook variables
    switch(nControlIndex)
    {
    case 0: // freq
        cookFrequency();
        break;

    case 50: // start
        m_bRunOscillator = true;
        break;

    case 51: // stop
        m_bRunOscillator = false;
        break;

    default:
        break;
    }
    return true;
}
```

Build and load the dynamic link library (DLL). Then, hit the Start and Stop buttons to control your oscillator. Play with the frequency slider to change the value. You will notice a lot of clicking due to the discontinuities that occur each time the oscillator is reset to re-trigger from the 0.0 value. Other than that problem, the output should be a pure sinusoid with very low distortion and noise.

### 9.2.5 Improving the Oscillator Design

One of the drawbacks of oscillators is their initial conditions usually must be met (there are noise generators and other devices that can start up in a random state). In this case, we must preload the delay elements with samples that would have occurred before the initial output sample. If the user changes the frequency of oscillation, the initial states must change too. The problem is that the oscillator can be in any state when the user changes the controls. Suppose the user decreased the frequency of oscillation a bit and that the oscillator had some values in y(n - 1) and y(n - 2). Then to set up the new initial state, you can share the y(n - 1) value between the two sinusoids and calculate a new y(n - 2) value. The next sample out of the oscillator is at the new rate, using the new initial state you created (Figure 9.7).

![](img/b54974d0a4317ec82d7ae02126d10a6f_284_0.png)

Figure 9.7: The new initial state samples, y(n - 1) and y(n - 2); we share the y(n - 1) sample as if it was from the new frequency and alter the y(n - 2) value to relocate it on the new sinusoid.

The initial conditions from the design equations are in Equation 9.4:
