```
// Add your code here: ............................................... //
CBiquad m_LeftAPF_1;
CBiquad m_RightAPF_1;

CBiquad m_LeftAPF_2;
CBiquad m_RightAPF_2;

CBiquad m_LeftAPF_3;
CBiquad m_RightAPF_3;

// function to calculate the new fc from the Envelope Value
float calculateAPFCutoffFreq(float FLOSample, float fMinFreq, float fMaxFreq);

// Two functions to calculate the BiQuad Coeffs: APF
void calculateFirstOrderLeftAPFCoeffs(float fLFOSample);
void calculateFirstOrderRightAPFCoeffs(float fLFOSample);

// helper function for APF Calculation
void calculateFirstOrderAPFCoeffs(float fCutoffFreq,
CBiquad* pBiQuadFilter);

// min/max variables
float m_fMinAPF_1_Freq;
float m_fMaxAPF_1_Freq;

float m_fMinAPF_2_Freq;
float m_fMaxAPF_2_Freq;

float m_fMinAPF_3_Freq;
float m_fMaxAPF_3_Freq;

// LFO Stuff
CWaveTable m_LFO;

// END OF USER CODE ................................................ //
```

# 12.6.4 Phaser.cpp File

# Constructor

+   * Initialize the rate min and max values. The objects are self-initializing upon creation.
+   * Initialize the first three APF min/max pairs according to the table. We'll add the others once we have tested it and find it works properly.

```
CPhaser::CPhaser()
{
    <SNIP SNIP SNIP>

    // Finish initializations here
    // set our Min and Max Modulation points
    m_fMinAPF_1_Freq = 16.0;
    m_fMaxAPF_1_Freq = 1600.0;

    m_fMinAPF_2_Freq = 33.0;
    m_fMaxAPF_2_Freq = 3300.0;

    m_fMinAPF_3_Freq = 48.0;
    m_fMaxAPF_3_Freq = 4800.0;
}
```

Write the calculateAPFCutoffFreq() function. This function behaves exactly like the function in the