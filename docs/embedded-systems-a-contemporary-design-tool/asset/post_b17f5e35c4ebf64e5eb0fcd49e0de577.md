
### 19.4.2 Programmable Array Logic – PAL

In the PAL or Programmable Array Logic device, the AND portion of the device is programmable and the OR portion is fixed. Such an architecture limits the number of product terms in the sum. Furthermore, the product terms are not reusable and must be duplicated if required. The implementation uses a fixed OR array. The output of each product term can be connected to only one OR gate. Typically, the device supports bidirectional I/O pins and tristate outputs with individual enables.

The structure of the device is shown in Figure 19.5. In the diagram, though drawn as only a single input to each device in the arrays, each supports multiple inputs. The open circles illustrate the programmable links.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_938_0.png)

### 19.4.3 Programmable Logic Array – PLA

In contrast to the PAL, in the PLA as shown in Figure 19.6, both the AND and the OR portions of the device are programmable. Consequently, the product terms are reusable.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_938_1.png)

### 19.4.4 Programmable Logic Sequencer – PLS

The PLS, which is also referred to as a registered device, is simply a PLA plus flip-flop storage elements. In most designs, the outputs of the storage elements are fed back to the logic array to support finite-state machine design. For these devices, both the AND and OR arrays are programmable. Once again, the product terms are reusable. A fragment of such a device is shown in Figure 19.7.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_939_0.png)

Figure 19.7 Basic Programmable Logic Sequencer

### 19.4.5 PLA vs. PAL vs. (P)ROM

A PAL is the opposite of a PROM. We can view the PROM as an AND-OR array with a fixed AND array and with all 2^n AND possibilities available. If a design needs a large-number of AND combinations, the PROM is a good option. Some example applications include lookup tables, high-speed mathematics, or code translations.

If the design requires only a few AND combinations and not many of those are shared between outputs, the PAL with the fixed OR array is a good choice. If complete flexibility is necessary, the PLA with its programmable AND and OR arrays is more appropriate.

## 19.5 PROGRAMMABLE AND REPROGRAMMABLE TECHNOLOGIES

Programmable logic devices fall into two major categories: programmable and reprogrammable. Those in the first category can be programmed one time and those in the second multiple times.

### 19.5.1 Programmable Technologies

Devices that are one-time programmable are either built to order by the manufacturer of the device or utilize a technology that will permit the designer to enter the desired configuration one time. Devices built by a vendor mirror the technologies studied earlier for implementing ROM-type devices. Transistors are selectively included to produce the desired behavior. Antifuse devices that can be programmed once, in the field, are often based on a technology called the antifuse. In traditional electronics, a fuse is utilized in a circuit to protect against potentially damaging high currents by opening a conducting path when necessary. The anti-fuse is designed to do the opposite. When a sufficiently high voltage is applied across an amorphous silicon link between two metal conductors, a metal-crystalline alloy is formed to complete the conducting path. The newly formed conducting path(s) enable the interconnection of generic blocks of primitive logic components to form more complex logic circuits. Once the low-resistance path is formed, the process is irreversible.

### 19.5.2 Reprogrammable Technologies

Today's (re)programmable logic devices are generally either Static Random Access Memory (SRAM) based or use variations on programmable ROM technologies. SRAM-based architectures are built around volatile Read/Write memory cells that control the state of intra-device connections. The device configuration and interconnection information are held in a companion nonvolatile storage medium such as a PROM or similar flash type of external boot device. One significant advantage of such an approach is that the configuration of the device can be dynamically changed at runtime, thereby permitting the system to adapt to the problem at hand.

Floating gate programmable ROM technologies fall into three broad categories: EPROM, Electrically Erasable PROM (EEPROM), and FLASH. All three of these devices are built on what are known as floating gate technologies. To introduce the concept, we will begin with the memory fragment in Figure 19.8, which gives a high-level view of a portion of a programmable AND array.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_940_0.png)

Figure 19.8 Programmable ROM Memory Architecture

Each column in the AND array implements a NOR type AND, that is, an AND of low true signals. All transistors on a column must be OFF for the output to be logical 1. Each N-type transistor comprising the AND has two gates. One of the gates is floating, that is, unconnected, and is surrounded by high-impedance insulating material as shown in Figure 19.9.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_941_0.png)

Figure 19.9 Dual Gate Programmable Memory Device

Initially, the floating gate has no charge on it and thus has no effect on circuit operation. All transistors are effectively connected. When a positive voltage is applied to the nonfloating gate, the transistor turns ON and the output of the associated AND is logical 0. To program the device, a high voltage is applied to each location where a link is not wanted, as shown in the first diagram in Figure 19.10. Through avalanche injection, a negative charge collects on the floating gate. When the programming voltage is removed, a number of electrons are trapped on the floating gate as shown in the second graphic. The trapped electrons cause an increase in the threshold voltage of the transistor to approximately 7.0 V, which thereby prevents the transistor from turning ON when a normal logical 1 is applied to the nonfloating gate as illustrated in the final drawing. The transistor is effectively disconnected from the circuit. Tests have shown that the charge can be retained for up to 10 years.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_941_1.png)

Figure 19.10 Programming of a Dual Gate Programmable Memory Cell

In the early years, an ultraviolet light was used to erase the device. Under the ultraviolet light, the floating gate becomes slightly conductive. Charges trapped during programming are given enough energy to leak away. Such devices are known as EPROMs – erasable PROMs.

Today's devices are significantly improved from the early designs. The floating gate is surrounded by an ultra-thin insulating layer. Rather than using an avalanche injection scheme, charge is placed onto the floating gate using tunneling physics. The devices are also electrically erasable. The device can be erased by applying a voltage of opposite polarity to the charging voltage on the nonfloating gate. Thus, we can use the same equipment as was used to program the device. Cross-sectional diagrams of two contemporary types of programmable device are given in Figure 19.11. The diagram on the left illustrates what is called the electrically erasable device, EEPROM. That on the right is known as FLASH technology.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_942_0.png)

## 19.6 ARCHITECTURES

Independent of whether the PLD appears as a PLD, CPLD, or FPGA, the architecture of the device comprises blocks of combinational logic and/or storage elements, the Input/Output logic, and the interconnections between these blocks of functionality. The size (or grain) and flexibility of the logic blocks and the speed and generality of the interconnection net determine the power and capabilities of the device.

The PLD and CPLD devices tend to be coarser grained. The building blocks are generally referred to as macrocells. They can be viewed as the programmable logic equivalent of MSI logic blocks. In contrast, the FPGA devices are usually finer grained with a very rich interconnection topology. The building blocks, often built as lookup tables (referred to as LUTs), tend to be the SSI logic equivalent.

Today, the devices range in capability from simple encoding or decoding networks to the ability to implement a full CPU core (refer back to Chapter 1) with accompanying peripheral devices. We will examine the architecture of these devices in greater detail beginning with the PLD.

### 19.6.1 PLDs

The simplest devices are known as PLDs, or programmable logic devices (distinguished from the general use of the term to describe the complete class of programmable devices). The basic devices are intended to replace collections of combinational logic circuitry implemented using SSI and MSI components. The devices are implemented as the AND array—OR array pair discussed earlier.

*generic array logic* Lattice Semiconductor provided an early implementation of such a device called a generic array logic, or GAL16V8™ device. The GAL™ supports 16 inputs and 8 outputs that are configured as 10 input only, 2 output only, and 6 that are bidirectional. Each output can accept up to seven product terms; each product term can have up to 32 inputs. The circuit
