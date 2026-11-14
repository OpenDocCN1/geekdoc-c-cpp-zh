# 4.10 AN SRAM DESIGN

A system specification requires an SRAM system that can store up to 4 K 16-bit words. However, the largest memory device available is 1 K by 8. That is, it can store up to 1024 8-bit words. Consequently, the device will require eight of the smaller memory devices: two sets of four.

In the worst case, to support 4 K 16-bit words, 12 address lines and 16 data lines are required. If sufficient I/O lines are available on the microprocessor, the design is straightforward. Let's assume that such is not the case and that only eight address lines and eight data lines are available. Under such a restriction, two address transfers and two data transfers will be necessary to complete a single transaction. The architecture of such a system is given in Figure 4.16.

# 4.10.1 The Memory Array

*memory array* Let's look at the various pieces of the design starting with the memory array. The requirements specify support for 4K 16-bit words. The available memory chips only support 1 K 8-bit words. We can use two 1 K by 8 memory chips to hold 1 K 16-bit words.

One memory chip will store the upper byte, and the other memory chip will store the lower byte, as we see in Figure 4.15. By duplicating such a configuration four times, we will have sufficient storage for the 4 K 16-bit words.

![](bbox=[0.263, 0.462, 0.733, 0.712])

Figure 4.15 Using Two 8-Bit SRAMs to Store 16-Bit Words

chip select output enable

Ten address bits enable us to identify each location in a 1 K block since 10 bits gives us 2^10 or 1024 combinations. Next, one must be able to identify which of the 1 K by 16-bit blocks to read from or write to. Two additional address bits enable such a selection to be made. These four combinations can be used to activate the chip select (CS) control input for the appropriate 1 K block. The output enable (OE) control inputs for the individual RAMs must be placed in the logical 1 state during a write cycle and in the logical 0 state during a read cycle.