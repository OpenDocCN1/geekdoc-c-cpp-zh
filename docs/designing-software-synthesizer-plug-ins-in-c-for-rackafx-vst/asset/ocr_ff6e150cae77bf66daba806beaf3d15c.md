+   - minimum control value
- maximum control value
- default control value
- if your control is an indexed list of strings (as in Filter Type from Table 2.9)

When you are working on a synth project from this book, use the GUI control table to help with the set up—it contains all this information (remember you can ignore the variable declarations).

After AU loops through your parameter setup, for each parameter you declared as an list of strings in GetParameterInfo(), the framework will call GetParameterValueStrings(), passing the zero-based index of the string-parameter list. You decode this value and pass back a string of substrings separated by commas, for example "LFF,HPF,BPF" from Table 2.9. When you declared that your parameter was indexed, you set a minimum (0), (maximum string-count) and default value. If your string count does not match the number of substrings in the comma-separated string, you will get a validation error. So, you need to be careful with parameter setup.

# Functions to Handle Presets and Saved States:

Fortunately, presets are fairly to deal with in AU and RackAFX, unlike VST3 where you must serialize yourself. The ones you need to implement are:

```
virtual ComponentResult
GetPresets()

virtual OSStatus
NewFactoryPresetSet()
```

```
OSStatus
RestoreState()
```

The AU framework will query your plug-in for a list of names of presets you have compiled into the instrument by calling GetPresets(). You pass it an array of strings that are your preset names. It is OK if you have no presets; our synths have one preset as an example, and you are urged to do more of your own.

The framework calls NewFactoryPreset() when the user recalls one of your factory presets. It gives you a zero-based index value for the preset and you respond by decoding the value and updating your synth parameters using the preset values. One of handling presets is with a simple array that is the same length as the number of parameters in your cloud. This is declared in the .h file:

```
double
factoryPreset[NUMBER_OF_SYNTH_PARAMETERS]
```

The array is declared as a double because all of our non-integer synth parameters are doubles. You could also declare this as a float or Float32 array.

RestoreState() is an optional function that called to restore the plug-ins internal state. If you need to do processing after a preset is loaded, you can implement that here. None of the book projects uses this function, you simply forward it to the base class.

# Functions to Declare GUI and MIDI Capabilities

The AU will query your plug-in at start-up to find out if it has capabilities beyond the stock Audio Unit. There are three functions that are implemented: