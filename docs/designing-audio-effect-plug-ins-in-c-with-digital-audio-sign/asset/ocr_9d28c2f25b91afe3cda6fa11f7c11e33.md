the volume does indeed change. Congrats on your first plug-in!

What makes this plug-in so easy and quick to develop is that the slider volume control maps directly to a variable that is used in the processAudioFrame() function, as depicted in Figure 3.14. This means the data coming from the slider can be used directly in the algorithm. The data coming from the slider and controlling m_fVolume is said to be raw data. You use the raw value to affect the signal processing algorithm.

# 3.10 Design a Volume-in-dB Plug-In

This next example will show you how to cook your raw data to be used in the signal processing algorithm. The VolumedB plug-in will also be a volume control, but will operate in dB instead of using a raw multiplier. You may have noticed that your previous volume control didn't seem to do much in the upper half of the throw of the slider. This is because your ears hear logarithmically and so linear deflections of the slider do not correspond to linear changes in perceived loudness. To fix this, we'll design another plug-in that will operate in decibels (dB). The block diagram is identical to the first project, only the control range of values has changed.

+   - a2 = -96 dB: Mute
+   - a2 = 0 dB: Max volume

Now, the volume control is specified in dB, so you need a formula to convert the dB value to a scalar multiplier for the algorithm. You should memorize the dB equations now if you haven't already, since they will reappear over and over in audio plug-ins. This is the cooking formula that will take the raw data from the slider –96 to 0 dB and cook it into a variable we can use in our scalar multiplication:

```
dB = 20log(x)
x = 10^(dB/20)
```

You set up the cooking formula by implementing the userInterfaceChange() function which is always called when the user changes anything on the control surface. When the user moves the slider, you cook the data. This is shown conceptually in Figure 3.15.

The cooking function simply converts the dB into a scalar multiplier. In this case, the cooking function is short enough to simply leave inside the userInterfaceChange() function; as the cooking functions become more complex, you will probably want to break them out into separate functions, which are called from userInterfaceChange(). Remember the two RackAFX rules you've learned so far:

> Coefficients in a block diagram (or transfer function or algorithm) become float member variables in your plug-in code. Each slider or button control on the UI will map to and control a member variable in your plug-in.