```
// LFO function to set:
// - the LFO Frequency
// - the oscillator type
void CModDelayModule::updateLFO()
{
    // set raw data
    m_LFO.m_fFrequency_Hz = m_fModFrequency_Hz;
    m_LFO.m_wOscType = m_uLFOType;

    // cook it
    m_LFO.cookFrequency();
} // DDL function to set:
// - the DDL Feedback amount (disabled for Vibrato)
void CModDelayModule::updateDDL()
{
    // test and set if needed
    //if(m_uModType != Vibrato)
    m_DDL.m_fFeedback_pct = m_fFeedback_pct;

    // cook it
    m_DDL.cookVariables();
}
```

Write the cookModType() function using the information in Table 10.3—this method is called when the user changes the effect type.

```
/* cookMod() function:
*/
Flanger    Min Delay (mSec)   Max delay (mSec)   Wet/Dry(%)   Feedback(%)
Vibrato    0                   7-10               50/50        -100 to +100
Chorus     5                   20-40              50/50        -100 to +100
*/
void CModDelayModule::cookModType()
{
    switch(m_uModType)
    {
        case Flanger:
        {
            m_fMinDelay_mSec = 0;
            m_fMaxDelay_mSec = 7;
            m_DDL.m_fWetLevel_pct = 50.0;
            m_DDL.m_fFeedback_pct = m_fFeedback_pct;
            break;
        }
        case Vibrato:
        {
            m_fMinDelay_mSec = 0;
            m_fMaxDelay_mSec = 7;
            m_DDL.m_fWetLevel_pct = 100.0;
            m_DDL.m_fFeedback_pct = 0.0; // NOTE! no FB for vibrato
        }
    }
}
```

Table 10.3: The default delay line settings for the various effects.

| | Min Delay(mSec) | Max Delay(mSec) | Wet/Dry(%) | Feedback(%) |
|---|---|---|---|---|
| Flanger | 0 | 7-10 | 50/50 | -100 to +100 |
| Vibrato | 0 | 7-10 | 100/0 | 0 |