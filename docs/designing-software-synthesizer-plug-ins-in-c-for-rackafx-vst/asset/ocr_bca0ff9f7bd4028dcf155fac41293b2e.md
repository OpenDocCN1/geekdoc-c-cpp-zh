```
CWaveData(char* pFilePath = NULL);
```

If you pass a valid path through construction, it will be used to load and initialize the object all at once. If you pass a NULL pointer, the object created audio data array is not allocated.

```
bool initWithUserWAVEFile(char* pInitDir = NULL);
```

initWithUserWAVEFile() is only available in the Windows version. When you call this function, a Windows File dialog opens, and the user browse to find the .wav file; you can suggest an initial directory as the argument or leave it blank to the current directory. We won't use this function in our synth, but you might come up with an interesting way to use it.

Using this object could be simpler. Just construct it and pass the file path as the argument, then check the m_bWaveLoaded for success or failure.

Iterating through the audio buffer requires that you check the channel first; multi-channel files are interleaved.

```
// create the new object
m_pWaveSample = new CWaveData(pSamplePath);
```

# 10.6 CSampleOscillator Object

```
// did we find the sample?
if(m_pWaveSample->m_bWaveLoaded)
{
    // ERROR! FILE NOT LOADED
}
```

This oscillator is used in the next three seconds, so you need to understand it. Since it is derived from CSOscillator, it bears all the same functionality and function names for resetting, updating, rendering. The big difference, however, is in the way the object is initialized since it needs audio files to operate. This object was designed to operate in two modes: single-sample and multi-sample. In single-sample mode, you only one .wav file, which is played across the range of notes. This is useful for pitch-less samples like sounds and drums when you don't intend on shifting pitch, or loops that are likewise pitch-less. You will use multi-sample mode for DigiSynth and VectorSynth and single-sample mode for AniSynth.

The multi-sample sets we use and that you receive with the book projects were distributed royalty-free samples in a CD-ROM from Music Magazine Number 171 and created by Cyclic. These are all stereo samples with the correct MIDI Unity Note information. As a free distribution, the synth designers give you three octaves of samples on minor boundaries. These are all designed to work in a bass synth application. Future Music grants full rights for commercial or non-commercial use, providing the samples are not part of a sample library. If you like them, you might want to contact Cyclic and purchase the rest of the samples. In all by-sample books, the quality of the synthesis ideally depends on the quality of the samples. No amount of material or signal processing will fix poorly recorded looped samples. I urge you to find your suppliers and find the best sounding for the synth. Many and loop suppliers will give you free samples if you sign up for a newsletter. Also, check magazines like Future Music that delivers gigabytes of royalty free samples and loops every month.

CSampleOscillator is initialized with a single file path in single-sample mode or a folder path in multi-sample mode. When using a folder to initialize multi-samples, CSampleOscillator finds every .wav file and regardless of file name. CSampleOscillator stores its samples in two different manners corresponding to the modes.