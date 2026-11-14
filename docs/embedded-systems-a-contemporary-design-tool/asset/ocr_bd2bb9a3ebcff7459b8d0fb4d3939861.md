# # Working Outside of the Processor III: Interfacing to Remote Devices

# ## THINGS TO LOOK FOR ...

+   - Some of the commonly used architectures for network-based interfaces.
+   - Some of the strengths and weaknesses of the different architectures.
+   - The different transport mechanisms.
+   - The control and synchronization schemes utilized for the different architectures.
+   - The implementation of device and subsystem addressing in each of the different designs.

# ## 18.1 COMMON NETWORK-BASED I/O ARCHITECTURES

We have been studying the many different ways that one can interact with and incorporate the world outside of the core microprocessor into an embedded design. That world includes devices that are local to the immediate context and those that may be substantially remote. Let's now look at some specific examples of how such techniques move from the textbook to the real world.

In this chapter we will study four different, commonly used network-based input/output designs. For each design, we will briefly examine the problems that motivated designers to develop the interface, identify the contributions that each has introduced to the embedded world, and cite the strengths and weaknesses of each approach.

Following the model of intertask communication and synchronization developed in earlier chapters, for each scheme we will examine the transport mechanism, study how control and synchronism are affected, and investigate how message senders and receivers are identified.

We will open with an examination of the traditional RS-232, which is now the EIA-232 standard asynchronous serial interface. We will then explore a synchronous serial interface approach utilized by the Universal Serial Bus (USB). The PC bus as a small local area network (LAN) will be the next design that we will study. Finally, we will conclude with the Controller Area Network (CAN) bus, another type of LAN commonly used in automotive applications.

These busses were selected because each represented a change in thinking about the way information was exchanged in the context in which the design was applied.