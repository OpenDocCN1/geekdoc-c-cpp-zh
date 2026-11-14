# 4.5.1 Write Operation

A value is written into the cell by applying a signal to b<sub>i</sub> and <o>b<sub>i</sub></o> through the write/sense amplifiers. Asserting the word line causes the new value to be written into the latch.

# 4.5.2 Read Operation

A value is read from the cell by first pre-charging b<sub>i</sub> and <o>b<sub>i</sub></o> to a voltage that is halfway between a 0 and a 1. Asserting the word line drives b<sub>i</sub> and <o>b<sub>i</sub></o> to high and low and high depending on the value that has been stored. The values are sensed and amplified by the write/sense amplifier. Typical timing for a read and a write operation is shown in Figure 4.6.

# 4.6 DYNAMIC RAM OVERVIEW

A typical cell in a DRAM array appears as illustrated in Figure 4.7. Observe that in contrast to the configuration of the SRAM cell, in the DRAM, there is only one transistor per cell. The read and write operations use a single bit line.

![](bbox=[0.27, 0.42, 0.86, 0.82])

Figure 4.7 The DRAM Inside