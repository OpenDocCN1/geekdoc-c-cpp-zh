| Variable Type | enum |
|---|---|
| Variable Name | m_uLFO_waveform |
| Enum String | sine, saw, tri, square |

Add the following to the .h file:

```
// Add your code here: ------------------------------------------------ //
// BiQuad Objects
CBiQuad m_LeftLPF;
CBiQuad m_RightLPF;

// one LFO for the fc
CWaveTable m_fcLFO;

// min and max values (to make it easy to change later)
float m_fMinCutoffFreq;
float m_fMaxCutoffFreq;

// function to calculate the fc given the LFO sample
float calculateCutoffFreq(float fLFOSample);

// calculate the coeffs for a given filter
void calculateLPFCoeffs(float fCutoffFreq, float fQ, CBiQuad* pFilter);

// END OF USER CODE ------------------------------------------------- //
```

# 12.1.4 ModFilter.cpp File

# Constructor

+   * Initialize the rate min and max values. The objects are self initializing upon creation.

```
CModFilter::CModFilter()
{
	<SNIP SNIP SNIP>

	// Finish initializations here

	// set our Min and Max Modulation points
	m_fMinCutoffFreq = 100.0;
	m_fMaxCutoffFreq = 5000.0;
}
```

Write the calculateCutoffFrequency() function. This function behaves exactly like the function in the flanger to calculate a new delay offset given the LFO sample and mod depth values. Here, we simply calculate the cutoff frequency between the min and max values according to the LFO sample and depth.

```
float CModFilter::calculateCutoffFreq(float fLFOSample)
{
	return (m_fMod_Depth_fc/100.0)*(fLFOSample*(
		m_fMaxCutoffFreq - m_fMinCutoffFreq)) + m_fMinCutoffFreq;
}
```

Next, we need to implement the cooking function for the LPFs to set the new coefficients for a given $f_c$ and $Q$ value. This is identical to the resonant LPF you designed in Chapter 6: