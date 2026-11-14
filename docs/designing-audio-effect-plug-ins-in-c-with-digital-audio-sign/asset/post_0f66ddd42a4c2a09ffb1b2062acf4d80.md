
| Appendix B | sendUpdateGUI() | updateDisplay() | N/A |
|---|---|---|---|
| Get the DLL's Directory | getMyDLLDirectory() | getDirectory() | N/A |
| Show a Custom GUI | showGUI() | dispatcher() | AudioUnitGetProperty() |

RackAFX, VST, and AU all provide for a default standard interface—a GUI that the user does not have to code. For RackAFX, you can optionally design your own custom GUI with the GUI designer (Appendix B) that requires no coding; alternatively, you can design your own (see Section A.1). VST and AU also allow you to design your own GUI. VST provides a GUI class of objects that you can optionally use in your coding that allows for cross-platform compatibility. AU only runs on Mac and does not provide cross-platform compatibility. The default interface setup for RackAFX involves you simply filling in a properties dialog for the components you want; the GUI object code is written for you. In VST and AU, you must set up a way to describe your controls. In all three formats, when you load your plug-in the client queries it for its default interface controls and then builds the GUI at run time. In RackAFX, the client simply iterates through your linked list of objects and sets up the GUI.

## A.4 VST Plug-in without Wrapping

Let's start by pretending to write a VST plug-in from scratch without wrapping any RackAFX code—of course, you can always cut and paste processing or cooking functions directly from your source, since it is pure C++. The pretend plug-in will be a delay with feedback called CDelay.

### A.4.1 Default GUI

First, you define an enumerated list of unsigned integer-type (UINT) constant values in your PlugIn.h file where “PlugIn” is the name and you have derived it from the AudioEffectX base class. These constants are the control ID values the host will use when querying about, getting, or setting a control variable. A delay plug-in might have delay time, feedback, and wet/dry mix controls, so you might define your enum as follows:

```
enum
{
   uDelayTime,    /* ID = 0 */
   uFeedBack,     /* ID = 1 */
   uWetDry,       /* ID = 2 */
   uNumParams     /* Always last = 3 = number of controls */
};
```

Next, you declare a parallel set of member variables that will be used in your plug-in. These are for cooked data values.

```
float m_fDelayTime;
float m_fFeedBack;
float m_fWetDry;
```

Finally, you declare the minimum and maximum values for each control.

```
float m_fMinDelayTime, m_fMaxDelayTime;
float m_fMinFeedBack, m_fMaxFeedBack;
float m_fMinWetDry, m_fMaxWetDry;
```

The last item in the enumeration keeps track of the control count by virtue of being last in the list. During operation, the VST client will use these ID values passed as the variable “index” in the following methods. First, there are three methods to fill out that describe the name, display, and units for each control.

- 1. getParameterName: You create the name of the control as a string.

```
void CDelay::getParameterName (long index, char *label)
{
    switch (index)
    {
        case uDelayTime: strcpy (label, "Delay"); break;
        case uFeedBack: strcpy (label, "FeedBack"); break;
        case uWetDry: strcpy (label, "Wet/Dry"); break;
    }
}
```

> All default VST controls use values from 0.0 to 1.0 regardless of how they map in your actual plug-in. You must write the cooking and uncooking functions that will convert your internal variable values to and from values from 0.0 to 1.0.

- 2. getParameterDisplay: You create a string that represents the value to display on the UI; the float2String() method is a helper function that is provided in the VST object file.

```
void CDelay::getParameterDisplay (long index, char *text)
{
    switch (index)
    {
        case uDelayTime: float2string (m_fDelayTime, text); break;
        case uFeedBack: float2string (m_fFeedBack, text); break;
        case uWetDry: float2string (m_fWetDry, text); break;
    }
}
```

- 3. getParameterLabel: You create a string that represents the units for the control.

```
void CDelay::getParameterLabel (long index, char *label)
{
    switch (index)
    {
        case uDelayTime: strcpy (label, "mSec"); break;
        case uFeedBack: strcpy (label, "%"); break;
        case uWetDry: strcpy (label, "%"); break;
    }
}
```

Next, there are two methods you need to implement to allow the client to get and set your control variables. However, these methods deal with raw VST client data.

- 1. getParameter: You return the raw data (0–1) for the control.

```
float CDelay::getParameter (long index)
{
    float fRawData = 0;

    switch (index)
    {
    case uDelayTime:
    {
        float fDiff = m_fMaxDelayTime - m_fMinDelayTime;
        fRawData = (m_fDelayTime - m_fMinDelayTime)/fDiff;
        break;
    }

    // same thing for the other variables
    }

    return fRawData;
}
```

- 2. setParameter: You cook the raw data (0–1) for use in your plug-in.

```
void CDelay::setParameter (long index, float value)
{
    switch (index)
    {
    case uDelayTime:
    {
        m_fDelayTime = (m_fMaxDelayTime - m_fMinDelayTime) * value +
                      m_fMinDelayTime;
    }

    // same thing for the other variables
    }
}
```

Thus, every time you add or remove a variable, you have to update your enumerated list, change the variables and min/max pairs, and update the five functions above.

### A.4.2 Signal Processing

You will notice that you've already had to write a lot of code just to deal with the UI; you have not written any code to do any meaningful processing. In RackAFX, you alter three functions for signal processing:

- 1. Constructor
- 2. prepareForPlay()
- 3. processAudioFrame()

### Constructor

- Init all variables.
- Set our input and output channel count (this is also done in the CPlugIn constructor).
- Set a unique four-character identifier (required by VST).
- Call the base class's constructor to pass it the number of presets (0 for now) and number of controls.
- The audioMasterCallback you see is a mechanism for client plug-in communication; its details are hidden from developers.

```
CDelay::CDelay (audioMasterCallback audioMaster)
: AudioEffectX (audioMaster, 0, uNumParams) // 0 presets, uNumParams controls
{
	m_fDelayTime = 1000;
	m_fFeedback = 0;
	m_fWetDry = 50;

	// VST Specific setup
	// NumInputs (2);
	setNumInputs (2);
	setNumOutputs (2);
	setUniqueID ('WDly');
}
```

### prepareForPlay() → setSampleRate() and resume()

prepareForPlay() is special for RackAFX because it is called after the sample rate is set. In VST, this is done in setSampleRate(). We also use prepareForPlay() to flush out our delay line buffers and do any other preparations for the next run of the plug-in. The resume() function is called when the VST plug-in is turned on so we can flush buffers there.

```
void CDelay::setSampleRate(float sampleRate)
{
	// Left
	if(m_pLeftBuffer)
		delete m_pLeftBuffer;

	// Create a 2 second buffer
	m_pLeftBuffer = new float[2*(int) sampleRate];

	// Right
	if(m_pRightBuffer)
		delete m_pRightBuffer;

	// Create a 2 second buffer
	m_pRightBuffer = new float[2*(int) sampleRate];

	// flush buffers
	memset (m_pLeftBuffer, 0, 2*(int) sampleRate * sizeof (float));
	memset (m_pRightBuffer, 0, 2*(int) sampleRate * sizeof (float));
}
```

```
void CDelay::resume()
{
	// flush buffer
	memset (m_pLeftBuffer, 0, 2*(int) sampleRate * sizeof (float));
	memset (m_pRightBuffer, 0, 2*(int) sampleRate * sizeof (float));

	// reset read/write indices, etc...
	m_nReadIndex = 0;
	m_nWriteIndex = 0;

	etc...
}
```

### processAudioFrame() → processReplacing()

The fundamental difference in the processing functions is in how the data arrives. In RackAFX, the default mechanism is that it arrives in frames, where each frame is a sample from each channel. The frames arrive as pointers to buffers. In VST, the audio is processed in buffers of frames, rather than single frames. Figure A.3 shows a two-channel in and two-channel out VST setup.

![](img/b54974d0a4317ec82d7ae02126d10a6f_486_0.png)

Figure A.3: VST audio data is delivered in buffers of frames.

Instead of passing a pointer to a buffer, you pass a pointer to a buffer of pointers, or float** variables. The processReplacing() method also passes you a count of the number of frames. You use these variables to iterate through and access your audio data. VST was designed to allow you to have any number of input and output channels, which you specify in the constructor. The parameters that are passed to the processReplacing() method are as follows:

- float** inputs: A pointer to a buffer of pointers to input buffers
- float** outputs: A pointer to a buffer of pointers to output buffers
- Long sampleframes: The count of frames in each buffer

```
void CDelay::processReplacing(float **inputs, float **outputs, long sampleframes)
{
    // pick up pointers to buffers
    float *inL = inputs[0];
    float *inR = inputs[1];
    float *outL = outputs[0];
    float *outR = outputs[1];

    UINT uFrameCount = 0;

    while (--sampleframes > 0)
    {
        // pick up samples from buffers
        float fxnL = inL[uFrameCount];
        float fxnR = inR[uFrameCount];

        // calculate and write out
        outL[uFrameCount] = doLeftDelayFunction(fxnL);
        outR[uFrameCount] = doRightDelayFunction(fxnR);

        // inc frame counter
        uFrameCount++;
    }
}
```

You can now see the similarities and differences in RackAFX and VST:
