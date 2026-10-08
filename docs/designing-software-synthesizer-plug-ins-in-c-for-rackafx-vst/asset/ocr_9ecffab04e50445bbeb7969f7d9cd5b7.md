![](bbox=[0.208, 0.031, 0.792, 0.403])

Figure 10.3: Transient and loop method of sustaining a sample indefinitely.

The CSampleOscillator is new for this chapter. It opens and loads the contents of .wav files into buffers. Then, it treats these buffers nearly the same as a wave table, reading and interpolating samples (with linear interpolation again). An increment value is used to update a read index that ultimately controls the pitch of the sample.

# 10.2 .wav Files

The .wav file format is very popular for delivering audio samples. It was designed to hold pertinent information that we need in order to play the samples at proper pitches. These .wav files are sometimes called “wave files.” In addition to the audio data itself, .wav files also encode the:

+   * manufacturer name
* product name
* sample period (1/fₛ)
* MIDI Unity Note
* MIDI Pitch Fraction
* SMPTE time code information
* loop points