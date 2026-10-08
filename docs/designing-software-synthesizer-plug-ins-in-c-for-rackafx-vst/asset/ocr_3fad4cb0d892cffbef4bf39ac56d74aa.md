```
m_dFeedbackPct = cookVSTGUIVariable(MIN_DELAY_FEEDBACK,
MAX_DELAY_FEEDBACK,
value);

break;
}
```

```
case DELAY_RATIO {
m_dDelayRatio = cookVSTGUIVariable(MIN_DELAY_RATIO,
MAX_DELAY_RATIO,
value);
```

```
case DELAY_WET_MIX: {
m_dWetMix = cookVSTGUIVariable(MIN_DELAY_WET_MIX,
MAX_DELAY_WET_MIX, value);
break;
}
```

```
case DELAY_MODE {
m_uDelayMode = (UINT)cookVSTGUIVariable(MIN_DELAY_MODE,
MAX_DELAY_MODE,
value);
break;
}
```

```
etc...
tresult PLUGIN_API Processor::process(ProcessData& data) {
```

```
// --- check for conrol chages and update synth if needed
doControlUpdate(data);
```

<SNIP SNIP SNIP and Indents Removed>

Download the Korg Triton Parameter Guide at