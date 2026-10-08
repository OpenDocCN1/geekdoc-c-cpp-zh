jTextField maintains the GUI parameters, IMIDIMapping deals with mapping the MIDI CC's to GUI parameters, and IViewGroup is used to instantiate our GUI.

One of the responsibilities of the Processor is to declare the plug-in's input and output capabilities. There are three different kinds of I/O for the Processor: audio, MIDI events and parameters. Figure 2.22 shows the block diagram of a generic Processor. The audio and MIDI Events move busses, which are zero-indexed and named bus 0, bus 1, etc. A plug-in may have any combination of input and output buses. In the most generic version here, the Processor may receive and transmit MIDI events and control change information.

Audio busses may have any number of channels so as not confuse bus with channel. Our synth plug-ins are going to implement a single audio output bus named bus 0 but bus 3 that is stereo with channels. MIDI event busses some number of MIDI channels, which we decide upon. There is only one parameter bus that the processor does not have to declare. Our synth plug-ins will only accept input parameters and will not transmit any, though template code it if you want to experiment with passing parameters and MIDI information out of the plug-in.

The component shown in Figure 2.23 depicts how the GUI communicates with the Parameters in its container. In this case the GUI might be the default version or a custom design. MIDI CC information may be mapped to the GUI controls as a kind of external control mechanism. We also may use sub-controllers as helpers for some of the more complicated GUI controls; we will use this for the joystick controller in Chapter 11. The Controller object does not have to declare any busses, and the underlying interfaces do most of the work for you, so you really need to set up the Controller and optionally a custom GUI. After everything is properly set up, it will essentially handle its own operation. This is a nice feature of VST3.

![](bbox=[0.198, 0.447, 0.8, 0.696])

Figure 2.21: A more complete view of the VST3 plug-in architecture shows its COM components and interfaces.

Figure 2.22: A generic plug-in Processor component includes busses for dealing with I/O.

![](bbox=[0.398, 0.773, 0.953, 0.91])

Figure 2.24 shows a complete diagram of the VST3 synth architecture. A MIDI controller sends events to the Processor and control events to the Controller. The Processor has only one input bus, the bus 0 and only one output bus, the stereo output bus 0. Although the Controller maintains the user interface, the Processor will also receive control change information. The