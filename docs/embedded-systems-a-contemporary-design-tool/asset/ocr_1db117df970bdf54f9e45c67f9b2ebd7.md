![](bbox=[0.28, 0.08, 0.75, 0.29])

the measurement device is frequently copper. Because copper is a different metal from the thermocouple alloys, by making a connection to the thermocouple, additional thermocouples are introduced as illustrated in the drawing. These additional thermocouples produce the voltages VjuncA and VjuncB as shown. Examining the circuit in the drawing, observe that the Voltage VAB will equal the algebraic sum of the voltages VjuncA and VjuncB. If the thermocouple–copper junctions (JuncTA and JuncTB) are maintained at the same temperature, they will act as a single thermocouple (driven by TR). Under such a condition, when making the measurement, the voltage value that is read will be proportional to the difference between TR and TM.

Once the voltage measurement of the thermoelectric voltage (VAB) is complete, the first operation in converting that value into an equivalent temperature value is the algebraic addition of the voltage measured at the reference junction terminals (VjuncA and VjuncB) – this is the resulting sum represents an approximation of the thermoelectric voltage generated at the temperature–sensing junction (TM in the figure).

# 17.8.3 Working with Nonlinear Devices

National Institute of Standards and Technology (NIST)

Thermocouples, like many other real-world sensors and transducers, have a monotonic non-linear relationship between the physical parameter and the electrical signal that is actually measured. In the United States, the National Institute of Standards and Technology (NIST) provides equations expressing such relationships. The equations are normally given in the form of a power series accompanied by tables of coefficients corresponding to the type of device and the ranges over which it is operated.

The mathematical operations for performing the conversion from the measured signal to the physical quantity are carried out in the software driver for the measurement device. The significant overhead in evaluating the power series for each measurement is an unreasonable burden in most applications. Thus, the series is often replaced by a linearized version of the polynomial. Such an approximation can be a linear fit (y = mx + b) or a higher order fit based on the degree of conformity required for the application.

In general, the approximation comprises a number of linearized segments. The length of each segment is determined by the required conformity to the actual curve for the measurement being made. To see this, consider the following curves in Figure 17.20 that are approximated by a linear curve fit.