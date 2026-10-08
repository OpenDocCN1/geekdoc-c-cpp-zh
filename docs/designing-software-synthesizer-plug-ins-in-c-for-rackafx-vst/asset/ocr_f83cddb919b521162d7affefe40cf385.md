![](bbox=[0.185, 0.038, 0.814, 0.313])

Figure 13.11: The new and improved MiniSynth + FX.

Using the StereoDelay object is refreshing. Of course for interfacing, but after that there are only a few functions called for operation. This delay object is not a member of voice—as master effect, it lies outside the stack of voices. For ease of implementation, we are going to make the delay object member of the plug-in object. The plug-in object will form the current sample output then it processes through the delay plug-in before writing to its output locations. Remember that this happens on a per-sample basis and not a per-voice-radius basis. Figure 13.11 shows the MiniSynth with the delay added after the DCA. We are not adding the modulation routines but if desired a Chapter Challenge. Remember the plug-in shares its modulation core with the voices and that it receives the MIDI control inputs, so we can add them to the FX section if desired. Table 13.5 lists the new GUI controls you need to add to your plug-in for interfacing with the delay object. Figures 13.12 and 13.13 show the GUIs for RackAFX and VST3/AU

DelayLine.h
DelayLine.cpp
StereoDelayFX.h
StereoDelayFX.cpp

To use the delay object, you need to implement the following chunks of code:

# Declaration

In the plug-in's h file, add the #include statement and add a member variable for the delay.

```
CStereDelayFX
m_DelayFX;
```

# Initialization

Initialize the object in your one-time function where the sample rate is known. This is one line of code to add before the main update function.

Table 13.5: CStereoDelayFX GUI Control List.