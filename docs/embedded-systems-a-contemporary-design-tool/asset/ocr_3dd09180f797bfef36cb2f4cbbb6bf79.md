# ## 1.3.1 The Microprocessor

A microprocessor is an integrated implementation of the CPU portion (control and arithmetic and logical unit) of the machine; it is often simply referred to as a CPU or datapath. Microprocessors differ in complexity, power consumption, and cost. Today, microprocessors range from devices with only a few thousand transistors at a cost of a dollar or less to units with 5–10 million transistors and a cost of several thousand dollars.

One may also find differences in the internal architecture of the machine, including the number of internal registers, the overall control structure of the machine, and the internal bus structure. Registers are small amounts of high-speed memory that are used to temporarily store frequently used values, such as a loop index or the index into a buffer. Increasingly, the internal single-memory scheme that characterizes the von Neumann machine is giving way to the Harvard architecture and the benefits of simultaneous instruction and data access.

To implement a complete (embedded) computer system, we must still include the input/output subsystems and the external (to the microprocessor) memory system. We also include a clock or timing reference as the basis for timing, scheduling, or measuring elapsed time. All such components are connected via a system bus or buses. Figure 1.6 depicts a high-level block diagram of a microprocessor-based system.

![](bbox=[0.283, 0.423, 0.646, 0.653])

Figure 1.6 A Block Diagram for a Microprocessor-Based System

+   - firmware
+   - data store
+   - Read Only Memory
+   - ROM
+   - Random Access Memory
+   - (RAM)

External to the microprocessor, we see two different memory blocks. The firmware, or program store, contains the application code, and the data store contains data that are being manipulated, sent to, or brought in from the external world. In the embedded world, we refer to the application code as firmware because it is generally stored in a Read Only Memory (ROM), rather than on a hard drive as one might do for a desktop application. The data memory is usually made up of Random Access Memory (RAM).

> > Caution: The two separate pieces of memory do not change the architecture from von Neumann to Harvard unless two separate buses are connecting them to the processor.