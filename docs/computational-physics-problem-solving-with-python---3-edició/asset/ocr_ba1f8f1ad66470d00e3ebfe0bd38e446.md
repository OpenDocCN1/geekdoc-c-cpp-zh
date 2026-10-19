As the simplest example, it makes little sense to have a CPU of incredibly high speed coupled to a memory system and software that cannot keep up with it.

# 10.2

# Memory Hierarchy

An idealized model of computer architecture is a CPU sequentially executing a stream of instructions and reading from a continuous block of memory. To illustrate, in Figure 10.1 we have a vector A[ ] and an array M[., . ] loaded in memory and about to be processed. The real world is more complicated than this. First, arrays are not stored in 2D blocks, but rather in the linear order. For instance, in Python, Java, and C it is in row-major order:

```
M(0, 0) M(0, 1) M(0, 2) M(1, 0) M(1, 1) M(1, 2) M(2, 0) M(2, 1) M(2, 2) .
```

(10.1)

In Fortran, it is in column-major order:

```
M(1, 1) M(2, 1) M(3, 1) M(1, 2) M(2, 2) M(3, 2) M(1, 3) M(2, 3) M(3, 3) .
```

(10.2)

Second, as illustrated in Figures 10.2 and 10.3, the values for the matrix elements may not even be in the same physical place. Some may be in RAM, some on the disk, some in cache, and some in the CPU. To give these words more meaning, in Figures 10.3 and 10.2 we show simple models of the memory architecture of a high-performance computer. This hierarchical arrangement arises from an effort to balance speed and cost, with fast, expensive memory supplemented by slow, less expensive memory. The memory architecture may include the following elements:

CPU Central processing unit, the fastest part of the computer. The CPU consists of a number of very high-speed memory units called registers containing the instructions sent to the hardware to do things like fetch, store, and operate on data. There are usually separate registers for instructions, addresses, and operands (current data). In many cases, the CPU also contains some specialized parts for accelerating the processing of floating-point numbers.

Cache A small, very fast bit of memory that holds instructions, addresses, and data in their passage between the very fast CPU registers and the slower RAM (also called a high-speed buffer). This is seen in the next level down the pyramid in Figure 10.2. The main memory is also called dynamic RAM (DRAM), while the cache is called static RAM (SRAM). If the cache is used properly, it can greatly reduce the time that the CPU waits for data to be fetched from memory.

Cache lines The data transferred to and from the cache or CPU are grouped into cache or data lines. The time it takes to bring data from memory into the cache is called latency.