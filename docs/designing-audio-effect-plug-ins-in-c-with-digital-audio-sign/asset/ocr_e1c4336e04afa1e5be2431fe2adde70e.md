as a reminder of how to get the audio data samples into and out of the I/O buffers. Currently, RackAFX only supports mono and stereo plug-ins. The left and right channels are accessed using the normal array-indexed C++ pointer mechanism. Of special note is the reminder that all values in and out are (and should be) between -1.0 and +1.0.

```
/* processAudioFrame
// ALL VALUES IN AND OUT ON THE RANGE OF -1.0 TO +1.0
LEFT INPUT - pinpBuffer[0];
RIGHT INPUT - pinpBuffer[1];
LEFT OUTPUT - pinpBuffer[0]
LEFT OUTPUT - pOutputBuffer[1]
*/
bool __stdcall CVolume::processAudioFrame(float* pinpBuffer, float* pOutputBuffer,
UINT uNumInputChannels, UINT uNumOutputChannels)
(
    // output = input -- change this for meaningful processing
    //
    // Do LEFT (MONO) Channel; there is always at least one input/one output
    (INSERT Effect)
    pOutputBuffer[0] = pinpBuffer[0];
    // Mono-In, Stereo-Out (AUX Effect)
    if(uNumInputChannels == 1 && uNumOutputChannels == 2)
    pOutputBuffer[1] = pInputBuffer[0];
    // Stereo-In, Stereo-Out (INSERT Effect)
    if(uNumInputChannels == 2 && uNumOutputChannels == 2)
    pOutputBuffer[1] = pInputBuffer[1];
    return true;
)
```

Take a look at the function as RackAFX wrote it for you—it is designed to pass audio through unmodified. In this case, you simply write the output buffer with the data from the input buffer. In your processAudioFrame() function, get used to always processing the first channel then optionally processing the second one. This makes it easy to write mono/stereo capable plug-ins and will also make it easier to extend when RackAFX has more channel options. Because the code is already done, you could compile it right now and try it in RackAFX as a sanity check to make sure your audio hardware is set up properly. In fact, we'll do that right after examining the last few functions in the file (I promise you will write code shortly).

# userInterfaceChange()

Perhaps the second most important function is userInterfaceChange(), which is called when the user changes a control on the control surface: