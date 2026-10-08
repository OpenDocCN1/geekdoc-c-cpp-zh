
Each SM has a set of 32-bit registers stored in a register file that are partitioned among threads, and a fixed amount of shared memory that is partitioned among thread blocks. The number of thread blocks and warps that can simultaneously reside on an SM for a given kernel depends on the number of registers and amount of shared memory available on the SM and required by the kernel.

Figure 3-13 illustrates that when a thread consumes more registers, fewer warps can be placed on an SM. If you can reduce the number of registers a kernel consumes, more warps will be processed simultaneously. Figure 3-14 illustrates that when a thread block consumes more shared memory, fewer thread blocks are processed simultaneously by an SM. If you can reduce the amount of shared memory used by each thread block, then more thread blocks can be processed simultaneously.

![](img/506ba3a4c9f4512233692f3f20de1f3a_115_0.png)
FIGURE 3-13

![](img/506ba3a4c9f4512233692f3f20de1f3a_115_1.png)
FIGURE 3-14

Resource availability generally limits the number of resident thread blocks per SM. The number of registers and the amount of shared memory per SM vary for devices of different compute capability. If there are insufficient registers or shared memory on each SM to process at least one block, the kernel launch will fail. Some of the key limits are shown in Table 3-2.

## TABLE 3-2: Resource Limits Pertaining to Compute Capability

| TECHNICAL SPECIFICATIONS | COMPUTE CAPABILITY (2.0) | 2.1 | 3.0 | 3.5 |
| --- | --- | --- | --- | --- |
| Maximum number of threads per block | | 1,024 | | |
| Maximum number of concurrent blocks per multiprocessor | | 8 | | 16 | |
| Maximum number of concurrent warps per multiprocessor | | 48 | | 64 | |
| Maximum number of concurrent threads per multiprocessor | | 1,536 | | 2,048 | |
| Number of 32-bit registers per multiprocessor | | 32 K | | 64 K | |
| Maximum number of 32-bit registers per thread | | 63 | | 255 | |
| Maximum amount of shared memory per multiprocessor | | 48 K | | |

A thread block is called *active* when compute resources, such as registers and shared memory, have been allocated to it. The warps it contains are called *active warps*. Active warps can be further classified into three types:

- Selected warp
- Stalled warp
- Eligible warp

The warp schedulers on an SM select active warps every cycle and dispatch them to execution units. A warp that is actively executing is called a *selected warp*. If an active warp is ready for execution but not currently executing, it is an *eligible warp*. If a warp is not ready for execution, it is a *stalled warp*. A warp is eligible for execution if both of the following conditions are met:

- Thirty-two CUDA cores are available for execution.
- All arguments to the current instruction are ready.

For example, the number of active warps on an SM at any time must be less than or equal to the architecture limit of 64 warps. The number of selected warps at any cycle is less than or equal to 4. If a warp stalls, the scheduler picks up an eligible warp in its place. Because compute resources are partitioned among warps and kept during the entire lifetime of a warp, switching contexts is fast. Compute resource partitioning requires special attention in CUDA programming: compute resources limit the number of active warps. Therefore, you must be aware of the restrictions imposed by the hardware and the resources used by your kernel. To maximize GPU utilization, you need to maximize the number of active warps.

## Latency Hiding

An SM relies on thread-level parallelism to maximize utilization of functional units. Utilization is therefore directly linked to the number of resident warps. The number of clock cycles between an instruction being issued and completed is defined as instruction latency. Full resource utilization is achieved when warp schedulers have an eligible warp every cycle. This ensures that the latency of each instruction can be hidden by issuing other instructions.

Compared with CPU programming, latency hiding is particularly important in CUDA programming. GPU cores are designed for one or two threads at a time, whereas GPUs are designed to handle a large number of concurrent threads in order to maximize throughput. GPU instruction latency is hidden by other warps.

When considering instruction latency, instructions can be classified into two basic types:

- Arithmetic instructions
- Memory instructions

Arithmetic latency is the time between an arithmetic operation starting and its output being produced. Memory latency is the time between a load or store operation being issued and the data arriving at its destination. The corresponding latencies for each case are approximately:

- 10-20 cycles for arithmetic operations
- 400-800 cycles for global memory accesses

Figure 3-15 illustrates a simple pipeline in which warp 0 stalls. The scheduler picks other warps to execute and executes warp 0 when it is eligible. ![](img/506ba3a4c9f4512233692f3f20de1f3a_117_0.png)
FIGURE 3-15

You may wonder how to estimate the number of active warps required to hide latency. Little's Law provides a reasonable approximation that can be applied to GPUs:

> Number of Required Warps = Latency × Throughput

Figure 3-16 illustrates Little's Law visually. Suppose the average latency for an instruction in a kernel is 5 cycles. To keep a throughput of 6 warps executed per cycle, you will need at least 30 warps in flight.![](img/506ba3a4c9f4512233692f3f20de1f3a_118_0.png)
FIGURE 3-16

## Throughput AND Bandwidth

Bandwidth and throughput are often confused, but may be used interchangeably depending on the situation. Both throughput and bandwidth are rate metrics used to measure performance. Bandwidth is usually used to refer to a theoretical peak value, while throughput is used to refer to an achieved value. Bandwidth describes the highest possible amount of data transfer per time unit, while throughput describes the rate of any kind of information or operations carried out per time unit, such as how many instructions are completed per cycle.

For arithmetic operations, the required parallelism can be expressed to hide arithmetic latency. Table 3-3 lists the number of required operations for Fermi and Kepler devices. The arithmetic operation used here is a 32-bit floating-point multiply-add ($a + b \times c$), expressed as the number of operations per clock cycle per SM. The throughput varies for different instructions.

## TABLE 3-3: SM Parallelism Required to Maintain Arithmetic Utilization

| GPU MODEL | INSTRUCTION LATENCY (CYCLES) | THROUGHPUT (OPERATIONS/CYCLE) | PARALLELISM (OPERATIONS) |
| --- | --- | --- | --- |
| Fermi | 20 | 32 | 640 |
| Kepler | 192 | | 3840 |

Throughput is specified in number of operations per cycle per SM, and a warp executing one instruction corresponds to 32 operations. Therefore, the required number of warps per SM to maintain full resource utilization can be calculated for Fermi GPUs as 640 ÷ 32 = 20 warps. Hence, the required parallelism for arithmetic operations can be expressed as either the number of operations or the number of warps. This simple conversion demonstrates that there are two ways to increase parallelism:

- Instruction-level parallelism (ILP): More independent instructions within a thread
- Thread-level parallelism (TLP): More concurrently eligible threads

For memory operations, the required parallelism is expressed as the number of bytes per cycle required to hide memory latency. Table 3-4 lists the metrics for the Fermi and Kepler architectures.

## TABLE 3-4: Device Parallelism Required to Maintain Memory Utilization

| GPU MODEL | INSTRUCTION LATENCY (CYCLES) | BANDWIDTH (GB/SEC) | BANDWIDTH (B/CYCLE) | PARALLELISM (KB) |
| --- | --- | --- | --- | --- |
| Fermi | 800 | 144 | 92 | 74 |
| Kepler | 800 | 250 | 96 | 77 |

Because memory throughput is usually expressed as gigabytes per second, you need to convert the throughput into gigabytes per cycle using the corresponding frequency. You can check your device's memory frequency with the following:

```bash
$ nvidia-smi -a -q CLOCK | grep -A 3 "Max Clocks" | grep "Memory"
```

A Fermi memory frequency (measured on a Tesla C200) is 1.566 GHz. A Kepler memory frequency (measured on a Tesla K20) is 1.6 GHz. Because 1 Hz is defined as one cycle per second, you can then convert the bandwidth from gigabytes per second to gigabytes per cycle as follows:

144 GB/Sec / 1.566 GHz ≈ 92 Bytes/Cycle

Multiplying bytes per cycle by memory latency, you derive the required parallelism for Fermi memory operations at nearly 74 KB of memory I/O in flight to achieve full utilization. This value is for the entire device, not SM, because memory bandwidth is given for the entire device.
