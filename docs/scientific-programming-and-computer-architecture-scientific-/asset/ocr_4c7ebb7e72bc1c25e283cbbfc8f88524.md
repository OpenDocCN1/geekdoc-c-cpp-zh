# Contents

+   3.2.7 A little compiler theory . . . . . . . . . . . . . . . . . . . . . . . . 180
3.3 Optimizing for the instruction pipeline . . . . . . . . . . . . . . . . . . . . . 186
3.3.1 Instruction pipelines . . . . . . . . . . . . . . . . . . . . . . . . . . . 188
3.3.2 Chipsets . . . . . . . . . . . . . . . . . . . . . . . . . . . . 193
3.3.3 Peak floating point performance . . . . . . . . . . . . . . . . 196
3.3.4 Microkernel for matrix multiplication . . . . . . . . 209
3.4 References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 219

+   4 Memory . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 221
4.1 DRAM and cache memory . . . . . . . . . . . . . . . . . . . . . . . 224
4.1.1 DRAM memory . . . . . . . . . . . . . . . . . . . . . . . . . 226
4.1.2 Cache memory . . . . . . . . . . . . . . . . . . . . . . . . . 230
4.1.3 Physical memory and virtual memory . . . . . . . . . . 234
4.1.4 Latency to DRAM memory: First attempts . . . . . . 237
4.1.5 Latency to DRAM . . . . . . . . . . . . . . . . . . . . . . . . 241
4.2 Optimizing memory access . . . . . . . . . . . . . . . . . . 246
4.2.1 Bandwidth to DRAM . . . . . . . . . . . . . . . . . . . . . . 248
4.2.2 Matrix transpose . . . . . . . . . . . . . . . . . . . . . . . 251
4.2.3 Optimized matrix multiplication . . . . . . . . . . . 256
4.3 Reading from and writing to disk . . . . . . . . . . . 266
4.3.1 C versus C++ . . . . . . . . . . . . . . . . . . . . . . . . . . 268
4.3.2 Latency to disk . . . . . . . . . . . . . . . . . . . . . . . . . 270
4.3.3 Bandwidth to disk . . . . . . . . . . . . . . . . . . . . . . . 273
4.4 Page tables and virtual memory . . . . . . . . . . . . . . 274
4.4.1 Partitioning the virtual address space . . . . . . . . 276
4.4.2 Physical address space and page tables . . . . . . 279
4.5 References . . . . . . . . . . . . . . . . . . . . . . . . . . . . 284

+   5 Threads and Shared Memory . . . . . . . . . . . . . . . . . . 287
5.1 Introduction to OpenMP . . . . . . . . . . . . . . . . . . . . . 290
5.1.1 OpenMP syntax . . . . . . . . . . . . . . . . . . . . . . . 290
5.1.2 Shared variables and OpenMP's memory model . . . . . 297
5.1.3 Overheads of OpenMP constructs . . . . . . . . . 299
5.2 Optimizing OpenMP programs . . . . . . . . . . . . . . . 304
5.2.1 Near memory and far memory . . . . . . . . . . . . . . . 305