+   To complete her analysis,
+   (a) Identify and label all of the currents in the circuit above if the input signal to the circuit above is a logical 1.
+   (b) Identify and label all of the currents in the circuit above if the input signal to the circuit above is a logical 0.
+   (c) For each of the combinations she has listed above, based on vendor data sheets, what is the maximum number of gates we can drive and still meet the vendor's specifications if the input signal is a logical 1? logical 0?
+   (d) What is the worst case noise margin for each configuration and for each logic state?

![](bbox=[0.52, 0.08, 0.9, 0.26])

| $I_{OH}$ | -400 $\mu$A | @ $V_{OH} = 3.4$ V |
| $I_{OL}$ | 4.0 mA | @ $V_{OL} = 0.4$ V |
| $I_{IH}$ | 20 $\mu$A | @ $V_{IH} = 3.4$ V |
| $I_{IL}$ | -500 $\mu$A | @ $V_{OL} = 0.4$ V |

+   Assume that the driver is an SN74LS04 and that the diode requires 1.25 mA to turn on. To settle the debate, you decide to do a complete analysis of the circuit.
+   (a) Based on your analysis, which configuration will give the brighter light?
+   (b) Which configuration will consume more power?
+   (c) What are the noise margins for the two configurations if one additional SN74LS04 device is to be driven?

| LED | ON | 1.25 mA |
| | OFF (leakage) | 1 $\mu$A |
| Relay | ON | 1.5 mA |
| | OFF | 0 $\mu$A |

![](bbox=[0.13, 0.57, 0.45, 0.68])

The design specifications require that, in addition to the relay and LED, the circuit must be able to drive four other gates. Determine if the design meets the specified requirements.
2.4 A warning annunciator is needed in a design that you are working on. In a discussion with several of your colleagues, several say the two circuits given in Figure P2.4 are equivalent, others say that the one on the left is better, while the remainder recommend the one on the left.

![](bbox=[0.52, 0.57, 0.85, 0.78])

Assume that the driver is a 74LS244 and the inverter is a 74LS04. Analyze the two circuits and select the values for the