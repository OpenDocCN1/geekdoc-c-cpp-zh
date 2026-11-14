| Variable Type | enum |
| Variable Name | m_fTimeConstant |
| Enum String | analog, digital |

| Button Property | Value |
| Control Name | Direction |
| Units | |
| Variable Type | enum |
| Variable Name | m_fDirection |
| Enum String | UP, DOWN |

And, it needs controls for the modulated filter:

+   - Q
+   - Direction of modulation (up or down)

# 12.5.3 EnvelopeFollower.h File

We need to add the following new functions and variables; most can be taken directly from your ModFilter project. We will need:

+   - An LPF bi-quad for each channel (left, right)
+   - An envelope detector for each channel (left, right)
+   - A function to calculate a new LPF cutoff value from an envelope value
+   - Functions to calculate the bi-quad coefficients from the LPF cutoff and Q values
+   - Min/max LPF cutoff variables

Add the following to your .h file:

```
// Add your code here: ------------------------------------------------------ //
// two LPF BiQuads for the filters
CBiquad m_LeftLPF;
CBiquad m_RightLPF;

// function to calculate the new fc from the Envelope Value
float calculateCutoffFreq(float fEnvelopeSample);

// calculate the coeffs for a given filter
void calculateLPFCoeffs(float fCutoffFreq, float f0, CBiquad* pFilter);

// min/max variables
float m_fMinCutoffFreq;
float m_fMaxCutoffFreq;

// envelope detectors
CEnvelopeDetector m_LeftDetector;
CEnvelopeDetector m_RightDetector;

// END OF USER CODE ------------------------------------------------------ //
```