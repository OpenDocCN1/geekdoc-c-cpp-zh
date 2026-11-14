

![](img/679b8d2d47f1bf86e17aca48f596f5cc_231_0.png)

The three-to-one-of-eight encoder converts the incoming address patterns into the equivalent in index numbers. The read and write signals perform the associated operations. Prior to writing, the output drivers for the memory must be placed into the high-impedance state so that there is no conflict with the incoming data words. For this simple model, the data is entered into or read from the memory as a 16-bit word.

**address, data, control** Thus, we see that a memory interface generally requires three categories of signals: address, data, and control. Address signals are inputs to the memory, data can be either an input or an output, and the control signals are generally inputs. All of the different memory types require both address and data signals. They differ in the number and the nature of the necessary control signals.

In Table 4.1, we identify some of the more common control signals.

| | Chip Select (CS) | Output Enable (OE) | Read (R) | Write (W) | Column Address Strobe (CAS) | Row Address Strobe (RAS) |
|---|---|---|---|---|---|---|
| ROM | X | X | | | | |
| SRAM | X | X | X | X | | |
| DRAM | X | X | X | X | X | X |

- Chip Select (CS) – Enables a memory device for reading or writing. Generally low true.
- Output Enable (OE) – Memory device output tristate control. Generally low true.
- Read (R) – Signify a read operation on the memory device.
- Write (W) – Signify a write operation on the memory device.
- Column Address Strobe (CAS) – Signify that the signals on the address inputs represent a column address for the memory device.
- Row Address Strobe (RAS) – Signify that the signals on the address inputs represent a row address for the memory device.

## 4.4 ROM OVERVIEW

Although there are exceptions, the ROM is generally viewed as a read only device. A high-level interface to the ROM given in Figure 4.3. Moving inside the ROM, we find that the adjacent diagram illustrates several bits in a ROM fragment. When the ROM is implemented, positions in the array that are to store a logical 0 have a transistor connected as shown in the figure. Those positions intended to store a logical 1 have none.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_232_0.png)

Figure 4.3 The ROM – Outside and Inside

### 4.4.1 Read Operation

A value is read from a ROM by asserting one of the row lines. Those rows in which there is a transistor will be pulled to ground, thereby expressing a logical 0. Those without the transistor will express a logical 1.

Typical timing for a ROM read operation is given in Figure 4.4.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_232_1.png)

Figure 4.4 The ROM – Read Operation Timing

## 4.5 STATIC RAM OVERVIEW

A high-level interface to the SRAM is very similar to that for the ROM. The major differences arise from support for write capability. Figure 4.5 presents the major I/O signals and a typical cell in an SRAM array.

Observe that there are six transistors per cell (two in each of the buffers and the two pull-up transistors); two access transistors enable the cell for read and write.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_233_0.png)

Figure 4.5 The SRAM – Outside and Inside

![](img/679b8d2d47f1bf86e17aca48f596f5cc_233_1.png)

![](img/679b8d2d47f1bf86e17aca48f596f5cc_233_2.png)

Figure 4.6 Timing for the SRAM – Read and Write Operations

### 4.5.1 Write Operation

A value is written into the cell by applying a signal to b<sub>i</sub> and <o>b<sub>i</sub></o> through the write/sense amplifiers. Asserting the word line causes the new value to be written into the latch.

### 4.5.2 Read Operation

A value is read from the cell by first pre-charging b<sub>i</sub> and <o>b<sub>i</sub></o> to a voltage that is halfway between a 0 and a 1. Asserting the word line drives b<sub>i</sub> and <o>b<sub>i</sub></o> to high and low and high depending on the value that has been stored. The values are sensed and amplified by the write/sense amplifier. Typical timing for a read and a write operation is shown in Figure 4.6.

## 4.6 DYNAMIC RAM OVERVIEW

A typical cell in a DRAM array appears as illustrated in Figure 4.7. Observe that in contrast to the configuration of the SRAM cell, in the DRAM, there is only one transistor per cell. The read and write operations use a single bit line.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_234_0.png)

Figure 4.7 The DRAM Inside

### 4.6.1 Read Operation

A value is read from the cell by first pre-charging b<sub>1</sub> to a voltage that is halfway between a 0 and a 1. Asserting the word line enables the stored signal onto b<sub>1</sub>. If the stored value is a logical 1, through charge sharing, the value on line b<sub>1</sub> will increase. Conversely, if the stored value is a logical 0, charge sharing will cause the value on b<sub>1</sub> to decrease. The change in value is sensed and amplified by the write/sense amplifier. The read operation causes the capacitor to discharge. The sensed and amplified value is placed back on to the bit line. This is called a restore or rewrite operation.

*restore, rewrite*

### 4.6.2 Write Operation

A value is written into the cell by applying a logical 0 or logical 1 to b<sub>1</sub> through the write/sense amplifiers. Asserting the word line charges the capacitor if a logical 1 is to be stored and discharges it if a logical 0 is to be stored.

### 4.6.3 Refresh Operation

Dynamic memories only store data for short periods of time on the parasitic capacitor associated with a MOS transistor. If the charge stored on the capacitor is not replaced periodically, it will leak away, thereby losing the data stored in the memory. Replacement is implemented by executing a read operation followed by a rewrite of the data back into the cell. Such replacement is referred to as refresh or a refresh cycle. The time between two refresh operations is called the refresh time interval. The interval is determined by the vendor's specification and the system in which memory is operating. A high-level interface to the DRAM is given in Figure 4.8.

*refresh, refresh cycle refresh time interval*

![](img/679b8d2d47f1bf86e17aca48f596f5cc_235_0.png)

Figure 4.8 The DRAM Outside

**Column Address Strobe Row Address Strobe** CAS or Column Address Strobe is a clock used in dynamic memories to control the input of column addresses to the memory. RAS or Row Address Strobe is a clock used in dynamic memories to control the input of row addresses to the memory.

Typical DRAM read and write timing is given in Figure 4.9.

### DRAM Read

![](img/679b8d2d47f1bf86e17aca48f596f5cc_236_0.png)

### DRAM Write

![](img/679b8d2d47f1bf86e17aca48f596f5cc_236_1.png)

Figure 4.9 Timing for the DRAM Read and Write Cycles

## 4.7 CHIP ORGANIZATION

Independent of type of internal storage, the typical memory chip appears as is shown in Figure 4.10.

## 4.8 TERMINOLOGY

Prior to delving into the detailed design and application of memory systems, it is appropriate to introduce some of the vocabulary.

**Access time.** The time to access a word in memory.

Access time specifies to perform a read or a write operation. Note that the times for these two operations may be different. The time is measured from the point at which the access commences (as defined by the application of the address) until the operation is complete. For a read operation, that time will be when the data appears at the output port of the device. For a write operation, that time will be when the data is successfully written into the memory.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_237_0.png)

Figure 4.10 Typical Memory Chip Internal Architecture

In the timing diagram for the write operation in Figure 4.11, it is assumed that the internal write process commences on the transition from high to low on the write line and completes sometime later.

**write**

The read and write operations are illustrated in the timing diagram in Figure 4.11.

**Cycle time.** The time interval from the start of one read or write operation until the start of the next. Cycle time is a measure of how quickly the memory can be repeatedly accessed. It is illustrated in the timing diagram in Figure 4.12.

**logical** Block size. A block is a logical view placed on a collection of words in memory.

**blocks** When quantities of data are transferred within a system, the units of transfer are called blocks. The block size specifies the number of words in such a collection. Figure 4.13 illustrates a memory organized into blocks.

**Bandwidth.** Memory bandwidth is a measure of the word transmission rate to and from memory via the memory I/O bus.

