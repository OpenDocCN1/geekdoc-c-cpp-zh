```
return noErr;
break;
}
case LF01_AMPLITUDE:
{
setUParameterInfo(outParameterInfo, CFSTR("LFO Amp"),
CFSTR(""), MIN_UNIPOLAR, MAX_UNIPOLAR,
DEFAULT_UNIPOLAR);
return noErr;
break;
}
case LF01_MODE:
{
setUParameterInfo(outParameterInfo, CFSTR("LFO Mode"),
CFSTR(""), MIN_LFO_MODE, MAX_LFO_MODE,
DEFAULT_LFO_MODE, false, true);
return noErr;
break;
}
}return kAudioUnitErr_InvalidParameter;
```