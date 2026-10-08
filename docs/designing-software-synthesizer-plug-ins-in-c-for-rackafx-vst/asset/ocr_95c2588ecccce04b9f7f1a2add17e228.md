synth, these parameter index values are implemented with an enumeration found at the top of the SynthParamLimits. file:

```
enum {
    MIDI_PITCHBEND,
    MIDI_MODWHEEL,
    MIDI_VOLUME_CC7,
    MIDI_PAN_CC10,
    MIDI_EXPRESSION_CC11,
    MIDI_SUSTAIN_PEDAL,
    MIDI_CHANNEL_PRESSURE,
    MIDI_ALL_NOTES_OFF,

    NUMBER_OF_SYNTH_PARAMETERS // always last
}
```

Initializing the MIDI Parameters

The GUI parameters are always created and initialized in the Controller::Initialize() function. Initializing the Parameter objects involves linking them to the enumerated parameter indices, as well as establishing the min, max and default values. Our parameter values will get delivered to the Processor as a normalized value anyway, so the simplest thing is to set them up unipolar. The SynthParamLimits.h file has constant declarations for the min, max and default values of all parameters in all the synths and includes unipolar and bipolar limits as well. Open the VSynthController.cpp file and set the dummy variables (refer to Chapter 2 if you need to), use the indexes and limits in the SynthParamLimits file:

```
result PLUGIN_API Controller::initialize(FUnknown* context)
{
    // -- base class does its thing
    result = EditController::initialize(context);

    // -- now define the controls
    if(result == kResultTrue) {
        // -- Init parameters
        Parameter* param;

        // MIDI Params -- these have no knobs in custom GUI but do have to
        appear in default
        // NOTE: this is V3 ONLY! Not needed in AU or RAFX
        param = new RangeParameter(USTring("PitchBend"), MIDI_PITCHBEND.
```