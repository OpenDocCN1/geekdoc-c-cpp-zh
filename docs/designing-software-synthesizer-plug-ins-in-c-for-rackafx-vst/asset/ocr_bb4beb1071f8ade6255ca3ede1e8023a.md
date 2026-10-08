# Processor::Processor()

```
<SNIP SNIP SNIP>

m_dFilterKeyTrackIntensity = DEFAULT_FILTER_KEYTRACK_INTENSITY;
m_dDEGI0scIntensity = DEFAULT_BIPOLAR;

// --- initialize intensities
m_dDefaultModIntensity = 1.0;
m_dDefaultModRange = 1.0;
m_dOscFoModRange = OSC_FO_MOD_RANGE;
m_dFilterModRange = FILTER_FC_MOD_RANGE;

// VSTMIDID specific
m_dDMIDIPitchBend = DEFAULT_MIDI_PITCHBEND; // -1 to +1
```

etc...

```
tresult PLUGIN_API Processor::setActive(TBool state)
{
if(state)
{
  <SNIP SNIP SNIP>

  // clear
m_dlastNoteFrequency = 0.0;

  // -- create the Mod Matrix Rows
  << INSERT ** Code Listing 8.1: Mod Matrix Routings I ** HERE >>
  // -- set the source and destination indexes on the components
  << INSERT ** Code Listing 8.2: Mod Matrix Connections I ** HERE >>
}
```

etc...

# Sustain Pedal

The MIDI sustain pedal directly affects the EG object; when the sustain pedal is held, the EG stays in the sustain