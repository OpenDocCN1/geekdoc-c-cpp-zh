| Chorus | 7 | 20-40 | 50/50 | Typically 0 |
|---|---|---|---|---|

```
```cpp
case Chorus:
{
  m_fMinDelay_mSec = 5;
  m_fMaxDelay_mSec = 30;
  m_DDL.m_fWetLevel_pct = 50.0;
  m_DDL.m_fInputAttenuation = 1.0;
  break;
}
default: // is Flanger
{
  m_fMinDelay_mSec = 0;
  m_fMaxDelay_mSec = 7;
  m_DDL.m_fWetLevel_pct = 50.0;
  m_DDL.m_fFeedback_pct = m_fFeedback_pct;
  break;
}
```
```

Write the calculateDelayOffset() function. It works by taking the LFO value from 0 to 1.0 and mapping it on to the range from min to max delay. Then, this value is scaled by the depth percent value so that at 100% the maximum range is used. For the chorus, we effectively move the operating range and chorus center by adding a delay offset to the minimum value, then using that as the starting (reference) point in the calculation.

```
```cpp
// calculateDelayOffset():
/*
 fLFOSample: a value from 0.0 to 1.0 from the LFO object

 returns: the calculated delay time in mSec for each effect

 NOTES: - the range for the flanger/vibrato is simply mapped from min to max
         starting at min: fLFOSample*(m_fMaxDelay_mSec - m_fMinDelay_mSec) +
         m_fMinDelay_mSec
     
     - the range for the Chorus includes the starting offset
        fStart = m_fMinDelay_mSec + m_fChorusOffset;
*/
if(m_uModType == Flanger || m_uModType == Vibrato)
{
  // flanger 0-1 gets mapped to 0->maxdelay
  return (m_fModDepth_pct/100.0)*(fLFOSample*(m_fMaxDelay_mSec -
  m_fMinDelay_mSec)) + m_fMinDelay_mSec;
}
else if(m_uModType == Chorus)
{
  // chorus adds starting offset to move delay range
  float fStart = m_fMinDelay_mSec + m_fChorusOffset;
  return (m_fModDepth_pct/100.0)*(fLFOSample*(m_fMaxDelay_mSec -
  m_fMinDelay_mSec)) + fStart;
}
```
```

# 10.3.5 PrepareForPlay()

+   - Forward the call to prepareForPlay() on the member objects.
+   - Reset and start up the LFO in unipolar mode.