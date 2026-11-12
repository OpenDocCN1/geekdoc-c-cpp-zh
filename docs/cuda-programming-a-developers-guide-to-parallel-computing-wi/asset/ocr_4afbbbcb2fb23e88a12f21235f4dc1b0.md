As you can see all we do is replace the OpenMP directive with an OpenACC directive. We then compile with the vendor-supplied OpenACC compiler. This may generate anything from high-level CUDA code to raw PTX code. It will then usually invoke the NVCC compiler to generate the target GPU code. Some vendors support additional targets other than simply NVIDIA GPUs.

During the compilation stage most vendors' compilers provide statistics about how they are transforming the serial code to device code. However, this is a little like the -v option in NCC, in that you need to be able to understand what the compiler is telling you. We look here at an example of the PGI compiler output.

```
Accelerator kernel generated
60, #pragma acc loop gang, vector /* blockIdx.x threadIdx.x */
CC 1.3 : 21 registers; 1024 shared, 20 constant, 0 local memory bytes; 100% occupancy
CC 2.0 : 23 registers; 1048 shared, 40 constant, 0 local memory bytes; 100% occupancy
```

To understand this output, you need to understand how the OpenACC terminology maps onto CUDA terminology (Table 10.6).

The first line states that the kernel occupied 60 gangs (blocks in CUDA terminology). It then states it generated output for “CC 1.3 and CC 2.0,” compute capacity 1.3 and 2.0 devices, respectively. It also tells you the number of registers used, the number of shared memory per block used, the number of bytes of constant memory per block, and any registers spilled to local memory.

Finally, it calculates the ideal number of threads (OpenACC calls these vectors) to achieve near 100% occupancy as possible based on the number of registers and shared memory the kernel is using. It may, however, not always select the best values for a given kernel/data pattern. Specifying this allows us to override or partially override such choices.

It will look at your data and decide on the best launch parameters (number of threads, number of blocks, number of grids, etc.). It will also automatically try to allocate data to constant and/or global memory. You are free to override these selections if you wish.

To override the default behavior of mirroring global data on the host (automatic background update commands), you need to specify how the data must be managed. This can be done as follows:

```
#pragma acc data <directives>
```

where <directives> can be one of the following plus some additional more complex ones not shown here:

+   - copy (data1, data2, ...)—Maintain an identical CPU version by copying in at the start of the kernel and out at the end (the default behavior).
+   - copyin (data1, data2, ...)—Only copy data to the GPU and do not copy it back, that is, discard the GPU data. This is useful for read-only data the GPU will process.

| OpenACC | CUDA |
|---|---|
| Gangs | Blocks |
| Workers | Warps |
| Vectors | Threads |