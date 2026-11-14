
fan-out = \left| \frac{-400 \, \mu\text{A}}{20 \, \mu\text{A}} \right| = 20 \quad (2.2)

Thus, when its output is in the logical 1 state, an SN74LS04 can source current to 20 similar devices.

In this case, the fan-out for the two configurations is the same. If the values were different, we would select the lower value as we see in the following example.

## EXAMPLE 2.1

In the circuit in Figure 2.7, the device identified as the Driver has an output that is connected to a light-emitting diode (LED) circuit and is also fanning out to a number of other gates.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_125_0.png)

**Figure 2.7** One Device Driving Several Different Kinds of Loads

When the output of the device is a logical 0, the warning LED is to be illuminated, leading to current flow as shown by the arrow in Figure 2.7. When the output of the Driver gate is a logical 1, the warning LED is off and no current flows through the LED.

The devices have the following specifications:

| Component | Specification | Condition |
|---|---|---|
| Inverter | I<sub>IL</sub> = -400 µA | |
| | I<sub>IH</sub> = 20 µA | |
| Driver | I<sub>OL</sub> = 24 mA | for V<sub>OL</sub> = 0.2V |
| | I<sub>OH</sub> = -15 mA | for V<sub>OH</sub> = 3.5V |
| LED current | 10 mA | |

To compute the fan-out for the driving device, we apply Kirchhoff's current law at node N1 for both logic states.

### Logical 1

If the output of the Driver is in the logical 1 state, the currents will appear as in the drawing in Figure 2.8. Summing currents at node N1 gives the results shown in the figures.

i1 + i2 - i3 = 0 \quad (2.3)

Since the LED is specified as OFF under the current conditions:

i3 = i1

i3 = 15 mA

fan-out = \frac{i3}{i4}
= \frac{5 \, \text{mA}}{20 \, \mu\text{A}}
= 750

![](img/679b8d2d47f1bf86e17aca48f596f5cc_126_0.png)

**Figure 2.8** Driving to the Logical 1 State

### Logical 0

If the output of the Driver is in the logical 0 state, the currents will now appear as in Figure 2.9. Observe that bubbles on the logic symbols are altered to reflect the logical 0 values on the respective gates. Once again, summing currents at node N1 gives,

```
-i1 + i2 + i3 = 0
(2.4)
```

For this case, i2 is not 0 and must be taken into account.

```
i3 = i1 - i2
i3 = 15 mA - 10 mA
fan-out = i3 / i4
= 5 mA / 20 µA
= 250
```

![](img/679b8d2d47f1bf86e17aca48f596f5cc_126_1.png)

**Figure 2.9** Driving to the Logical 0 State

In the logical 0 case, the driver must be able to sink the current from the LED as well as that from the collection of inverters. After the LED current has been taken into account, substantially less remains available for the inverters. As this analysis illustrates, in the logical 0 case, the fan-out is reduced to 250. Thus, we must use the smaller of the two figures in any design. The fan-out for the circuit is determined to be 250.

We now extend our two-switch device output model to incorporate the nonideal output signal levels by adding two resistors as shown in Figure 2.10. The resistors will model the ON resistance of the top and bottom transistors in the totem pole output configuration. When the device is sinking current, from Ohm's law, there will be a voltage drop across R2, giving an increase in the output voltage from the ideal case of 0.0 VDC. Similarly, when it is sourcing current, we will see a drop across R1 and a corresponding decrease in the output voltage from the ideal value of +5.0 VDC. The device input interface can also be modeled as a resistor network and voltage source as shown in the right-hand figure.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_127_0.png)

**Figure 2.10** A First-Order Model for Device Input and Output Circuitry

When the device is sourcing current, that is, the input signal is a logical 0, from Ohm's law, there will be a voltage drop across R3. Under normal operation conditions, the worst case current draw will occur when the input is at 0.0 VDC. The output signal level from the driver, V_OL, is generally going to be higher. Lowering the input signal level below 0.0 VDC can potentially damage the part. Similarly, when the device is sinking current, there will be a drop across R4. Forcing the device to exceed the specified limit, once again, can damage the part.

## 2.3 A LOOK AT REAL-WORLD GATES – PART 2: TIME

In the ideal world, signal levels change from one state to another in zero time, and the effect of an input change on a device output is immediate. There is no delay. In the real world, signals take time to change state, and their effect on the output of a device will occur some time in future. Such delays and delayed behavior must be taken into consideration during design, particularly if signaling paths have tight time constraints. Under such constraints, one must carefully analyze the part's data sheet to understand the delays as well as to consider how any variations may affect the system behavior.

### 2.3.1 Rise and Fall Times

rise time, fall time. We define the time for a signal to change from one state to another as its rise time if the change is from a logic 0 state to a logic 1 state and as its fall time if the change is from logic 1 to logic 0. These times are specified as \(\tau_{rise}\) and \(\tau_{fall}\). In real-world parts, these two values are generally not the same. In fact, there can be as much as a two to one difference.

The parameters, how we measure them, and their asymmetry are illustrated in Figure 2.11. Observe that we measure the rise and fall time at the 10% and 90% points of the signal.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_128_0.png)

**Figure 2.11** Digital Signal Rise and Fall Times

Rise and fall times that are too long can create problems. Under such conditions, the gate no longer acts as a switch; instead, it becomes a rather poor amplifier and enters what is called a metastable region. We’ll discuss this shortly. metastable

The syntax for including rise and fall times in a Verilog device model is given as,

```
Syntax
# (riseTime, fallTime) deviceInstance
```

The following code fragment illustrates the inclusion of such parameters in a part model.

```
parameter riseTime = 1;
parameter fallTime = 2;
not #(riseTime, fallTime) myNot (sigOut, sigIn);
```

### 2.3.2 Propagation Delay

propagation delay. The time required for the effects of an input signal to be reflected in a corresponding change in a device’s output is called the propagation delay of the part. In response to an input signal, the time for the output to change from a logical 0 to a logical 1 is often different from a state change in the opposite direction. The two different propagation delays are designated \(t_{pLH}\) and \(t_{pHL}\).

Propagation delay can easily be observed in an inverter. If a high going signal is set as the input into the device, the output will change to low sometime later. We measure that time at the 50% point of two signals. The parameters, how we measure them, and their asymmetry are illustrated in Figure 2.12.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_129_0.png)

In real-time embedded applications, one of the major design concerns is meeting time specifications. Although in some cases the concern is about a signal arriving too quickly, generally the focus is on trying to ensure that the signal arrives before a specified deadline. Thus, when modeling a combinational circuit, we use the longer of the two delays, specifying that value as simply, τpd.

The syntax for modeling such a delay in Verilog is given by

```
Syntax
# delay LHS = RHS; // RHS changes and is assigned to LHS after
// delay
```

The following code fragment illustrates the inclusion of a delay of two time units in a part model.

```
parameter propagationDelay = 2;
not #propagationDelay myNot (sigOut, sigIn);
```

Verilog also supports the inclusion of device rise time, fall time, and delay. The syntax is given as

```
Syntax
# (rise time, fall time, delay) device;
```

The code fragment in Figure 2.13 illustrates the inclusion of a rise time of one time unit, a fall time of two time units, and a delay of three time units in a part model.

```
parameter riseTime = 1;
parameter fallTime = 2;
parameter propagationDelay = 3;
not #(riseTime, fallTime, propagationDelay)
myNot (sigOut, sigIn);
```

**Figure 2.13** Modeling Rise Time, Fall Time, and Propagation Delay
