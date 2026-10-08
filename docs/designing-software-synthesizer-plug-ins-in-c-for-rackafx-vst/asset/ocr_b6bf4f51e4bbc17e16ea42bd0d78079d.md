In Bckfrth, the vector path starts at vertex 0 uninterrupted to the final vertex, where it turns around moves backwards to the starting vertex 0, reverses direction again and moves towards the last vertex. This operation repeats and the program progresses. This mode is taken from AniMog and is not available on the ProphetVS/Wastvation.

![](bbox=[0.318, 0.045, 0.952, 0.213])

# # 11.7 The Vector and JS Program in RackAFX

RackAFX includes a vector joystick control in the classic ProphetVS/Wastvation orientation, a square turned on and shaped like a diamond

as in Figure 11.22. The x-axis is labeled A-C and the y-axis is B-D. The <Joystick> button shows the control and the <Program> button is used for programming. There are set of drop list boxes that may optionally populate with values and receive messages when the users select an item. The idea is to show what kind of oscillator, waveform or sound source is attached to each of the four A, B, C, and D, and allow the user to change that sound source. For VectorSynth and AniSynth, populating these boxes is optional and these synths have fixed sources, you won't mean much. You can add, more-samples to the project and eventually manage the controls with multiple choices to allow the user to map many different sounds to the apex of the mix surface. To set these boxes, you click on the down-arrow to the right, and an item appears says "Select to Setup. Select this item from the list, and finally enumerated UINT dialog opens--same as the radio buttons. You enter a variable like m_uSapexList, and an enumerated list, like "saw, sine, triangle, square". When the users select an item, updating is set with the zero-based index of the item in the list, and userInterfaceChange() is called. The ControlID values for the four boxes are 60, 61, 62, and 63 for the A, B, C, and controls.

![](bbox=[0.418, 0.223, 0.852, 0.375])

For our projects the most important controls are the vector itself and the joystick logic. Unlike of the RackAFX controls, the joystick does not map to any variable in your plug-in and does not call userInterfaceChange(). Instead, it calls an exclusive message handler joystickControlChange().

Figure 11.22 The vector joystick in RackAFX uses the classic Prophet orientation.

```
floatControlChange(float fControl, /* Vector Mix A *//
float fControl, /* Vector Mix C *// float fControl, /* Vector Mix D *// floatFACMix, /* A-C Projection *//
float FBDMix() /* B-D Projection */
```

There is a comment about the function to remind you the moves by one pixel on the screen, so it may be called in rapid succession; make

This function is called when you don't place time consuming in this message handler. Typically, you copy the new joystick mix values into the plug-in; here we are using global parameters:

Table 11.1: A multi-dimensional array stores the joystick program as a set of rows.