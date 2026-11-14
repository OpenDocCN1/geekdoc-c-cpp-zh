```
// Add your code here: ------------------------------------ //
//
// Pre-Delay Block
CDelay m_PreDelay;

// input Diffusion
COnePoleLPF m_InputLPF;
CDelayAPF m_InputAPF_1;
CDelayAPF m_InputAPF_2;

// parallel Comb Bank 1
CCombFilter m_Parallel1CF_1;
CCombFilter m_Parallel1CF_2;
CLPFBCombFilter m_Parallel1CF_3;
CLPFBCombFilter m_Parallel1CF_4;

// parallel Comb Bank 2
CCombFilter m_Parallel2CF_5;
CCombFilter m_Parallel1CF_6;
CLPFBCombFilter m_Parallel1CF_7;
CLPFBCombFilter m_Parallel1CF_8;

// damping
COnePoleLPF m_DampingLPF1;
COnePoleLPF m_DampingLPF2;

// output diffusion
CDelayAPF m_OutputAPF_3;
CDelayAPF m_OutputAPF_4;

// function to cook all member object's variables at once
void cookVariables();

// END OF USER CODE ------------------------------------ //
```

# 11.17.4 Reverb.cpp

Write the only extra function, cookVariables():

```
// function to cook all variables at once
void CReverb::cookVariables()
{
    // Pre-Delay
    m_PreDelay.setDelay_mSec(m_fPreDelay_mSec);
    m_PreDelay.setOutputAttenuation_dB(m_fPreDelayAtten_dB);

    // input diffusion
    m_InputAPF_1.setDelay_mSec(m_fAPF_1_Delay_mSec);
    m_InputAPF_1.setAPF_g(m_fAPF_1_g);
```