
The diagrams in Figure 14.32 illustrate several common impedance configurations with associated leakage currents. In each case, an input (impedance) circuit is connected to the device; the device can be either an analog or a digital component. The purposes of the various input circuits include:

### Digital Device

- To define the state of unused inputs or inputs that are driven by a tristate driver that is in a high impedance mode.
- To define the termination impedance of a driven line in a bus or networked context.

### Analog Device

- To define or establish an input bias state.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_758_0.png)

Figure 14.32 Leakage Currents in Common Configurations.

In the diagrams, the device can be as simple as a single logic gate, transistor, or operational amplifier or as complex as a CPU, FPGA, A/D converter, or analog control subsystem. The current directions shown are merely illustrative; in practice, the direction of the current flow will be dependent on specific device and type.

## 14.21.2.2 Addressing Static Power Consumption

### 14.21.2.2.1 POWER GATING

power gating

Looking at the circuits in Figure 14.32, the pull-up and pull-down impedance networks provide paths for leakage currents to flow. Utilizing a technique defined as *power gating* can help to significantly reduce leakage current power consumption.

Power gating is a scheme invoked during passive periods, following power ON, and during normal idle or sleep periods punctuating active periods. When activated, the pull-up and pull-down devices are disconnected from the power rails and clocks and other timing elements are turned off. Doing so can significantly reduce or eliminate substantial portions of leakage current power consumption. The devices are reconnected or re-enabled as needed when active periods commence or resume.

When utilizing power gating, however, one must ensure that disconnecting state defining impedances from device inputs does not allow the device to enter an intermediate (metastable) state in which partially conducting semiconductor elements provide a path to ground.

**zero delay** One important issue that can occur when utilizing power gating in a static or dynamic context is the need to ensure minimum delay in reconnecting the impedance networks. Such a scheme is often referred to as a zero-delay technique. A second important issue is to ensure that the devices managing the connections do not provide an alternative leakage path to ground.

### 14.21.2.2.2 FLOATING INPUTS

When working with small-scale integrated circuit (SSI) or medium-scale integrated circuit (MSI) logic devices or some of the more complex very large-scale integrated (VLSI) or FPGA devices, having some portions of the device unused is not unusual. All such unused components should be put into a low power state. In particular, devices should not be left with unused open or floating input pins. Under such conditions, active components can not enter a state in which the implementing series transistors are both ON or partially ON, thereby connecting power to ground and, thus, significantly increasing the current draw.

When complementary output symmetry MOS (CMOS) logic was first developed, a colleague reimplemented an earlier design for a subsystem in a weather satellite using the new logic devices. He expected to see a significant decrease in power consumption. To his disappointment, power consumption actually increased. Following a little debugging, he observed that he had left inputs on the unused gates in his ICs unconnected. After properly connecting them so that the unused parts were disabled, he was excited to see that his power consumption had dropped below even what he had calculated and expected.

### 14.21.2.2.3 DIGITAL INPUTS AND OUTPUTS

To ensure accurate input signal recognition and proper operation of a digital device, logic 1 or high signals into the device cannot be lower than a specified minimum value and logic 0 or low signals cannot be higher than a specified maximum value. Pull-up or pull-down resistor networks are often used to define the state of an unused inputs driven by a tristated driver, as was illustrated for several circuits in Figure 14.32. As such, such networks can be a significant source of power consumption.

If a pull-down resistor is used, the value needs to be small enough such that for a floating (tristated driver) input, leakage current through the resistor from the driven device cannot yield a voltage that exceeds a specified maximum low level V_IL,max value. At the same time, the resistor must be large enough to enable a driven logic 1 input above the specified minimum V_IH,min value, which a very small pull-down impedance value may not permit. Further, if the pull-down resistor is too small, a large current flow from a device trying to drive to a logic 1 signal can add to system power consumption. The general design heuristic in such cases is to use a large value pull-up rather than a pull-down resistor.

### 14.21.2.2.4 PCB LEAKAGE CURRENTS

Another source of leakage currents arises from the leakage resistance of the standard printed circuit board. Both surface contaminants and the dielectric impedance of the implementing material (typically FR4, a glass fiber composite) can provide paths for such currents to flow, potentially to ground. From Ohm's law, current through an impedance yields power: V^2/R or I^2R. Such leakage problems can be significantly reduced or eliminated by well-designed guards. See the material on signal integrity in Chapters 20 and 21.

## 14.21.3 Dynamic Power Consumption

Turning to dynamic power consumption, we begin with a very high-level model of the system and its power consumption. We view the embedded system as a simple black box with an external supply as we see in the upper diagram in Figure 14.33. Looking inside the black box, as illustrated in the lower diagram, we see the state diagram reflecting the behavior of the system when power is first applied to the system. We move from Power OFF to Static then to Dynamic power consumption. With the voltage applied, current flows into the box from the power source. Following Power ON, the typical system will enter a boot up or initialization state and has initiated minimal activity.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_760_0.png)

Figure 14.33 States of Power Consumption.

- **Idle State** As the system, or a portion thereof, transitions from a passive state to a dynamic state, a significant current surge can occur as the current that the active elements are requiring increases. Following the initial activity, the system may enter an Idle State or any of the states in which it is now running both the hardware and software as it is performing its intended tasks.

- **Maximum dynamic**

- **Normal dynamic** The dynamic state can be characterized as being comprised of varying groups of parts with differing levels of activity ranging from OFF, to sleep, to idle, to low power, or to fully active. When the system is engaged in performing its worst case operating activity, as noted earlier, the state is identified as the level of maximum dynamic power consumption. Power consumption levels between these two extremes typify normal dynamic activity and evolve to and from differing levels, corresponding to the level of activity.

### 14.21.3.1 Sources of Dynamic Power Consumption – Hardware

Sources of the hardware contribution to dynamic power consumption can be classified into two major groups:

- **Pure hardware**
  - Pure hardware comprises those components that are essential to the core operation of the system in its active state and, therefore, must be operational full-time.

Potential devices in this category can include (portions of) the main CPU, the necessary subset of cores in a multicore system, ROM-based instruction memory and RAM external to the CPU, essential input and output drivers, important system peripherals, the system clock and time base as well as other critical components.

### Pure controlled hardware

Pure controlled hardware comprises those components that can be turned off and disconnected from power or those that can be turned off or put into an idle, low power, or sleep mode yet remain connected to power. Potential devices in this category can also include (portions of) the main CPU, the nonessential subset of cores in a multicore system, certain timers, ROM-based instruction memory, and RAM external to the CPU.

### 14.21.3.1.1 PARASITIC DEVICES AND SWITCHING

Digging deeper into the real world, circuit components live in regions populated by demons discovered by hundreds of physicists in times past. Gauss, Lenz, Maxwell, Faraday, and all their friends explored, introduced, and taught us of the black magic world populated by electromagnetic fields and passive parasitic resistors, capacitors, and inductors of all sorts and varieties. Switching current through any of these parasitic, seemingly invisible, devices will consume power.

Figure 14.34 illustrates typical totem pole output configurations of standard CMOS and bipolar devices. Generally, parasitic capacitances to ground will also exist on the inputs and outputs of the devices as illustrated. That capacitance can be, and often is, the parallel combination of a number similar parasitics from different nearby sources. During switching, an additional current flow, I1 and/or I4, will occur to charge or discharge the capacitances, thereby adding a component to the dynamic power consumption.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_761_0.png)

Figure 14.34 CMOS and Bipolar Totem Pole Input and Output Configurations.

In either case, the device can source current through the top transistor when the input is a logical 0 and sink current through the bottom transistor when the input is a logical 1.
