
$K = \tan(\pi f_c/f_s)$
$V_0 = 10^{boost/cut \, dB/20}$
$d_0 = 1 + \frac{1}{Q}K + K^2$ (6.43)
$e_0 = 1 + \frac{1}{V_0 Q}K + K^2$

| | Boost | Cut |
|---|---|---|
| $\alpha = 1 + \frac{V_0}{Q}K + K^2$ | $a_0 = \frac{\alpha}{d_0}$ | $a_0 = \frac{d_0}{e_0}$ |
| $\beta = 2(K^2 - 1)$ | $a_1 = \frac{\beta}{d_0}$ | $a_1 = \frac{\beta}{e_0}$ |
| $\gamma = 1 - \frac{V_0}{Q}K + K^2$ | $a_2 = \frac{\gamma}{d_0}$ | $a_2 = \frac{\delta}{e_0}$ |
| $\delta = 1 - \frac{1}{Q}K + K^2$ | $b_1 = \frac{\beta}{d_0}$ | $b_1 = \frac{\beta}{e_0}$ |
| $\eta = 1 - \frac{1}{V_0 Q}K + K^2$ | $b_2 = \frac{\delta}{d_0}$ | $b_2 = \frac{\eta}{e_0}$ |
| | $c_0 = 1.0$ | $c_0 = 1.0$ |
| | $d_0 = 0.0$ | $d_0 = 0.0$ |

![](img/b54974d0a4317ec82d7ae02126d10a6f_192_0.png)

Figure 6.32: A set of responses for the constant-Q parametric/peaking filter with a variety of boost/cut settings. \(f_c = 1 \, \text{kHz}, Q = 2\).

## 6.7.5 Cascaded Graphic EQ: Non-Constant-Q

Specify:

- \(f_c\), center frequency
- Gain/attenuation in dB

The graphic EQ is a fixed Q variation on the parametric EQ. In a graphic EQ, the user only has control over the boost and cut of a set of filters tuned to fixed center frequencies. The Q that is used will depend on the boost or cut settings as well as the number of bands of EQ. For non-constant-Q graphic EQs, the method of finding the proper Q can be difficult because the bandwidth will change for various settings of the boost/cut. The value for Q is sometimes chosen so that when all the controls are set to the maximum boost or cut values, the frequency response is as flat as possible.

The Q for constant-Q filters is easy to calculate knowing the number of bands split across the 10 octaves of audio. It is a good starting point for developing a non-constant-Q EQ plug-in; experimentation may be needed to find the ideal Q for your particular design. You might also allow the user to adjust the value within reason. The equation relating Q to the number of EQ bands is Equation 6.44.

```
N = \frac{\text{Number of modules}}{10}

Q = \frac{\sqrt{2^N}}{2^N - 1}

(6.44)
```

For a 10-band graphic EQ, Q = 1.414, while for a 31-band (aka 1/3 octave) EQ, Q = 4.32. The center frequencies of the bands are usually found with the following International Organization for Standardization (ISO) standard equation:

```
q = \frac{\text{Number of bands}}{10}

f_n = 1000 * 2^{n/q}

n = 0, \pm 1, \pm 2, \pm 3, \text{ etc ...}

(6.45)
```

For a 10-band EQ, this works out (with rounding) to 32 Hz, 64 Hz, 125 Hz, 250 Hz, 500 Hz, 1 kHz, 2 kHz, 4 kHz, 8 kHz, and 16 kHz.

The cascaded graphic EQ topology is shown in Figure 6.33. It consists of a simple series cascade of each of the filter modules. The non-constant-Q graphic uses the same non-constant-Q peaking filter algorithm, but with the Q fixed according to Equation 6.42. You can get a good feel for how the Q affects the overall response by looking at a plot with all controls set to the maximum boost (or cut). For a 10-band non-constant-Q graphic, we observe the combined response shown in Figure 6.34.

## 6.7.6 Cascaded Graphic EQ: Constant-Q

Specify:

- f_c, center frequency
- Gain/attenuation in dB

![](img/b54974d0a4317ec82d7ae02126d10a6f_193_0.png)

Figure 6.33: The cascaded graphic EQ topology; this is for a 10-band design using the ISO center frequencies. The design equations for each module use the non-constant-Q algorithm above.

![](img/b54974d0a4317ec82d7ae02126d10a6f_194_0.png)

Figure 6.34: At the prescribed constant-Q value of Q = 1.414 we observe rippling and an increased high-frequency response with all controls at maximum boost.

![](img/b54974d0a4317ec82d7ae02126d10a6f_194_1.png)

Figure 6.35: The cascaded graphic EQ topology; this is for a 10-band design using the exact unrounded ISO center frequencies. The design equations for each module use the constant-Q algorithm above.

![](img/b54974d0a4317ec82d7ae02126d10a6f_194_2.png)

Figure 6.36: The 10-band constant-Q graphic EQ with the prescribed Q = 1.414 produces less low-frequency rippling and a decreased high-frequency response with all controls at maximum boost.

The constant-Q graphic EQ follows the same design pattern (Figure 6.35) except that you use the constant-Q peaking filter in each of the modules. The equations for finding the center frequencies and Q are the same as above. Bohn (1986) recommends not rounding the ISO center frequencies but rather use the exact values. Figure 6.36 shows the composite response with all controls set to full boost.

## 6.8 Design a Resonant LPF Plug-In

We'll continue with a resonant LPF design. The filter will use the second-order bilinear transform design and the bi-quad structure for implementation. After that you will redesign the filter using the Massberg technique for analog emulation and examine the differences. Note: This filter is found in RackAFX's module menu item under “HP/LP Filter” for you to experiment with and use to check your own implementations.

For this project, we'll be using our first built-in object. I've already prepared a bi-quad object for you to use in this (or any other) project. It is not a RackAFX plug-in but rather a simple C++ object that accomplishes only one task: the bi-quad structure realization. The bi-quad can be used to make any first- or second-order feed-forward or feed-back type filter. Let's take a moment to check out the CBiquad object. You can find the interface in the pluginconstants.h file and the implementation in the pluginobjects.cpp files, respectively. The CBiquad object has the members and variables in Table 6.2.

Table 6.2: The CBiquad object interface.

| CBiquad |
| --- |
| Member Variables | Purpose |
| protected: float m_f_Xz_1 float m_f_Xz_2 float m_f_Yz_1 float m_f_Yz_2 | Implements the four delay elements needed for the bi-quad: x(n - 1), x(n - 2), y(n - 1) and y(n - 2) in these protected variables |
| public: float m_f_a0 float m_f_a1 float m_f_a2 float m_f_b1 float m_f_b2 | The filter coefficients |
| Member Functions | |
| void flushDelays() | Initialize all delay elements with 0.0s |
| float doBiQuad(float f_xn) | Do one cycle of filter operation; return value is y(n) |
| Parameters | |
| - float f_xn | Input: the current input sample, x(n) |

### 6.8.1 Project: ResonantLPF

Create the project and name it “ResonantLPF,” then add the sliders for the graphical user interface (GUI).

### 6.8.2 ResonantLPF GUI

Figure 6.37 shows what your final GUI will look like. You will need the controls shown in Table 6.3.

![](img/b54974d0a4317ec82d7ae02126d10a6f_196_0.png)

Figure 6.37: The resonant LPF GUI.

Table 6.3: The GUI controls for the resonant LPF.

| Slider Property | Value |
|---|---|
| Control Name | Fc |
| Units | Hz |
| Variable Type | float |
| Variable Name | m_f_fc_Hz |
| Low Limit | 100 |
| High Limit | 5000 |
| Initial Value | 1000 |

| Slider Property | Value |
|---|---|
| Control Name | Q |
| Units | |
| Variable Type | float |
| Variable Name | m_f_Q |
| Low Limit | 0.5 |
| High Limit | 20 |
| Initial Value | 0.707 |

### 6.8.3 ResonantLPF.h File

RackAFX provides you with the built-in bi-quad object named CBiquad and you don't need to do anything at all to add it to your project. You can just declare your bi-quad objects directly in the .h file like you would any other object:

```
CBiquad m_LeftLPF; // or whatever you like to name it
```

Here's my .h file with the left and right LPF objects declared:

```
// Add your code here:-------------------------------------------------- //
CBiquad m_LeftLPF;
CBiquad m_RightLPF;
// END OF USER CODE -------------------------------------------------- //
```

We'll also need a function to calculate the bi-quad's coefficients ($a_0, a_1, a_2, b_1,$ and $b_2$) and we can share this between the left and right objects (i.e., both LPFs will have the same cutoff and $Q$, so they will also have the same coefficients). Declare this now:

```
// Add your code here:-------------------------------------------------- //
CBiquad m_LeftLPF;
CBiquad m_RightLPF;

void calculateLPFCoeffs(float fCutoffFreq, float f0);
// END OF USER CODE -------------------------------------------------- //
```

### 6.8.4 ResonantLPF.cpp File

Write the calculateLPFCoeffs() function in the .cpp file by using Equation 6.35. I have used the same intermediate coefficient names here too.

```
void CResonantLPF::calculateLPFCoeffs(float fCutoffFreq, float f0)
{
    // use same terms as in book:
    // Moat theta_c = 2.0*pi*fCutoffFreq/(float)m_nSampleRate;
    float d = 1.0/f0;

    // intermediate values
    float fBetaNumerator = 1.0 - ((d/2.0)*(sin(theta_c)));
    float fBetaDenominator = 1.0 + ((d/2.0)*(sin(theta_c)));

    // beta
    float fBeta = 0.5*(fBetaNumerator/fBetaDenominator);

    // gamma
    float fGamma = (0.5 + fBeta)*(cos(theta_c));

    // alpha
    float fAlpha = (0.5 + fBeta - fGamma)/2.0;

    // left channel
    m_LeftLPF.m_f_a0 = fAlpha;
    m_LeftLPF.m_f_a1 = 2.0*fAlpha;
    m_LeftLPF.m_f_a2 = fAlpha;
    m_LeftLPF.m_f_b1 = -2.0*fGamma;
    m_LeftLPF.m_f_b2 = 2.0*fBeta;

    // right channel
    m_RightLPF.m_f_a0 = fAlpha;
    m_RightLPF.m_f_a1 = 2.0*fAlpha;
    m_RightLPF.m_f_a2 = fAlpha;
    m_RightLPF.m_f_b1 = -2.0*fGamma;
    m_RightLPF.m_f_b2 = 2.0*fBeta;
}
```
