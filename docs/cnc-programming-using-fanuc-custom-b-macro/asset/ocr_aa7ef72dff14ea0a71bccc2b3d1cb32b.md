![](bbox=[0.22, 0.07, 0.85, 0.32])

**Figure 12.1** An NPN transistor.

The ratio of I_C to I_B is called the current gain of the transistor, a typical value being 100. (Since the current gain is typically very high, I_C and I_E would be nearly equal.) This describes the use of a transistor as a current amplifier. However, beyond a certain value of base current, R_CE becomes nearly zero. As a result, I_C does not increase any further, and the transistor is said to be saturated. In saturation mode, I_C depends on external resistance (load) and power supply; with the transistor offering nearly zero resistance to the current flow. Such an ideal transistor characteristic is shown in Fig. 12.2.

Thus, a transistor can be used as an electronic switch, in saturation mode. For such a use of a transistor, the circuit (regulating the base current) is designed in such a manner that the transistor remains either OFF (I_B = 0, resulting in I_C = 0) or becomes saturated.

The digital inputs/outputs of a PLC use similar electronic switching. However, to protect the internal circuits from external currents, generally some kind of optoisolator is used. An optoisolator is a device consisting of a light-producing element, such as an LED, and a light-sensing element, such as a phototransistor. When a voltage is applied

![](bbox=[0.16, 0.738, 0.8, 0.926])