```
```cpp
bool __stdcall CDirectOscillator::userInterfaceChange(int mControlIndex)
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
```

Build and load the dynamic link library (DLL). Then, hit the Start and Stop buttons to control your oscillator. Play with the frequency slider to change the value. You will notice a lot of clicking due to the discontinuities that occur each time the oscillator is reset to re-trigger from the 0.0 value. Other than that problem, the output should be a pure sinusoid with very low distortion and noise.

# 9.2.5 Improving the Oscillator Design

One of the drawbacks of oscillators is their initial conditions usually must be met (there are noise generators and other devices that can start up in a random state). In this case, we must preload the delay elements with samples that would have occurred before the initial output sample. If the user changes the frequency of oscillation, the initial states must change too. The problem is that the oscillator can be in any state when the user changes the controls. Suppose the user decreased the frequency of oscillation a bit and that the oscillator had some values in y(n - 1) and y(n - 2). Then to set up the new initial state, you can share the y(n - 1) value between the two sinusoids and calculate a new y(n - 2) value. The next sample out of the oscillator is at the new rate, using the new initial state you created (Figure 9.7).

![](bbox=[0.35, 0.71, 0.65, 0.85])

Figure 9.7: The new initial state samples, y(n - 1) and y(n - 2); we share the y(n - 1) sample as if it was from the new frequency and alter the y(n - 2) value to relocate it on the new sinusoid.

The initial conditions from the design equations are in Equation 9.4: