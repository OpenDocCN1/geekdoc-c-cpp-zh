Modulating the pitch of an oscillator is a commonly used synthesis technique. Sounds feature both time and frequency domain evolution, and modulating pitch is a fundamental component of frequency domain evolution. Musicians use the vibrato effect to modulate the pitch of instruments or voices. Modulating the pitch of an oscillator with a LFO produces the vibrato. Most synths also contain a dedicated pitch-bend control in the form of a wheel or joystick. The control resets when released and sends bend message when moving. An envelope generator (EG) is often used to modulate the pitch over the note event. For LFO and EG pitch-bend, the pitch modulation is exponential and expressed in cents.

```
double k = 1.059463094359; // 12th root of 2
double a = 6.875; // a
a *= k; // b
a *= k; // bb
a *= k; // c, frequency of midi note 0
for (int i = 0; i < 128; i++) // 128 midi notes

// Hz Table
midifreqTable[i] = (float)a;

// update loop...
a *= k;

/* pitchShiftMultiplier()
```

you apply vibrato with a depth of one octave to the note 440 Hz, then the upper extreme would be 880 Hz while the lower would be 220 Hz—this is not linearly centered around 440 Hz. However, with FM synthesis, the modulation is linear around the oscillator pitch. This means that we have more pitch multipliers to implement. For our oscillators, we will need three pitch inputs:

returns a multiplier for a given pitch shift in semitones
to shift octaves, call pitchShiftMultiplier(octaveValue*12.0);
to shift semitones, call pitchShiftMultiplier(semitonesValue);
to shift cents, call pitchShiftMultiplier(centsValue/100.0);

```
*
// 2^(N/12)
return pow2(dPitchShiftSemitones/12.0);
```

double octave = pitchShiftMultiplier(2.0*12.0);
double semi = pitchShiftMultiplier(-7.0);
double cents = pitchShiftMultiplier(50.0/100.0);

```
// put it all together
double final15scFreq = m_dFrequencyHz*octave*semi*cents;
```

+   - pitch bend
- exponential modulation
- linear modulation

![](bbox=[0.635, 0.485, 0.915, 0.535])