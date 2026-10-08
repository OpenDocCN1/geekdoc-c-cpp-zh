
![](img/b42d0dca53f4a889d8162d55f7c8c05d_679_0.png)
Figure 10.6: Each rounded box represents a single sample that covers a pitch range of one octave and a velocity range determined by the height.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_679_1.png)
Figure 10.7: Four regions; regions 2 and 4 are shaded for easier viewing.

## 10.5 The CWaveData Object

Let's have a look at the CWaveData object. Remember that its job is to crack open a .wav file and extract the audio into a floating point buffer. The object can handle files with any number of channels, though it is up to you to decode the interleaved samples. For interleaved files, the channels are coded L,R,L,R,L,R etc. CWaveData can open and read the following .wav file types on both Windows and MacOS:

- 16-bit signed integer
- 24-bit signed integer packed in three or four bytes
- 32-bit signed integer
- 32-bit floating point
- 64-bit double floating point

It does not read 8-bit files (though you could that fairly easily), and will only read PCM or uncompressed files. The industry standard for sample files is 24-bit integer for a while, though that may change. The files for the synth are all 24-bit. Initialize the CWaveData object with a string that is for the .wav file. It opens the file and extracts the audio into a newly created floating point buffer. Once successful, you can access its member variables to get information about the sample, as its MIDI Unit Note, MIDI Pitch Fraction, length, channel count, and so on. The object can be re-used to open multiple files, but the buffers will be destroyed and recreated with the new contents. We are going to use one .wav file in the oscillator. If you are a seasoned RackFX user, this object has been there all along, albeit undocumented. Table 10.1 shows the CWaveData member variables.

### SMPTE Format

- 0 no SMPTE offset
- 24 24 frames per second
- 25 25 frames per second
- 29 30 frames per second with frame dropping (30 drop)
- 30 30 frames per second

### SMPTE Offset

Table 10.1: CWaveData's member variables give you all the information you need about the .wav file.

| Type | Variable Name | Description |
|---|---|---|
| float* | m_pWaveBuffer | the buffer of audio extracted from the .wav file |
| bool | m_bWaveLoaded | true if the object successfully opened and parsed the audio data |
| HANDLE | m_file | handle to the file (Windows only)—you can safely ignore it |
| UINT | m_uNumChannels | channel count |
| UINT | m_usampleRate | sample rate of file |
| UINT | m_usampleCount | total of samples in file |
| UINT | m_uLoopCount | number of loops in file |
| UINT | m_uLoopStartIndex | start index of first loop |
| UINT | m_uLoopEndIndex | end index of first loop |
| UINT | m_uLoopType | Value Loop Type |
| | 0 | Loop forward (normal) |
| | 1 | Alternating loop (backforth) |
| | 2 | Loop backward (reverse) |
| | 3-31 | Manufacturer Specific |
| UINT | m_uMIDINote | MIDI Unit Note number |
| UINT | m_uPitchFraction | MIDI pitch fraction |
| UINT | m_uSMPTEFormat | SMPTE format |
| UINT | m_uSMPTEOffset | SMPTE Offset |

The SMPTE Offset value specifies the time used for the synchronization/calibration to the first sample in the waveform. This value uses a format of 0hhhhmmssff where hh is a signed value that specifies the number of hours (-23 to 23), mm is an unsigned value that specifies the number of minutes (0 to 59), ss is an unsigned value that specifies the number of seconds (0 to 59) and ff is an unsigned value that specifies the number of frames (0 to 79).

The CWaveData object only has two member functions and both involve the extraction of audio data. The Constructor is:

```cpp
CWaveData(char* pFilePath = NULL);
```

If you pass a valid path through construction, it will be used to load and initialize the object all at once. If you pass a NULL pointer, the object created audio data array is not allocated.

```cpp
bool initWithUserWAVEFile(char* pInitDir = NULL);
```

initWithUserWAVEFile() is only available in the Windows version. When you call this function, a Windows File dialog opens, and the user browse to find the .wav file; you can suggest an initial directory as the argument or leave it blank to the current directory. We won't use this function in our synth, but you might come up with an interesting way to use it.

Using this object could be simpler. Just construct it and pass the file path as the argument, then check the m_bWaveLoaded for success or failure.

Iterating through the audio buffer requires that you check the...
