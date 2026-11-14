# 17.7 MEASURING CURRENT

A current measurement is similar to a resistance measurement. Once again, the measurement can be implemented in a number of ways. One common method is to reverse the roles of the current source and the resistance in the design for measuring resistance. The resistor now becomes a current shunt – a precision resistor with typical values of 0.1–1 Ω inserted into the current path. The voltage across the shunt is measured and converted to the equivalent current using Ohm's law and the known value for the shunt. Such a design is presented in Figure 17.17.

![](bbox=[0.25, 0.235, 0.75, 0.455])

Figure 17.17 Measuring Current

As was done in the previous measurements, the process begins when the microprocessor issues a Start command. In response, the A/D closes both measure switches, thereby connecting the current source and the A/D to the unknown resistor. Once the measurement is complete, the A/D asserts the Complete signal back to the microprocessor, which can then issue a Read command at any time to retrieve the measured value. The conversion from volts to amps will typically be done in the associated measurement driver. The one drawback of using a shunt is the need to interrupt the current path to insert the shunt. An alternate scheme is to utilize a coil of wire wrapped around the conductor in which the current is to be measured and to measure the induced voltage. Basic physics provides the conversion to current.

# 17.8 MEASURING TEMPERATURE

Like the other measurements discussed to this point, a large number of approaches can be taken in making temperature measurements. One common and inexpensive technique is to use a sensing device called a thermocouple.

The phenomenon of thermoelectricity was discovered by a German physicist, Johann Seebeck, in 1821. He found that, when two wires made of dissimilar metals were connected to each other at two points and the two junctions held at different temperatures, a current will flow due to a phenomenon that is now called the Seebeck Effect. The force driving the current is known as the Seebeck thermal emf. The flow will continue as long as a temperature difference exists between the two junctions. This electromotive force (voltage) is the parameter measured in thermocouple thermometry.