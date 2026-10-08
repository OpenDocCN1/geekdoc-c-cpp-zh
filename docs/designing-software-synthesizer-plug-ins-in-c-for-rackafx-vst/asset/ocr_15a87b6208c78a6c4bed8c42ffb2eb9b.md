# Single-Sample Mode

In this mode, the .wav file is opened and its contents are stored in the member variable:

```
CWaveData*
m_pWaveSample;
```

You access its internal buffer by simply:

```
m_pWaveSample->m_pWaveBuffer
```

Since this variable is a pointer, it is possible for multiple CSampleOscillators to share the same CWaveData object.

# Multi-Sample Mode

In this mode, a set of CWaveData objects are constructed and pointers to each are stored in an array capable of holding 128 pointers:

```
CWaveData*
m_WaveSamplePtrArray[128];
```

The array index correspond to MIDI note numbers, so you can theoretically populate the array with 128 samples taken on semitone boundaries. When playing back, the index value is used to extract the proper samples. Most likely you'll have it and replicate pointers in groups based on the idea in Figure 10.8. The samples we use are sampled on minor third boundaries C, Eb, F# and A. For example, MIDI CWaveData pointer for the middle C file in slots 60, 59 and 58 corresponding to C, Bb and B. This is shown in Figure 10.8, which depicts a piece of the array. The index of the CWaveData object pointer in the array. Like the single sample operation, you can set up multiple CSampleOscillators to share a common array of wave objects via a pointer-to-pointer. We will use this option in VectorSynth and AniSynth. The first and very last wave object pointers are copied into the extremes of the array; if the lowest note is 32, it will be used for all notes below it, down to MIDI note 0, while the highest note pointer will be used for all notes above it, to MIDI note 127.

Table 10.2 lists the CSampleOscillator member variables, and Table 10.3 lists the member functions and descriptions.