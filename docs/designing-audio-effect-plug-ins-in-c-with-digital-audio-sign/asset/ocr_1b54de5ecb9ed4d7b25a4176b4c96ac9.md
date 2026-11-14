+   - const Float32: *inSourceP (a pointer to an input buffer)
+   - Float32: *inDestP (a pointer to the output buffer)
+   - UInt32: InSamplesToProcess (number of samples in the input buffer)
+   - UInt32: inNumChannels (number of channels to process)
+   - bool: &ioSilence (indicates no processing, if true)

Here is the AU process function for a volume plug-in.

```
void AURVolume::AUVolumeKernel::Process(const Float32		*inSourceP,
								Float32		*inDestP,
								UInt32	inFramesToProcess,
								UInt32	inNumChannels,
								bool		&ioSilence)
{
	// setup counter
	UInt32 nSampleFrames = inFramesToProcess;

	// setup pointers to I/O
	const Float32 *sourceP = inSourceP;
	Float32 *destP = inDestP;

	// use our own Get method
	Float32 gain = GetParameter( kParam_One );

	while (nSampleFrames-- > 0) {
		Float32 inputSample = *sourceP;

		sourceP += inNumChannels;

		// here's where you do your DSP work
		Float32 outputSample = inputSample * gain;

		*destP = outputSample;
		destP += inNumChannels;
	}
}
```

If you need to process multi-channel audio data independently, then you need to remove the Process() method override and replace it by overriding ProcessBufferLists().

```
ProcessBufferLists(AudioUnitRenderActionFlags &ioActionFlags,
const AudioBufferList &inBuffer,
AudioBufferList &outBuffer,
UInt32 inFramesToProcess)
```

This method passes data back and forth by using AudioBufferList objects. These objects contain pointers so buffers of interleaved data along with a variable that tells you how many channels the buffer holds. For example, for the input buffer:

```
inBuffer.mNumberBuffers = the number of channels in this Buffer List
inBuffer.mBuffers[0].mData = a float* to the buffer for channel 0
inBuffer.mBuffers[1].mData = a float* to the buffer for channel 1, etc...
```

You would typically write something like this to extract them (in this case, we know the channel count is 2):