Here use the constructor and destructor, which we use to initialize variables and destroy objects.

```
AUSynth (AudioUnit
inComponentInstance);

virtual
~AUSynth();
```

+   - the constructor's argument is the instance of an Audio Unit
- you will allocate memory in the constructor and destroy these objects in the destructor
- you will declare the parameters for the first time here

```
virtual OSStatus
Initialize();
```

+   - this is where you declare your user interface and initialize our synth object
- you also initialize your base class by calling its initialize function

```
virtual void Cleanup();
```

+   - called after user has unloaded the plug-in before the destructor

```
virtual OSStatus
Reset();
```

+   - similar to prepareForPlay() in RACKFS, when the plug-in is first opened and again if the user makes changes to the project's global settings, such as sample rate or bit depth

# Audio Rendering:

```
virtual OSStatus Render(AudioUnitRenderActionFlags& ioFlags, const AudioTime& inTimeStamp, UInt32 inNumberFrames);
```

You can ignore the flags and time stamp for now. In inNumberFrames argument is the number of audio frames to process, where a frame represents a single sample for mono and a left/right pair for stereo. Since our left and right channels each have their owners, inNumberFrames represents the length of these buffers.

# Functions to Declare User Controls:

In the constructor we will declare the interface controls by first defining the number of controls, then calling SetParameter() once for each control to set the initial value, but the parameter is not yet completely initialized. This happens in another pair of functions:

```
virtual OSStatus
GetParameterInfo();
```

```
virtual OSStatus
GetParameterStrings();
```

For each parameter we declare in the constructor, the AU framework will subsequently call GetParameterInfo() and pass the index of the parameter in construction. This happens in a loop after construction occurs. In GetParameterInfo() you decode the index and set the control by declaring:

+   - control name
- control units