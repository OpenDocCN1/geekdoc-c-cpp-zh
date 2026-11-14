
## Modulated Filter Effects

Modulated filter effects alter one or more filter parameters with other signals called control signals. The filter parameters might include cutoff frequency, Q, bandwidth, filter type, or overall gain. The control signals are usually periodic low-frequency oscillators (LFOs), a signal envelope, an envelope generator (EG) or even another audio signal. In the modulated delay effects, the LFO control signal changed the delay amount of the signal. In modulated filter effects, the filter parameters are the ones that are changing. In this chapter you will design and implement the following effects:

- Mod filter using an LFO
- Envelope follower using an audio detector
- Phaser

The phaser is a specialized effect that uses a bank of all-pass filters (APFs) to try to brute force delay the signal to make a flanging effect. An LFO modulates the depth of the APFs. In Figure 12.1 you can see a simple modulated filter. The filter type is a low-pass filter (LPF). The control signal is an LFO. The control parameter is the cutoff frequency of the filter.

In Figure 12.2, an EG moves the filter parameter. An EG is triggered by some external event, such as a note-on or note-off event, or possibly triggered when the input level crosses a threshold. A modulated filter might have multiple parameters controlled by multiple control signals. For example, Figure 12.3 shows another LPF that has two modulation sources for two different parameters.

In Figure 12.3 you can see a new module labeled envelope detector; it detects and follows the peak, mean-squared (MS), or root-mean-squared (RMS) value of the control signal which is the input signal here. The control signal could be taken from other sources such as another audio signal or a complex LFO signal. The effect in Figure 12.2 has a special name too: it is called an envelope follower.

![](img/b54974d0a4317ec82d7ae02126d10a6f_392_0.png)

Figure 12.1: A simple LFO-modulated LPF.

![](img/b54974d0a4317ec82d7ae02126d10a6f_393_0.png)

Figure 12.2: An envelope generator can also modulate a filter parameter.

![](img/b54974d0a4317ec82d7ae02126d10a6f_393_1.png)

Figure 12.3: A doubly modulated LPF with both $f_c$ and $Q$ controls.

## 12.1 Design a Mod Filter Plug-In: Part I Modulated $f_c$

For our first effect design, we'll start with a modulated second-order LPF and modulate the cutoff frequency with an LFO. Then, we can increase the complexity by adding another LFO to control the Q and even give the option to run the two LFOs in quadrature phase. We can use the second-order digital resonant LPF you've already designed from Chapter 6 for the filter. Notice that for this initial project, we will hold the LPF Q constant at 2.0. And, we will introduce a built-in RackAFX object to handle the LFO for us. The block diagram is shown in Figure 12.4.

The parameters are as follows:

- $f_c$ mod rate (0.2 to 10 Hz)
- $f_c$ mod depth (0 to 100%)
- LFO type (sine, tri, saw, square)
- LPF Q: fixed at 2.0
- $f_c$ mod range: 100 Hz to 5 kHz
- LPF is fixed as second-order bi-quad variety

By now, you should be getting really good at building RackAFX plug-ins. If you haven't just been cutting and pasting the code then you will have no problems with the next chapters. We can use the digital resonant LPF from Chapter 6 along with the built-in wave table oscillator object to quickly implement the mod filter effect. This project will use two built-in objects:

1. CBiquad for the filter
2. CWaveTable for the LFO

![](img/b54974d0a4317ec82d7ae02126d10a6f_394_0.png)

Figure 12.4: The mod filter block diagram.

You used CBiquad in Chapter 6 to begin your filtering work. The CWaveTable object was taken directly from your WTOscillator object. You can find the definition and implementation in the pluginconstants.h and pluginobjs.cpp files. Table 12.1 shows the object's members and attributes. The flow chart for processAudioFrame() is shown in Figure 12.5.

### 12.1.1 Project: ModFilter

Create the project; because we are using built-in objects for the filter and LFO there are no member objects to add.

### 12.1.2 ModFilter GUI

For the initial design, you will need the following slider controls in Table 12.2. Note that these LFO waveform enumerations follow exactly that of the built-in CWaveTable object to make mapping the button control easy.

### 12.1.3 ModFilter.h File

Declare instances of the BiQuad and WaveTable objects. You don't need #include anything since these are built-in:

```
// Add your code here:-----------------------------------------------//
// BiQuad Objects
CBiquad m_LeftLPF;
CBiquad m_RightLPF;

// one LFO for the fc
CWaveTable m_fcLFO;
//-----------------------------------------------//
// END OF USER CODE
```

We are also going to need some variables and functions to control the effect. Specifically, we need:

- Minimum fc variable
- Maximum fc variable
- Function to calculate the current fc given a LFO value
- Functions to calculate the bi-quad coefficients for left and right channels independently (we want to calculate them separately for the third part of the project where we allow for quad-phase LFOs)

Table 12.1: The CWaveTable object interface.

| CWaveTable | |
| Member Variables | Purpose |
| --- | --- |
| float m_SinArray[1024]; float m_SawtoothArray[1024]; float m_TriangleArray[1024]; float m_SquareArray[1024]; | Arrays to store the non-band limited wave tables |
| float m_SawtoothArray_BL5[1024]; float m_TriangleArray_BL5[1024]; float m_SquareArray_BL5[1024]; | Arrays to hold the band-limited wave tables |
| float m_fReadIndex; float m_fQuadPhaseReadIndex; | Indices for reading the wave table |
| float m_f_inc; | Table increment value for current output frequency |
| int m_nSampleRate; | Sample rate IMPORTANT: Needed for calculation of table inc; do not forget it! |
| float m_fFrequency_Hz; | Oscillator frequency |
| bool m_bInvert; | Flag to invert output |
| UINT m_uOscType; enum{sine, saw, tri, square}; | Enumerated unsigned integer type (UINT) for osc waveform type |
| UINT m_uTableMode; enum{normal, bandlimit}; | Enumerated UINT for table mode (we will use normal mode in this plug-in since the oscillator is a LFO) |
| UINT m_uPolarity; enum{bipolar, unipolar}; | Enumerated UINT for osc polarity (we will use unipolar for this plug-in) |
| Member Functions | |
| void doOscillate(float* pYn, float* pYqn) Parameters: • float* pYn • float* pYqn | The oscillate function Output: pYn is the normal output Output: pYqn is the quadrature phase output |
| bool prepareForPlay() | The prepareForPlay() function for the oscillator; same use as a normal plug-in |
| void reset () | Reset the pointers to top |
| void setSampleRate(int nSampleRate) | Called by parent to set the sample rate in Hz |
| Parameters: • int nSampleRate | Input: the current sample rate |
| void cookFrequency() | Calculates the new inc value for a changed oscillation frequency |

![](img/b54974d0a4317ec82d7ae02126d10a6f_396_0.png)

Figure 12.5: The flowchart for the mod filter process function.

Table 12.2: GUI controls for the ModFilter.

| Slider Property | Value |
|---|---|
| Control Name | Mod Depth fc |
| Units | % |
| Variable Type | float |
| Variable Name | m_fMod_Depth_fc |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 50 |

| Slider Property | Value |
|---|---|
| Control Name | Mod Rate fc |
| Units | Hz |
| Variable Type | float |
| Variable Name | m_fModRate_fc |
| Low Limit | 0.2 |
| High Limit | 10 |
| Initial Value | 1.0 |

| Slider Property | Value |
|---|---|
| Control Name | LFO |
| Units | |
| Variable Type | enum |
| Variable Name | m_uLFO_waveform |
| Enum String | sine, saw, tri, square |

Add the following to the .h file:

```
// Add your code here: ------------------------------------------------ //
// BiQuad Objects
CBiquad m_LeftLPF;
CBiquad m_RightLPF;

// one LFO for the fc
CWaveTable m_fcLFO;

// min and max values (to make it easy to change later)
float m_fMinCutoffFreq;
float m_fMaxCutoffFreq;

// function to calculate the fc given the LFO sample
float calculateCutoffFreq(float fLFOSample);

// calculate the coeffs for a given filter
void calculateLPFCoeffs(float fCutoffFreq, float fQ, CBiquad* pFilter);

// END OF USER CODE ------------------------------------------------- //
```

### 12.1.4 ModFilter.cpp File

### Constructor

- Initialize the rate min and max values. The objects are self initializing upon creation.

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
