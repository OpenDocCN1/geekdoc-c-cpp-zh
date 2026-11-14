
- const Float32: *inSourceP (a pointer to an input buffer)
- Float32: *inDestP (a pointer to the output buffer)
- UInt32: InSamplesToProcess (number of samples in the input buffer)
- UInt32: inNumChannels (number of channels to process)
- bool: &ioSilence (indicates no processing, if true)

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

```
// create the mini-frame arrays
float **inputs = new float*[2 * sizeof(float*)];
inputs[0] = (float*)inBuffer.mBuffers[0].mData;
inputs[1] = (float*)inBuffer.mBuffers[1].mData;

float **outputs = new float*[2 * sizeof(float*)];
outputs[0] = (float*)outBuffer.mBuffers[0].mData;
outputs[1] = (float*)outBuffer.mBuffers[1].mData;

// call your processing function
doProcess(inputs, outputs, inFramesToProcess);
```

In this case, your processing function is just like the VST processReplacing()—it is taking pointers to buffer pointers as arguments, then it would split out the data as in the VST version above. Lastly, the AUKernelBase method Reset() is implemented to reset your plug-in to its just-instantiated state.

## More RackAFX Controls and GUI Designer

RackAFX has several optional graphical user interface (GUI) controls that were not covered in the book chapters. It also has a GUI designer that lets you convert your slider-based default GUI into a fully customized version. The website www.willpirkle.com is always the best way to get the latest information on the GUI designer and any additional controls that may be added at a later date. The two additional GUI controls are the alpha wheel and liquid crystal display (LCD) and the vector joystick control.

### B.1 The Alpha Wheel and LCD Control

In the upper right of the main RackAFX UI is a control that represents an alpha wheel, LCD matrix view, and the control knob. During the course of designing your project, you've noticed that the LCD is used to give you feedback about the state of your project and compiler. However, it can also be used as a GUI control just like the other sliders. The LCD control allows you to store up to 1024 continuous slider controls inside it. Anything you can set up with a normal slider control will work as one of the LCD embedded controls. And, the GUI designer lets you place one of these controls on your own GUI. There are several uses for the control:

- It's a different way to store the continuous controls.
- If you run out of sliders, you can always put 1024 more of them in the LCD.
- You can use the enumerated list variable to create a set of presets or other global functions or configuration controls.

To set up the LCD control, right-click on it when you are in development mode (not with a plug-in loaded). A box pops up as shown in Figure B.1. Click on New to open the very familiar slider properties dialog. Fill it out just as you would any other slider control. After adding a few more controls, you might have something resembling Figure B.2, with three controls embedded. You can edit the controls, remove them, or move them up and down the list (which changes their sequence in the LCD control).

You treat these embedded slider controls just as any other slider, so there's nothing to add to your normal operational code. When you run your plug-in, use the alpha wheel to select one of the controls and the value knob to adjust its value. Note there is currently no edit control connected to the LCD for manual entry of control values. Figure B.3 shows the LCD control with the alpha wheel adjusted for the bass control.

![](img/b54974d0a4317ec82d7ae02126d10a6f_494_0.png)

Figure B.1: The New button pops up the slider properties to add a control to the LCD.

![](img/b54974d0a4317ec82d7ae02126d10a6f_494_1.png)

Figure B.2: The LCD is loaded with three controls.

An alternative way to use the LCD control is for global operations (like effects configurations) or to store presets, either because you need more than RackAFX provides or you need to write your own methods for loading and storing data. You can use the enumerated list variable to create up to 256 individual string names. You can also take advantage of a feature of the LCD control: You can use the underscore (_) to separate strings in your list (you can't have spaces in an enumerated name). When the LCD control uses them, it replaces the underscores with single white spaces. This allows you much more flexibility than the radio buttons or normal sliders provide. For example, you could set up a preset list with names like “Heavy_Lead,” “Liquid_Pad,” “Lush_Space,” and so on. Then, you can use the up/down arrows to place your “presets” control at the top of the control list. Now, as shown in Figure B.4, the user can select one of your custom presets (remember, it’s up to you to code your own preset format) and then scroll to adjust the other controls. The underscores have been replaced with spaces.

![](img/b54974d0a4317ec82d7ae02126d10a6f_495_0.png)

Figure B.3: The alpha wheel and LCD control is reminiscent of vintage synthesizer and rack effects.

![](img/b54974d0a4317ec82d7ae02126d10a6f_495_1.png)

Figure B.4: The underscores are automatically removed from enumerated list variables in the LCD control.

### B.2 The Vector Joystick Control

RackAFX also has a dedicated vector joystick control that communicates with your plug-in. Dave Smith designed the first vector synthesizers for Sequential Circuits, Inc. and then later for Yamaha and Korg. The vector joystick is a combination of a traditional x/y track-pad and an exponential joystick. The calculation documentation is available on the website. In the original synthesizers, the vector joystick was used to program or alter in real time the mixture of two or four different waveforms. The position of the joystick determines the mix ratios, which are not linear but rather exponential. In RackAFX, you can use the joystick to alter up to four different parameters at once, exponentially. In addition, a linear x/y value of the joystick location is available for your plug-in. Figure B.5 shows the vector joystick and components.

![](img/b54974d0a4317ec82d7ae02126d10a6f_495_2.png)

Figure B.5: The RackAFX vector joystick.

The joystick is arranged in a diagonal with four corners labeled A, B, C, D, clockwise; this is in keeping with Dave Smith's original lingo. As the joystick moves around, a new set of mix ratios is generated and appears in the mix blurb. The mix ratios will always add up to 1.0. In the center, the
