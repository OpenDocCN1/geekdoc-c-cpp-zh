```
m_ModDelayLeft.m_uLFOPhase = 1; // 1: quad phase
m_ModDelayCenter.m_uLFOPhase = 0; // 0: normal
m_ModDelayRight.m_uLFOPhase = 1; // 1: quad phase

m_ModDelayLeft.m_LFO_m_bInvert = false;
m_ModDelayCenter.m_LFO_m_bInvert = false;
m_ModDelayRight.m_LFO_m_bInvert = true; // this one is inverted

m_ModDelayLeft.m_fModDepth_pct = m_fModDepth_pct_L;
m_ModDelayCenter.m_fModDepth_pct = m_fModDepth_pct_C;
m_ModDelayRight.m_fModDepth_pct = m_fModDepth_pct_R;

m_ModDelayLeft.m_fModFrequency_Hz = m_fModFrequency_Hz_L;
m_ModDelayCenter.m_fModFrequency_Hz = m_fModFrequency_Hz_C;
m_ModDelayRight.m_fModFrequency_Hz = m_fModFrequency_Hz_R;

m_ModDelayLeft.m_fFeedback_pct = m_fFeedback_pct_L;
m_ModDelayCenter.m_fFeedback_pct = m_fFeedback_pct_C;
m_ModDelayRight.m_fFeedback_pct = m_fFeedback_pct_R;

// CHORUS!
m_ModDelayLeft.m_uModType = 2;
m_ModDelayCenter.m_uModType = 2;
m_ModDelayRight.m_uModType = 2;

m_ModDelayLeft.m_uLFOType = 0; // triangle
m_ModDelayCenter.m_uLFOType = 0; // triangle
m_ModDelayRight.m_uLFOType = 0; // triangle

// cook them
m_ModDelayLeft.updateLFO();
m_ModDelayCenter.updateLFO();
m_ModDelayRight.updateLFO();

m_ModDelayLeft.updateDDL();
m_ModDelayCenter.updateDDL();
m_ModDelayRight.updateDDL();
}
```

# prepareForPlay()

+   • Forward the calls to prepareForPlay() to the member objects.

```
bool __stdcall CStereoLCRChorus::prepareForPlay()
{
    // Add your code here:
    // call forwarding!
    m_ModDelayLeft.prepareForPlay();
    m_ModDelayCenter.prepareForPlay();
    m_ModDelayRight.prepareForPlay();

    // don't leave this out - it inits and cooks
    updateModules();

    return true;
}
```

# UserInterfaceChange()

+   • Just do a brute force update of all modules (you can streamline this later):