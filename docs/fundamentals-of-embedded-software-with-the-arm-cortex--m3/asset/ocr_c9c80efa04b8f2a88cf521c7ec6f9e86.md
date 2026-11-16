![](bbox=[0.16, 0.09, 0.92, 0.27])

| Bits | Name | Description |
|---|---|---|
| 31 | N | Negative (or less than) |
| 30 | Z | Zero (or Equal) |
| 29 | C | Carry or Borrow Out |
| 28 | V | Overflow (2's complement) |
| 27 | Q | Sticky Saturation Flag |

FIGURE 5-12 Bit fields within the Program Status Register.

that (from address PC-4) is executed. Note that the PC holds the address of the instruction currently being fetched, not the one being executed. By overlapping these operations, instructions can be executed at the rate of one every clock cycle rather than one every three clock cycles (Figures 5-13 and 5-14).

When a branch instruction is executed, the other two instructions in the pipeline must be discarded and the pipeline refilled. To accelerate the process, the processor fetches the destination instruction during the decode stage. For conditional branch instructions, the branch decision is determined during the execute stage. If the branch decision fails, then the next sequential instruction already in the pipeline is executed.

![](bbox=[0.26, 0.67, 0.81, 0.9])

FIGURE 5-13 Cortex-M3 instruction pipeline.