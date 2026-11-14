# prepareForPlay()

+   - Initialize the LFO.
+   - Forward the prepareForPlay() method to the LFO.

```
bool __stdcall CTremoloPanner::prepareForPlay()
{
    // Add your code here:
    m_LFO.m_fFrequency_Hz = m_fModRate;
    m_LFO.m_uPolarity = m_uMode == Panner ? 0 : 1; // 0 - bipolar, 1 - unipolar
    m_LFO.m_uTableMode = 0; // normal, no band limiting
    m_LFO.m_u0sCtype = m_uLFO_Waveform;
    m_LFO.setSampleRate(m_nSampleRate); // really important!

    // the LFO prepareForPlay() calls reset() and cookFrequency()
    m_LFO.prepareForPlay();

    return true;
}
```

# userInterfaceChange()

+   - Decode the control index and update variables as needed.
+   - Note: Make sure you check your nControlIndex values to match your GUI.

```
bool __stdcall CTremoloPanner::userInterfaceChange(int nControlIndex)
{
    // decode the control index, or delete the switch and use brute force calls
    // switchInControlIndex
    {
    case 0:
    {
        m_LFO.m_fFrequency_Hz = m_fModRate;
        m_LFO.cookFrequency();
        break;
    }

    // 41: LFO Waveform change
    case 41:
    {
        m_LFO.m_u0sCtype = m_uLFO_Waveform;
        break;
    }

    case 42:
    {
        if(m_uMode == Panner)
        m_LFO.m_uPolarity = 0; // 0 - bipolar, 1 - unipolar
        else // is tremolo
        m_LFO.m_uPolarity = 1; // 0 - bipolar, 1 - unipolar
        break;
    }
    }
}
```

# processAudioFrame()

+   - Generate the LFO value.
+   - Calculate the channel gain values according to the mode.

In processAudioFrame() we need to generate a new LFO value, calculate the new gain factor, then