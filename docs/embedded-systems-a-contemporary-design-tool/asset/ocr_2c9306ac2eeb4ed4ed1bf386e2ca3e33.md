# 16.3.2.6 Bidirectional Bus

Higher speed systems with hard real-time constraints will often have two unidirectional busses, thereby eliminating the cost of turning the bus around. The design in Figure 16.13 illustrates a first attempt at a bidirectional bus.

![](bbox=[0.27, 0.17, 0.65, 0.45])

Figure 16.13 A Bidirectional I/O Bus – design 1

Let's look at the pieces of this system. First, notice that the bus lines are buffered as they come off the bus into the device. This is done to ensure a known load on the bus. Next, each of the bus lines has a pull-up resistor to VCC to ensure that there is never a floating signal line.

This design uses a single control signal to select whether the processor or the device is driving the bus. Such a scheme can create several different problems.

Consider the following sequence of events:

+   1. The state of the direction line is changed from logical 1 (device on the bus) to logical 0 (processor on the bus).
+   2. The state change will enable the tristate drivers on the processor and allow them to begin driving the bus.
+   3. Simultaneously, the state change on the direction line begins to propagate through the inverter to the tristate control on the drivers on the device. The delay through the inverter permits both sets of drivers to be on the bus for the length of the delay.

The consequences of having both sets of drivers on the bus simultaneously include:

+   - Excessive current draw as the drivers are fighting, producing noise in the power and ground system.
+   - Excessive power consumption in the system.
+   - Potential damage to the drivers.