# Working Outside of the Processor II: Interfacing to Local Devices

# THINGS TO LOOK FOR ...

+   - Some of the commonly used architectures for local device interfaces.
+   - Some of the strengths and weaknesses of the different architectures.
+   - The different transport mechanisms.
+   - The control and synchronization schemes utilized for the different architectures.
+   - The implementation of device and subsystem addressing in each of the different designs.

# 17.1 SHARED VARIABLE I/O – INTERFACING TO PERIPHERAL DEVICES

In this chapter, we will continue to study the many ways that one can interact with the seemingly endless array of peripheral devices in the world outside of the local microprocessor. In the previous chapter, we studied network-based systems. The primary purpose of such remote systems is to move information from one point within the system to another or to utilize computational capability that may not be available within the local components.

In the embedded world, we also routinely work with a wide variety of analog and digital signals typically originating in or being sent to devices within the local proximity. As inputs to the application, such signals can originate either from the environment surrounding the application or from the myriad peripheral devices that may comprise the application. As outputs, they may be generated as control signals to a portion of the application or as captured data being sent somewhere for further processing. Such signals are dealt with more effectively utilizing a shared variable model.

Analog signals may arrive directly or indirectly (transduced) as inputs from physical world signals, or they may be produced as outputs from an internally generated digital data source. Digital signals may also arise as inputs from physical world signals originating in either the time or frequency domains or from a direct interface to a wide variety of peripheral devices that produce digital data. As outputs, they may function as control or configuration information for a peripheral device or information to be stored or displayed.