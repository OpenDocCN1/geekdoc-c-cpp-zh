+   • IMidiMapping: MIDI mapping interface

+   • VST3EditorDelegate: handles the custom creation and interfacing for joystick and other more complicated controls

```
result PLUGIN_API initialize(FUnknown* context);
```

+   • setup the GUI controls, define min, max, defaults

+   • setup log control template

```
result PLUGIN_API setComponentState(IBStream* fileStream);
```

+   • serialize (read) to the GUI state for startup and preset loads

```
result PLUGIN_API setParamNormalizedFromFile(ParamID tag, ParamValue value);
```

+   • helper function for serialization (custom, not Steinberg)

```
virtual result PLUGIN_API setParamNormalized(ParamID tag, ParamValue value);
```

+   • set a normalized [0.+1] parameter

```
virtual ParamValue PLUGIN_API getParamNormalized(ParamID tag);
```

+   • get a normalized [0.+1] parameter

```
virtual IPluginView* PLUGIN_API createView(FString name);
```

+   • create the view object (GUI or custom GUI)

```
virtual result PLUGIN_API getMidControllerAssignment(int32 busIndex, int16 channel, CtrlNumber midiControllerNumber, aramID6 id*/**/);
```

+   • link MIDI controllers to underlying GUI controls

+   • The MIDI controller manager will be routed into the Processor object via the dummy variables we set up

```
IController* createSubController(UTF8StringPtr name, UIDescription* description, VST3Editor* editor) VSTGUI_OVERRIDE_VMTHOD;
```

+   • we will use this when we create the joystick controller in VectorSynth and AniSynth

```
static FUnknown* createInstance(void d*) {return (IEditController*)new Controller(d)};
```

+   • COM creation function

```
static FUID cid;
```

+   • the globally unique identifier for this value

When you implement the synths you get instructions on how to place various chunks of code into these files. The