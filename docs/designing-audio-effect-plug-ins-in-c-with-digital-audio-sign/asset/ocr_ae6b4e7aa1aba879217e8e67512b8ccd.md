```
case 3:
{
    m_LeftDetector.setReleaseTime(m_fRelease_mSec);
    m_RightDetector.setReleaseTime(m_fRelease_mSec);
    break;
}
case 42:
{
    if(m_uTimeConstant == Digital)
    {
        m_LeftDetector.setTCModeAnalog(false);
        m_RightDetector.setTCModeAnalog(false);
    }
    else
    {
        m_LeftDetector.setTCModeAnalog(true);
        m_RightDetector.setTCModeAnalog(true);
    }
}
default:
    break;
}
return true;
}
```

# processAudioFrame()

+   - Follow the block diagram to complete the operations.
+   - Apply input gain to detector.
+   - Detect input sample.
+   - Calculate gain.
+   - Apply dynamic gain reduction and static make-up gain.

```
bool __stdcall CDynamicsProcessor::processAudioFrame(float* pInputBuffer, float*
    pOutputBuffer, UINT
    uNumInputChannels, UINT
    uNumOutputChannels)
{
    // output <- input -- change this for meaningful processing
    // Do LEFT (MONO) Channel; there is always at least one input, one output
    // calculate gains
    float fInputGain = pow(10.0, m_fInputGain_dB/20.0);
    float fOutputGain = pow(10.0, m_fOutputGain_dB/20.0);

    // detect left channel
    float fLeftDetector = m_LeftDetector.detect(pInputBuffer[0]);
```