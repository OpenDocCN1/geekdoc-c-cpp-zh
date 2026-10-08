
or resource-limited device. Another possibility is to set a set of tables for each octave from A0 to C8, or for all
octaves from 20 Hz to 20480 Hz. Another is a set of tables for each third interval near A0 to C8 would produce a smooth transition, as the notes are played through the intervals whereas-octave-table might produce an audible change in timbre as the octave boundary is crossed.

Figure 5.34 (a) is the spectrum of a bandlimited sawtooth wave at 440 Hz containing the fundamental plus
harmonics, while Figure 5.34 (b) shows the waveform of a 150 Hz sawtooth using the same method. The ripples are
seen as exaggerated because the table lacks the upper harmonics; a 150 bandlimited sawtooth should contain 147
harmonics. Adding more harmonics will smooth out the ripples. Multiplying each harmonic by the Lanczos sigma factor
further smooth the ripples, but this is sometimes ignored for oscillators where a perfect frequency
demand is more desirable than a time domain. The Lanczos sigma factor:

Pulse width modulation of a square
wave presents a problem in wave
synthesis of the square wave
with pulse. An option might be to
pre-calculate several tables of
various pulse width and interpolate them. A simpler option is to use the sum-of-saws method for Section 5.12.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_275_0.png)

Figure 5.35 shows the difference in the waveform shape with and without applying the Lanczos sigma factor.
The spectrum of the Lanczos sawtooth method is not as smooth as the unsmo one; however, in the case of
sawtooth, we can apply it so that the waves we generate with the sum-of-saws method will have its
pulses modulated, which is more dependent on the shape of the waveform than its spectrum.

You should also know that the Lanczos sigma correction also affects the bit-limit in both the waveform and
spectrum results with the eight-point BLEP oscillator using non-rectangular windowing. Figure 5.36
shows the spectrum of a 440 Hz sawtooth with and without the sigma correction. Compare these with the BLEP oscillator
spectrum including the waves sawtooth. You should also do listening tests to see if you can hear a difference in
the normal and corrected versions.

The code implements a wavetable lookup using a read index and index value.

- the two samples surround the target index value are found
- the output is interpolated between them
- the read index is increased by the inc value

Figure 5.34: (a) The spectrum of a 440
sawtooth wave using a bandlimited
wavetable and (b) the waveform
shape of a 150 Hz sawtooth using the
same as (a).

![](img/b42d0dca53f4a889d8162d55f7c8c05d_275_1.png)

Figure 5.35: A 150 Hz
sawtooth (a) with and without (b)
Lanczos sigma correction.

Figure 5.36: Spectra for the 440 Hz
wavetable without Lanczos sigma
correction (b) 440 Hz wavetable with
sigma correction.

- check for, both forward and
reverse (for negative frequencies
in FM/PM)
- bound the read index to the table boundaries (FM/PM)
- m_currentTable is a pointer to the table used

![](img/b42d0dca53f4a889d8162d55f7c8c05d_275_2.png)

With the Fourier equations, we can create limited triangle and square waves. The triangle waves work perfectly.

However, the square waves are static and cannot have their pulse width changed. A solution is to use the sum-of-methods method used in the BLEP wave oscillator. The same block diagram arrays are discussed later, but you should compare the wavetable versions with the BLEP oscillators as shown in 5.37. Once again, aliasing is improved by using transition regions in the BLEP correction.

# 5.22

```cpp
double dWavetable(double& dReadIndex, double dWT_inc)
double dOut = 0;

// get INT part
int nReadIndex = abs((int)dReadIndex);

// get FRAC part
float frac = dReadIndex - nReadIndex;

// setup second index for interpolation
int nReadIndexNext = nReadIndex + 1 > WT_LENGTH-1 ? 0 : nReadIndex + 1;

// interpolate the output
dOut = dInterp(0, 1, m_pCurrentTable[nReadIndex], m_pCurrentTable[nReadIndexNext], frac);

// add the increment for next time
dReadIndex += dWT_inc;

// check for wrap
if(dWT_inc > 0) // forward
{
    if(dReadIndex > WT_LENGTH)
        dReadIndex = dReadIndex - WT_LENGTH;
}
else
{
    if(dReadIndex < 0) // reverse
        dReadIndex = WT_LENGTH + dReadIndex;
}

// clamp the index to table bounds for FM
dReadIndex = min(dReadIndex, WT_LENGTH);
```

![](img/b42d0dca53f4a889d8162d55f7c8c05d_276_0.png)

# 5.23 Sinusoidal Oscillators by Approximation

Wavetables with linear interpolation can produce very clean waveforms. The fundamental frequency of the oscillator comes from