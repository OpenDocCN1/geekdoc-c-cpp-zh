In this case, we rename the secondary output that optionally passed as an argument. It is now called pAuxOutput and will be used for stereo inline double doSawtooth(double dModule, double dinc) oscillators. The

```
double dTrivialSaw = 0.0;
doubleOut = 0.0;
```

```
if (m_uWaveform == SAW1) { // SAW1 = normal sawtooth (ramp)
    dTrivialSaw = unipolarToBipolar(dModule);
}
else if (m_uWaveform == SAW2) { // SAW2 = one sided wave shaper
    dTrivialSaw = 2.0*(tanh(1.5*dModule)/tanh(1.5)) - 1.0;
}else if (m_uWaveform == SAW3) { // SAW3 = double sided wave shaper
    dTrivialSaw = unipolarToBipolar(dModule);
    dTrivialSaw = tanh(1.5*dTrivialSaw)/tanh(1.5);
}
```

```
// // fs/8 = Nyquist/4; uncomment to use 8-point BLEP
// // fs/8 = Nyquist/4; uncomment to use 8-point BLEP
if (m_dFo <= m_dSampleRate+doPLE_N&dBLETABLE_8_BLKHAR[0], 4096,
    dOut = dTrivialSaw + doPLE_N&dBLETABLE_8_BLKHAR[0], 4096,
    dModule, fabs(dinc), 1.0, false,
    4, false);
else if // 2-point BLEP correction
ndOut = dTrivialSaw + doPLE_N&dBLETABLE_4096,
    dModule, fabs(dinc), 1.0, false,
    1, false);

// --- or uncomment this to use PolyBLEP correction
dOut = dTrivialSaw + doPolyBLEP_2(dModule);
    abs(dinc); // *abs(dinc) for negative frequencies /
    1.0, // *sawtooth edge = 1.0 *
    false); // *falling edge */

return dOut;
```

CQBLimitedOscators are all monophonic, so we simply copy the normal output into this aux variable if needed. Refer back to the doOscillator(), as of the general outline is the same (for example, starting with checking the note on flag).

# 5.33 The CWTOOscillator

The waveform oscillator is different from the others. It will feature one sine wave and a sawtooth and triangle of varying harmonics. For non-sinusoidal, there is one table octave with the lowest note on the piano, AO (27.5 Hz), and going up through nine octaves. In the tenth octave, there is only one harmonic before Nyquist, so is equivalent to a simple sine. We can use the sine for that octave. The sawtooth and triangle are created dynamically depending on the sampleRate, so they must be re-created if the sample rate changes; this necessitates setting the sampleRate() virtual function. A pointer to each is stored in a n-slot array of