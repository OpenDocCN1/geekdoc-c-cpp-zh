![](bbox=[0.28, 0.08, 0.45, 0.32])

![](bbox=[0.58, 0.09, 0.78, 0.32])

![](bbox=[0.28, 0.36, 0.45, 0.56])

![](bbox=[0.48, 0.36, 0.65, 0.56])

Figure 2.5 CMOS and NMOS Totem Pole Output Configuration

In Figure 2.5, the circuit on the left presents the CMOS configuration. The architecture remains a totem pole structure. The upper transistor is a PMOS (p-type metal oxide semiconductor) device and the lower an NMOS (n-type metal oxide semiconductor) device. The NMOS device, presented in the circuit on the right, is a simple modification of the CMOS device. The upper transistor is replaced by a second NMOS transistor implemented as a load device. They are shorthand for P channel and N channel. The ability of the top transistor to source current when the output of the device is a logical 1 and the bottom transistor to sink current when the output is a logical 0 is called the drive capability of the device.

# 2.2.3 Fan-In and Fan-Out

+   - **fan-out sources**: The number of devices that a typical gate can drive without degrading its specified minimum and maximum output logic levels is called the fan-out of the device. The fan-out of a device specifies how much current the device can source to other devices in logic high state and sink from other devices in the logic low state. Fan-in is a measure of a device's input current requirements.
+   - **sink, fan-in source**: It specifies how much current the device sources to other devices when the input is in the logical 0 state and sinks from other devices when the input is in the logical 1 state.
+   - **sinks**: 
+   - **sourcing current**: 
+   - **sinking current**: