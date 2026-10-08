```
void Processor::update(
{
    <SNIP SNIP SNIP>
    // --- DCA controls
    m_DCA.setPanControl(m_dPanControl);
    m_DCA.setAmplitude_dB(m_dVolume_dB);
    m_DCA.update();

    // --- filter controls
    m_Filter1.m_dFcControl = m_dFcControl;
    m_Filter1.setQControl(m_dQControl);
    m_Filter1.update();

}
```

```
bool __stdcall Processor::process(args...)
{
    <SNIP SNIP SNIP and Indents Removed>
    for(int32 j=0; j<samplesToProcess; j++)
{
        // --- clear accumulators
        dOutL = 0.0;
        dOutR = 0.0;
        if(m_Osc1.m_bNoteOn)
        {
            << INSERT ** Code Listing 7.1: Audio Rendering ** >>
            // write out to buffer
            buffers[0][j] = dOutL; // left
            buffers[1][j] = dOutR; // right
        }
    }
```

etc...