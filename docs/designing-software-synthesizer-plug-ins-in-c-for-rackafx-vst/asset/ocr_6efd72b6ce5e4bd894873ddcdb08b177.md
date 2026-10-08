```
if(!s.readInt32(udata)) return kResultFalse;
else
    setParamNormalizedFromFile(OSC_WAVEFORM, (ParamValue)udata);

if(!s.readInt32(udata)) return kResultFalse;
else
    setParamNormalizedFromFile(LF01_WAVEFORM, (ParamValue)udata);

if(!s.readDouble(dDoubleParam)) return kResultFalse;
else
    setParamNormalizedFromFile(LF01_RATE, dDoubleParam);

if(!s.readDouble(dDoubleParam)) return kResultFalse;
else
    setParamNormalizedFromFile(LF01_AMPLITUDE, dDoubleParam);

if(!s.readInt32(udata)) return kResultFalse;
else
    setParamNormalizedFromFile(LF01_MODE, (ParamValue)udata);

// --- do next version...
if (version >= 1)
{
    // add v1 stuff here
}

return kResultTrue;
```