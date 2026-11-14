```
/*
RackAFX(TM) Rapid Plug-In Development (RapiD) Client
Applications Programming Interface
Base Class Object Definition
Copyright(C) Will Pirkle 2002-2012
In order to write a RackAFX Plug-In, you need to create a C++ object that is
derived from the CPlugIn base class. Your Plug-In must implement the
constructor, destructor and virtual Plug-In API Functions below.
*/
```

```
// RackAFX abstract base class for DSP Filters
class CPlugIn
{
public:
    // Plug-In API Member Methods:
    // The following 5 methods must be implemeted for a meaningful Plug-In
    // 1. One Time Initialization
    CPlugIn();
    // 2. One Time Destruction
    virtual ~CPlugIn(void);
    // 3. The Prepare For Play Function is called just before audio streams
    virtual bool __stdcall prepareForPlay();
    // 4. processAudioFrame() processes an audio input to create an audio
    // output
    virtual bool __stdcall processAudioFrame(float* pInputBuffer,
                                             float* pOutputBuffer,
                                             UINT uNumInputChannels,
                                             UINT uNumOutputChannels);
    // 5. userInterfaceChange() occurs when the user moves a control.
    virtual bool __stdcall userInterfaceChange(int nControlIndex);
};
```

The five functions in Table 2.2 are the core RackAFX API—implement them and you have a legitimate RackAFX plug-in. Best of all, the RackAFX plug-in designer will write and provide default implementations of all these functions for you. You need only to go in and alter them to change your plug-in's behavior. See Appendix A for a comparison of the RackAFX API and other commercially available formats as well as notes on using RackAFX plug-in objects inside API wrappers for other formats.

# Table 2.2: The RackAFX API core functions.

| RackAFX Function | Remarks |
|---|---|
| CPlugIn () Parameters: • none | The constructor for the plug-in object, this function is the one-time initialization function. |
| ~CPlugIn () Parameters: • none | The destructor for the plug-in. |