and 5.85 cycles per instruction for 10 programs in the SPEC CPU benchmark.22 The 2.66 GHz AMD Opteron of that time used fewer cycles per instruction by a factor of 1.27. As a result, the 2.66 GHz Opteron performed slightly better than the 3.2 GHz Pentium. The use of deep pipelines by the 3.2 GHz Pentium to accommodate a higher clock rate resulted in more pipeline stalls and more cycles per instruction, outweighing the advantage of greater clock speed.

For the SPEC CPU benchmark programs, the Pentium 4 did not better than 1.19 cycles per instruction, although its peak bandwidth was 1/3 of a cycle per instruction. Unsurprisingly, typical performance is useful short of the peak bandwidth. Apart from making simplifying assumptions about the instruction stream, the definition of the peak bandwidth entirely ignores the cost of memory accesses. Yet processor bandwidth is a useful metric. From 1982 to 2001, the processor bandwidth increased by a factor of 2,250. The processor performance increased by a factor close to 2,250 (an annual rate of about 50%) in the 19 years from 1982 to 2001, as measured by the SPECint.

# AVX2 and SSE pipelines

Figures 3.4 and 5 show instruction pipelines for the SSE2-capable Nehalem/Westmere microarchitecture and the AVX2-capable Haswell microarchitecture. If we want to write programs that approach MKL stalls for matrix multiplication and other tasks, such microarchitectures must be understood in some detail.

The pipelines shown have four parts. The first part, the front-end, fetches and decodes instructions. Certain instructions, mainly instructions that store in memory, may be broken up into micro-ops. The front-end can fetch and decode multiple instructions in a single cycle.

The second part, called the reorder engine, is responsible for renaming registers as well as scheduling instructions. Instructions may be scheduled for execution out of order. Predicting branches and recovering from mispredictions is also the responsibility of this part. The reorder engine includes reorder buffers. The reorder buffer holds partially complete instructions or “instructions in flight.” It corresponds roughly to renamed registers.

> 22See sections 2.10 and 1.8 of Hennessy and Patterson (1990-2011) (4th ed).