```
class AUSynth : public AUInstrumentBase
{
public:
    <SNIP SNIP SNIP>

    // Add your code here: ---------------------- /

    << INSERT ** Code Listing 10.1: Declarations ** HERE >>

etc...
ASynth::AUSynth(AudioUnit inComponentInstance)
    : AUInstrumentBase(inComponentInstance, 0, 1)
{
    // --- create input, output ports, groups and parts
    CreateElements();

    // --- set default factory preset (as example)
    factoryPreset[OSC1_AMPLITUDE_DB] = 0.0;
    factoryPreset[OSC2_AMPLITUDE_DB] = 0.0;

<SNIP SNIP SNIP>

    // --- define number of params (controls)
    Globals()->UseIndexedParameters(NUMBER_OF_SYNTH_PARAMETERS);

    // --- initialize the controls here!
    // --- these are defined in SynthParamLimits.h
    //
    Globals()->SetParameter(OSC1_AMPLITUDE_DB, DEFAULT_OUTPUT_AMPLITUDE_DB);
```