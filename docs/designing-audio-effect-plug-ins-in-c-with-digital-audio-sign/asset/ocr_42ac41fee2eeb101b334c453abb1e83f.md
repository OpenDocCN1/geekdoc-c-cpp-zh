In the same file, you create constant definitions for the initial value and name.

```
// set the initial value
static const Float kDefaultValue_ParamOne = 0.5;

// set the name; CFStringRef is a Core Foundation String object
static CFStringRef kParameterOneName = CFSTR("Volume");
```

You declare your controls by filling in the GetParameterInfo() method. It is beyond the scope of this book to analyze the code line by line, but you can get a feel for how it works by looking at the way the objects are set up.

```
OSStatus AUVolume::GetParameterInfo(AudioUnitScope
    inScope,
    AudioUnitParameterID    inParameterID,
    AudioUnitParameterInfo  &outParameterInfo)
{
    <SNIP SNIP SNIP>
    switch(inParameterID)
    {
    case kParam_One:
        AUBase::FillInParameterName (outParameterInfo, kParameterOneName,
        false);
        outParameterInfo.unit = kAudioUnitParameterUnit_LinearGain;
        outParameterInfo.minValue = 0.0;
        outParameterInfo.maxValue = 1;
        outParameterInfo.defaultValue = kDefaultValue_ParamOne;
        break;
    default:
        result = kAudioUnitErr_InvalidParameter;
        break;
    }
}
```

Here, when the Client queries the plug-in on its first parameter (kParam_One) it fills out a structure about the control. You can see the minimum, maximum, and default values being set. The “unit” variable of the structure is set to kAudioUnitParameterUnit_LinearGain. A linear gain control moves between 0 and 1.0. Another example is kAudioUnitParameterUnit_Boolean, which specifies a boolean control variable. What is interesting here is that you don’t declare the actual variable that stores the control data. The variable is a float variable that the framework stores for you. You tell the framework what kind of variable it represents. When you need to get or set the variable, you use GetParameter() and SetParameter(), which get and set a float data type.

# A.6.2 Signal Processing

The AU processing function is simply named Process(). The audio data moves in buffers. The buffers can contain any arbitrary number of channels with the simplest systems being N × N or equal input/outputs. Although the inNumChannels variable is passed to the function, it is always set to 1.0 for the current version of AU. This is OK for mono or when you don’t need to process channels independently. A boolean flag is passed to the method, indicating the mute condition and the function simply returns without processing. The parameters that are passed to the Process() method are as follows: