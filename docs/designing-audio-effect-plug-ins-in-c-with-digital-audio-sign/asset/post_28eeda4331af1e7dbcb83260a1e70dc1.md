
## prepareForPlay()

```cpp
bool __stdcall CReverb::prepareForPlay()
{
// Add your code here:
// up to 2 seconds predelay
m_PreDelay.init(2.0f*(m_nSampleRate));

// init up to 100 mSec
m_InputAPF_1.init(0.1f*(m_nSampleRate));
m_InputAPF_2.init(0.1f*(m_nSampleRate));

// 100 mSec each max
m_ParallelECF_1.init(0.1f*(m_nSampleRate));
m_ParallelECF_2.init(0.1f*(m_nSampleRate));
m_ParallelECF_3.init(0.1f*(m_nSampleRate));
m_ParallelECF_4.init(0.1f*(m_nSampleRate));
m_ParallelECF_5.init(0.1f*(m_nSampleRate));
m_ParallelECF_6.init(0.1f*(m_nSampleRate));
m_ParallelECF_7.init(0.1f*(m_nSampleRate));
m_ParallelECF_8.init(0.1f*(m_nSampleRate));

// 100 mSec each max
m_OutputAPF_3.init(0.1f*(m_nSampleRate));
m_OutputAPF_4.init(0.1f*(m_nSampleRate));

// init the three LPFs
m_InputLPF.init();
m_DampingLPF1.init();
m_DampingLPF2.init();

// Call all delay resets
m_PreDelay.resetDelay();
m_InputAPF_1.resetDelay();
m_InputAPF_2.resetDelay();

m_ParallelECF_1.resetDelay();
m_ParallelECF_2.resetDelay();
m_ParallelECF_3.resetDelay();
m_ParallelECF_4.resetDelay();
m_ParallelECF_5.resetDelay();

m_ParallelECF_6.resetDelay();
m_ParallelECF_7.resetDelay();
m_ParallelECF_8.resetDelay();

m_OutputAPF_3.resetDelay();
m_OutputAPF_4.resetDelay();

// set sample rates on combs (needed to calc g values)
m_ParallelECF_1.setSampleRate(this->m_nSampleRate);
m_ParallelECF_2.setSampleRate(this->m_nSampleRate);
m_ParallelECF_3.setSampleRate(this->m_nSampleRate);
m_ParallelECF_4.setSampleRate(this->m_nSampleRate);
m_ParallelECF_5.setSampleRate(this->m_nSampleRate);
m_ParallelECF_6.setSampleRate(this->m_nSampleRate);
m_ParallelECF_7.setSampleRate(this->m_nSampleRate);
m_ParallelECF_8.setSampleRate(this->m_nSampleRate);

// flush buffers
m_InputLPF.init();
m_DampingLPF1.init();
m_DampingLPF2.init();

// cook everything
cookVariables();
return true;
}
```

## userInterfaceChange()

- Call the one and only cooking function

```cpp
bool __stdcall CReverb::userInterfaceChange(int nControlIndex)
{
    // add your code here
    cookVariables();
    return true;
}
```

## processAudioFrame()

In this function, you tie all the member objects together by creating variables to pass into/out of their processAudio() functions. By stepping through the code, you can see just how the series and parallel elements are connected. You can always go back and make this code more streamlined by removing intermediate variables, and so on. The four outputs of each comb filter bank are mixed at 15% ratios with alternating signs.

```cpp
bool __stdcall CReverb::processAudioFrame(float* pInputBuffer, float* pOutputBuffer, UINT uNumInputChannels, UINT uNumOutputChannels)
{
    //
    // output = input - change this for meaningful processing
    //
    // Form our input - L + R (if there is a R)
    //
    float fInputSample = pInputBuffer[0];
    if(uNumInputChannels == 2)
    {
        // mix
        fInputSample += pInputBuffer[1];
        // attenuate by 0.5
        fInputSample *= 0.5;
    }
    // begin the series/parallel signal push
    // Pre-Delay
    float fPreDelayOut = 0;
    m_PreDelay.processAudio(&fInputSample, &fPreDelayOut);
    // Pre-Delay Out -> fAPF_1_Out
    float fAPF_1_Out = 0;
    m_InputAPF_1.processAudio(&fPreDelayOut, &fAPF_1_Out);
    // fAPF_1_Out -> fAPF_2_Out
    float fAPF_2_Out = 0;
    m_InputAPF_2.processAudio(&fAPF_1_Out, &fAPF_2_Out);
    // fAPF_2_Out -> fInputLPF
    float fInputLPF = 0;
    m_InputLPF.processAudio(&fAPF_2_Out, &fInputLPF);

    // comb filter bank
    // variables for each output
    float fPC1_Out = 0;
    float fPC2_Out = 0;
    float fPC3_Out = 0;
    float fPC4_Out = 0;
    float fPC5_Out = 0;
    float fPC6_Out = 0;
    float fPC7_Out = 0;
    float fPC8_Out = 0;
    float fC1_Out = 0;
    float fC2_Out = 0;

    // fInputLPF -> fPC1_Out, fPC2_Out, fPC3_Out, fPC4_Out
    m_ParallelECF_1.processAudio(&fInputLPF, &fPC1_Out);
    m_ParallelECF_2.processAudio(&fInputLPF, &fPC2_Out);
    m_ParallelECF_3.processAudio(&fInputLPF, &fPC3_Out);
    m_ParallelECF_4.processAudio(&fInputLPF, &fPC4_Out);

    // fInputLPF -> fPC5_Out, fPC6_Out, fPC7_Out, fPC8_Out
    m_ParallelECF_5.processAudio(&fInputLPF, &fPC5_Out);
    m_ParallelECF_6.processAudio(&fInputLPF, &fPC6_Out);

    m_ParallelECF_7.processAudio(&fInputLPF, &fPC7_Out);
    m_ParallelECF_8.processAudio(&fInputLPF, &fPC8_Out);

    // form outputs: note attenuation by 0.15 for each and alternating signs
    fC1_Out = 0.15*fPC1_Out - 0.15*fPC2_Out + 0.15*fPC3_Out - 0.15*fPC4_Out;
    fC2_Out = 0.15*fPC5_Out - 0.15*fPC6_Out + 0.15*fPC7_Out - 0.15*fPC8_Out;

    // fC1_Out -> fDampingLPF_1_Out
    float fDampingLPF_1_Out = 0;
    m_DampingLPF1.processAudio(&fC1_Out, &fDampingLPF_1_Out);

    // fC2_Out -> fDampingLPF_2_Out
    float fDampingLPF_2_Out = 0;
    m_DampingLPF2.processAudio(&fC2_Out, &fDampingLPF_2_Out);

    // fDampingLPF_1_Out -> fAPF_3_Out
    float fAPF_3_Out = 0;
    m_OutputAPF_3.processAudio(&fDampingLPF_1_Out, &fAPF_3_Out);

    // fDampingLPF_2_Out -> fAPF_4_Out
    float fAPF_4_Out = 0;
    m_OutputAPF_4.processAudio(&fDampingLPF_2_Out, &fAPF_4_Out);

    // form output = ((100-Wet)/100*x(n) + (Wet/100)*fAPF_3_Out
    pOutputBuffer[0] = ((100.0 - m_fWet_pct)/100.0)*fInputSample +
    (m_fWet_pct/100.0)*(fAPF_3_Out);

    // Do RIGHT Channel if there is one
    if(uNumOutputChannels == 2)
    {
    // form output = ((100-Wet)/100*x(n) + (Wet/100)*fAPF_4_Out
    pOutputBuffer[1] = ((100.0 - m_fWet_pct)/100.0)*fInputSample +
    (m_fWet_pct/100.0)*(fAPF_4_Out);
    }

    return true;
}
```

Build and test the example reverb module. Use RackAFX's impulse response tool in the analyzer to tweak your settings. Adjust the impulse response time according to your RT60 times. Notice how the impulse response can drastically change with only a slight modification of the parameters. Also, try adjusting the mix coefficients for the comb filter outputs by alternating signs or using different weightings. Visit the website www.willpirkle.com for more example reverb algorithms and code.

## 11.18 Challenge

Design your own reverb. Start by implementing some of the classics (Schroeder, Moorer) and some of the more recent versions (Gardner, Jot, Dattorro) combining different modules. Or start with the reverb design here and modify it. For example, try replacing the APFs with nested all-pass modules or add or remove comb filters. You can easily identify ringing and oscillations using the impulse response tool, so keep it open as you experiment.

## Bibliography

Griesinger, D. 1995. How loud is my reverberation? Journal of the Audio Engineering Society, preprint 3943, pp. 1–11.

Roads, C. 1996. The Computer Music Tutorial, Chapter 3. Cambridge, MA: The MIT Press.

## References

Beranek, L. 1986. Acoustics. New York: American Institute of Physics.

Browne, S. 2001. “Hybrid reverberation algorithm using truncated impulse response convolution and recursive filtering.” Master’s diss., University of Miami, Miami, FL.

Chemstrum, M., Marcolini, K., and Pirkle, W. 2012. Generating matrix coefficients for feedback delay networks using genetic algorithms. Journal of the Audio Engineering Society, preprint N/A.

Dahl, L. and Jot, J-M. 2000. A reverberator based on absorbent all-pass filters. Proceedings of the COST G-6 Convention on Digital Audio Effects, DAFX-00. pp. 1–6.

Dattorro, J. 1997. Effect design part 1: Reverberators and other filters. Journal of the Audio Engineering Society 45(9): 660–665.

Frenette, J. 2000. “Reducing artificial reverberation requirements using time-variant feedback delay networks.” Master’s diss., University of Miami, Miami, FL.

Gardner, W. G. 1992. “The virtual acoustic room.” Master’s diss., Massachusetts Institute of Technology, Boston, MA.

Gardner, W. G. 1995. Efficient convolution without input-output delay. Journal of the Audio Engineering Society 43(3): 127–135.

Gerzon, M. A. Synthetic stereo reverberation. Studio Sound Magazine, January 14, 1972.

Griesinger, D. 1989. Practical processors and programs for digital reverberation. 7th International Conference of the Audio Engineering Society, pp. 187–195.

Jot, J-M. and Chaigne, A. 1991. Digital delay networks for designing artificial reverberators. Journal of the Audio Engineering Society, preprint 3030, pp. 1–16.

Jot, J-M. 1992. “Design and implementation of a sound spatializer based on physical and perceptual models.” PhD diss., Telecom, Paris.

Kahrs, M. and Brandenberg, K. 1998. Applications of Digital Signal Processing to Audio and Acoustics, Chapter 3. Boston: Kluwer Academic Publishers.

Kuttroff, H. 1991. Room Acoustics. New York: Elsevier.

Moorer, J. A. 1979. About this reverberation business. Computer Music Journal 3(2): 13–28.

Reilly, A. and McGrath, D. S. 1995. Convolution processing for realistic reverb. Journal of the Audio Engineering Society, preprint 3977, pp. 1–8.

Sabina, W. 1973 “Reverberation.” Lindsay, R. B., ed., Acoustics: Historical and Philosophical Development. Stroudsburg, PA: Dowden, Hutchinson & Ross.

Schroeder, M. 1962. Natural-sounding artificial reverberation. Journal of the Audio Engineering Society 10(3): 209–213.

Schroeder, M. 1984. Progress in architectural acoustics and artificial reverberation: Concert hall acoustics and number theory. Journal of the Audio Engineering Society 32(4): 194–202.

Smith, J. O. 1985. A new approach to digital reverberation using closed waveguide networks. Proceedings of the 1985 International Computer Music Conference, pp. 47–53.

Smith, J. O. and Rocchesso, D. 1994. Connections between feedback delay networks and waveguide networks for digital reverberation. Proceedings of the 1994 International Computer Music Conference, pp. 376–377.

Stautner, J. and Puckette, M. 1982. Designing multi-channel reverberators. Computer Music Journal 6(1): 52–65.
