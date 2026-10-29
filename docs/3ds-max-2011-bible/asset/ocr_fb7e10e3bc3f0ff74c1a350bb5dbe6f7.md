# Chapter 34: Using Animation Layers, Modifiers, and Complex Controllers

The Set Active button lets you specify which controller you can interactively control in the viewport; the active controller is marked with an arrow, which is displayed to the left of the name. You also can cut and paste controllers from one track to the list. Because you can use the same controller type multiple times, you can distinguish each one by entering a name in the Name field.

# On/Off controller

The On/Off controller works on tracks that hold a binary value, such as the Visibility track; you can use it to turn the track on and off or to enable and disable options. In the Track View, each On section is displayed in blue, with keys alternating between on and off. No parameters exist for this controller. Figure 34.26 shows a Visibility track that has been added to a sphere object. This track was added using the Tracks → Visibility Track → Add menu command. You can add keys with the Add Keys button. Each new key toggles the track on and off.

# Note

You also can add a Visibility track by changing the Visibility value in the Object Properties dialog box. ■

# FIGURE 34.26

The On/Off controller lets you make objects appear and disappear.

![](bbox=[0.03, 0.429, 0.615, 0.626])

# Waveform controller

The Waveform controller can produce regular periodic waveforms, such as a sinusoidal wave. Several different waveform types can make up a complete waveform. The Waveform Controller dialog box, shown in Figure 34.27, includes a list of all the combined waveforms. To add a waveform to this list, click the Add button.

When you select a waveform in the list, you can give it a name and edit its shape using the buttons and values. Preset waveform shapes include Sine, Square, Triangle, Sawtooth, and Half Sine. You also can invert and flip these shapes.

The Period value defines the number of frames required to complete one full pattern. The Amplitude value sets the height of the wave, and the Phase value determines its location at the start of the cycle. The Duty Cycle value is used only for the square wave to define how long it stays enabled.

You can use the Vertical Bias options to set the values range for the waveform. Options include Centered, which sets the center of the waveform at 0; Auto > 0, which causes all values to be positive; Auto < 0, which causes all values to be negative; and Manual, which lets you set a value for the center of the waveform.