```
bool __stdcall CModDelayModule::processAudioFrame(float* pInputBuffer, float*
        pOutputBuffer, UINT uNumInputChannels,
        UINT uNumOutputChannels)
{
    // Do LEFT (MONO) Channel
    //
    // 1. Get LFO Values, normal and quad phase
    float fYn = 0;
    float fYqn = 0;
    m_LFO.doOscillate(&fYn, &fYn, &fYqn);

    // 2. calculate delay offset
    float fDelay = 0.0;
    if(m_uLFOPhase == quad)
        fDelay = calculateDelayOffset(fYqn); // quadrature LFO
    else
        fDelay = calculateDelayOffset(fYn); // normal LFO

    // 3. set the delay & cook
    m_DDL.m_fDelay_ms = fDelay;
    m_DDL.cookVariables();

    // 4. get the delay output one channel in/one channel out
    m_DDL.processAudioFrame(&pInputBuffer[0], &pOutputBuffer[0], 1, 1);

    // Mono-In, Stereo-Out (AUX Effect)
    // if(uNumInputChannels == 1 && uNumOutputChannels == 2)
    pOutputBuffer[1] = pOutputBuffer[0];

    // Stereo-In, Stereo-Out (INSERT Effect)
    // if(uNumInputChannels == 2 && uNumOutputChannels == 2)
    pOutputBuffer[1] = pOutputBuffer[0];

    return true;
}
```

Build and test the module. Be sure to listen to the flanger as the delay hits the zero point.

# 10.3.6 Challenge

Add another radio button switch to turn on or off TZF that we employ. To turn off TZF, set the minimum delay time for flanging to a nonzero value (try 0.1 mSec to begin with) in the cookModType() method. You now have a working modulated delay module that can be combined in many ways to create a wide variety of modulated delay effects. Let's try a couple of them now.

# 10.4 Design a Stereo Quadrature Flanger Plug-In

The block diagram of the stereo quad flanger is shown in Figure 10.5 and it consists of two identical flanger delay lines running off of LFO values that are in quadrature phase. Since our mod delay module has a built-in LFO and delay, we can assemble this plug-in quickly.

# 10.4.1 Project: StereoQuadFlanger

Make sure to add all the existing modules when you create the new StereoQuadFlanger project:

+   • ModDelayModule.h.