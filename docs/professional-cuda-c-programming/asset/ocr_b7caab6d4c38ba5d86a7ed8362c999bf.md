# Understanding the Nature of Warp Execution

Total number of registers available per block: 32768
Maximum number of threads per block: 1024
Maximum number of threads per multiprocessor: 1536
Maximum number of warps per multiprocessor: 48

The CUDA Toolkit includes a spreadsheet, CUDA Occupancy Calculator, which assists you in selecting grid and block dimensions to maximize occupancy for a kernel. Figure 3-17 shows a screenshot of the Occupancy Calculator.

![](bbox=[0.148, 0.246, 0.941, 0.715])



+   - Select active sms (1, 2, and 3 or click here below)
- Select Compute Capability (3.0)
- Select Shared Memory Size (Bytes) (912)
- Choose your usage:
  - Threads Per Block
  - Warps Per Block
  - Registers Per Thread
  - Blocks Per Block
  - (Don't edit anything below this line)
- 15.0 CUDA Occupancy is displayed and in here:
- Active Threads per Multiprocessor
- Active Warps per Multiprocessor
- Occupancy of each Multiprocessor
- Physical Limits for GPU Capacity:
- Warps per Multiprocessor
- Threads per Multiprocessor
- Blocks per Multiprocessor
- Total registers and size
- Register utilization and size
- Shared memory per multiprocessor
- Shared memory per unit
- Warp allocation granularity
- Allocated Memory
- (Threads per Block / Threads per Warp)
- Shared memory (Bytes,)
- Maximum Warps or Blocks Per Multiprocessor
- Limited by Warps or Blocks per Multiprocessor
- CUDA Occupancy Calculator Results
- Version

| | Per Block | Limit Per SM | Blocks Per SM |
|---|---|---|---|
| Warps | 32 | 48 | 32 |
| Shared memory (Bytes,) | 912 | 65536 | 72 |
| Blocks | 16 | 32 | 48 |

![](bbox=[0.573, 0.269, 0.941, 0.706])

FIGURE 3-17

There are several sections in the Occupancy Calculator. First, you must provide information about your GPU's compute capacity and your kernel's resource usage.