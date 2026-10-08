```
bool Processor::doControlUpdate(ProcessData& data)
{
  <SNIP SNIP SNIP Indents Removed>

  switch (pid)
  {
    // cookVSTGUIVariable(min, max, currentValue) - cooks raw data into
    // meaningful info for for us
    case OSC1_AMPLITUDE_DB:
    {
      m_d0sc1Amplitude_dB = cookVSTGUIVariable(MIN_OUTPUT_AMPLITUDE_DB,
                              MAX_OUTPUT_AMPLITUDE_DB,
                              value);

      break;
    }

    case OSC2_AMPLITUDE_DB:
    {
      m_d0sc2Amplitude_dB = cookVSTGUIVariable(MIN_OUTPUT_AMPLITUDE_DB,
                              MAX_OUTPUT_AMPLITUDE_DB,
                              value);

      break;
    }

    case LOOP_MODE:
    {
      m_uLoopMode = (UINT)cookVSTGUIVariable(MIN_LOOP_MODE,
                              MAX_LOOP_MODE, value);

      break;
    }
  }
```