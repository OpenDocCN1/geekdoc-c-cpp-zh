```
AUSynth::AUSynth(AudioUnit inComponentInstance)
    : AUInstrumentBase(inComponentInstance, 0, 1)
{
    // --- create input, output ports, groups and parts
    CreateElements();

    // --- setup default factory preset (as example)
    // <SNIP SNIP SNIP>

    factoryPreset[DELAY_TIME] = 125.0;
    factoryPreset[DELAY_FEEDBACK] = 20;
    factoryPreset[DELAY_RATIO] = 0.5;
    factoryPreset[DELAY_WET_MIX] = 0.5;
    factoryPreset[DELAY_MODE] = 3;

    // --- define number of params (controls)
    Globals()->UseIndexedParameters(NUMBER_OF_SYNTH_PARAMETERS);

    // <SNIP SNIP SNIP>

    // Delay FX stuff
    Globals()->SetParameter(DELAY_TIME, DEFAULT_DELAY_TIME);
    Globals()->SetParameter(DELAY_FEEDBACK, DEFAULT_DELAY_FEEDBACK);
    Globals()->SetParameter(DELAY_RATIO, DEFAULT_DELAY_RATIO);
    Globals()->SetParameter(DELAY_WET_MIX, DEFAULT_DELAY_WET_MIX);
    Globals()->SetParameter(DELAY_MODE, DEFAULT_DELAY_MODE);

    // Finish initializations here
    m_dLastNotefrequency = -1.0;

    etc...

    ComponentResult AUSynth::Reset(AudioUnitScope inScope,
    AudioUnitElement inElement)
```