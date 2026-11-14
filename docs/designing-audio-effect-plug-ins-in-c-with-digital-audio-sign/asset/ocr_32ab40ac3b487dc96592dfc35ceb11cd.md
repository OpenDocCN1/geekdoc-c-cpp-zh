| Function | Description |
| :--- | :--- |
| **prepareForPlay()**<br>Parameters: • none | Function is called just before audio begins streaming. The audio file's sample rate, bit depth, and channel counts are extracted and then set by the client just before calling this method. |
| **processAudioFrame()**<br>Parameters<br>• pInputBuffer<br>• pOutputBuffer<br>• uNumInputChannels<br>• uNumOutputChannels | The most important function in the API; this is where the audio processing is handled. You might do all the processing in this function or use it to call sub-functions. You are responsible for writing the data to the output buffer via pOutputBuffer.<br>A pointer to one frame of audio input data. A frame is a set of channels as defined by uNumInputChannels.<br>A pointer to one frame of audio output data. A frame is a set of channels as defined by uNumOutputChannels.<br>The number of input channels in this frame of data. Currently, this value will be either 1 (mono) or 2 (stereo).<br>The number of output channels in this frame of data. Currently, this value will be either 1 (mono) or 2 (stereo). |
| **userInterfaceChange()**<br>Parameters:<br>• nControlIndex | Function is called after the user changes a control in the RackAFX UI. RackAFX will automatically update the variable linked to this control prior to calling this method.<br>The index of the control that was moved and whose value RackAFX has changed. |

# Bibliography

Apple Computers, Inc. 2011. The Audio Unit Programming Guide. https://developer.apple.com/library/mac/#documentation/MusicAudio/Conceptual/AudioUnitProgrammingGuide/Introduction/Introduction.html. Accessed August 7, 2012.
Bargen, B. and Donnelly, P. 1998. Inside DirectX, Chapter 1. Redmond, WA: Microsoft Press.
Coulter, D. 2000. Digital Audio Processing, Chapters 7–8. Lawrence, KS: R&D Books.
Petzold, C. 1999. Programming Windows, Chapter 21. Redmond, WA: Microsoft Press.
Richter, J. 1995. Advanced Windows, Chapters 2 and 11. Redmond, WA: Microsoft Press.
Rosenberg, D. 1997. Inside COM, Chapters 1–2. Redmond, WA: Microsoft Press.
Steinberg.net. The Steinberg VST API. http://www.steinberg.net/en/company/developer/sdk_download_portal.html. (Note: you must create a free developer's account to download the API.) Accessed August 7, 2012.