```
param = new RangeParameter(STRING("Octave"),
OCTAVE,
STRING("""),
MIN_OCTAVE,
MAX_OCTAVE,
DEFAULT_OCTAVE);
/* Ctrl Name */
/* index */
/* units */
/* LOW */
/* HIGH */
/* DEF */
// integer, no sig digits
param->setPrecision(0); // <--- this is an Integer (int)
// add to container
parameters.addParameter(param);
```

straightforward; we set the parameter to 0 which indicates an integer display—note the control will still transmit a raw value from 0.0 to 1.0. The log-scale parameter takes a bit more work to setup. Outside of the object methods the top of the .cpp file you define the scaling:

The first four parameters show the range mapping of the control from 0.0 to 1.0 will map from 80.0 to 18000.0 and the last two arguments show the center-anchor point—you could read these arguments as “when the raw value is 0.5 the control will display 1800”. The last two allow you to create quasi-logarithmic controls that have expanded or compressed or lower ranges.

```
// these are defined in SynthParamLimits.h
#define MIN_UNIPOLAR 0.0
#define MAX_UNIPOLAR 1.0
#define DEFAULT_UNIPOLAR 0.0
```

For the LogScaleParameter, you have to set the default value in a separate function, and you may only set the normalized (raw) value. To do this, use a helper method called toNormalized(), which converts the value for you. This is especially important here where the control is logarithmic and the mapping is not linear. In this case, we set the control to the default value, DEFAULT_FILTER_FC.

Lastly, we can use the StringListParameter to define the Filter Type control. First, you create the Parameter then you load the strings:

Notice that the string indexing—remember that in VST3 it is up to you reconcile the integer values (0,1,2...) with the strings (LPF,HPF,BPF...).

# 2.24 VST3 Controller Serialization

# Step Four: Implement the Serialization-ReadState() in the componentState() Method

For the Controller, the componentWillState() method is the serialization-read method. The Processor uses slightly different function names, which we will get shortly. In both objects, the argument that is passed to the function is an IBState pointer. This interface allows reading and writing to a binary file. We will be storing and loading your variables, which will be of the types listed above, like int and UINT. The IBState interface provides relatively easy methods for writing and reading values to and from it. In this case, we be reading values. The most important thing to remember with this code is that the order of variable reading and writing be