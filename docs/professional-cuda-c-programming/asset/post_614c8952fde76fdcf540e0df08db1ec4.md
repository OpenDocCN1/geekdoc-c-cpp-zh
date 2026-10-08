
Recompile the code with L1 cache enabled, and run the following commands to compare performance between the two transpose kernels. The results measured on a Fermi M2090 are summarized in Table 4-9.

```
$ ./transpose 4
$ ./transpose 5
```

# TABLE 4-9: Effective Bandwidth of Kernels (L1 Cache Enabled)

| KERNEL | BANDWIDTH | RATIO TO PEAK BANDWIDTH |
|---|---|--|
| Unroll4Row: Load rows/store columns | 44.15 GB/s | 24.85% |
| Unroll4Col: Load columns/store rows | 90.20 GB/s | 50.76% |

Block size: 16 x 16; Matrix size: 2,048 x 2,048; Unit of Effective Bandwidth: GB/sec

Again, with L1 cache enable, loading columns and storing rows yields better effective bandwidth and overall execution time.

# Diagonal Transpose: Reading Rows versus Columns

When you launch a grid of thread blocks, the thread blocks are distributed among SMs. While programming model abstractions may present grid to you in a 1D or 2D layout, the perspective all blocks are arranged one-dimensionally. Each block has its own unique identifier, bid, which is calculated using a row-major ordering of thread blocks in a grid:

```
int bid = blockIdx.x * gridDim.x + blockIdx.y;
```

Figure-47 illustrates a sample example of a 4 x 4 grid of thread blocks and the corresponding block ID of each thread block.

Cartesian coordinate | Corresponding block ID

FIGURE 4-27

When a kernel is launched, the order in which thread blocks are assigned to SMs is determined by the block ID. Once all SMs are at full occupancy, any remaining thread blocks are held until currently executing ones. Once a thread block completes, another thread block is assigned to that SM. Because the speed and order in which thread blocks complete is not deterministic, active thread blocks are initially contiguous but become less contiguous over time as execution of the kernel progresses.

Although you do not have direct control over how the block coordinates are scheduled, you can be flexible in how you interpret the block coordinates blockId.x and blockId.y. Figure 4-27 illustrated block coordinates corresponding to the Cartesian coordinate system. Figure 4-28 illustrates a different way of interpreting blockId.x and blockId.y: using a diagonal block coordinate system.

# Diagonal coordinate

# Corresponding block ID

| | | | | |
|---|---|---|--|
| (0,0) | (0,1) | (0,2) | (0,3) |
| 0 | 4 | 8 | 12 |
| (1,3) | (1,0) | (1,1) | (1,2) |
| 13 | 1 | 5 | 9 |
| (2,2) | (2,3) | (2,0) | (2,1) |
| 10 | 14 | 2 | 6 |
| (3,1) | (3,2) | (3,3) | (3,0) |
| 7 | 11 | 15 | 3 |

FIGURE 4-28

The diagonal coordinate system is used to determine thread block ID. However, for data access, y still need to use the Cartesian coordinate system. Therefore, interpreting block IDs as diagonal coordinates, you need to map from diagonal coordinates to Cartesian coordinates so that you can access the correct data block. For a square matrix, this mapping can be calculated with the following equation:

```
block_x = (blockId.x + blockId.y) % gridDim.x;
block_y = blockId.x;
```

Here, blockId.x and blockId.y are interpreted as diagonal coordinates. block_x and block_y are their corresponding Cartesian coordinates. The row-based matrix transpose kernel uses diagonal coordinates as follows. At the beginning of the kernel, then calculate thread index (ix, iy) using mapped Cartesian coordinates assigned to thread blocks. The example kernel below uses diagonal block coordinates to implement the transpose with coalesced reads and writes:

```
__global void transposeDiagonalRow(float *out, float *in, const int nx, int ny) {
  unsigned int block_x = blockId.x;
  unsigned int block_y = (blockId.x+blockId.y)%gridDim.x;

  unsigned int ix = gridDim.x * block_x + threadIdx.x;
  unsigned int iy = blockDim.y * block_y + threadIdx.y;

  if (ix < nx && iy < ny) {
    out[ix*ny + iy] = in[iy*nx + ix];
  }
}
```

The column-based version that uses diagonal coordinates is below:

```cpp
__global void transposeDiagonalCol(float *out, float *in, const int nx, const int ny) {
    unsigned int blk_y = blockIdx.x;
    unsigned int blk_x = [blockIdx.x+blockIdx.y]%gridDim.x;

    unsigned int ix = blockDim.x * blk_x + threadIdx.x;
    unsigned int iy = blockDim.y * blk_y + threadIdx.y;

    if (ix < nx && iy < ny) {
        out[iy*nx + ix] = in[ix*ny + iy];
    }
}
```

Add the following code into the kernel switch statement to handle these kernels:

```
case 6:
    kernel = &transposeDiagonalRow;
    kernelName = "DiagonalRow";
    break;

case 7:
    kernel = &transposeDiagonalCol;
    kernelName = "DiagonalCol";
    break;
```

Recompile the code with L1 cache enabled and run the following commands to compare performance between the two new transpose kernels. The results are summarized in Table 4-10.

```
$ ./transpose 6
$ ./transpose 7
```

# TABLE 4-10: Effective Bandwidth of Kernels (L1 Cache Enabled)

| KERNEL | BANDWIDTH | RATIO TO PEAK BANDWIDTH |
|---|---|--|
| DiagonalRow: Load rows/store columns | 73.42 GB/s | 41.32% |
| DiagonalCol: Load columns/store rows | 75.92 GB/s | 42.72% |

Block size: 16x16; Matrix: 2,048 x 2,048; Unit of Effective Bandwidth: GB/sec

By altering the block execution order using diagonal coordinates, the performance achieved by the row-based kernel improves considerably. However, the column-based kernel still performs better with Cartesian block coordinates than diagonal block coordinates. The diagonal kernel implementation could be further improved by unrolling blocks, but that implementation is not as straightforward as it was with the Cartesian-based kernel.

The reason for this performance improvement is related to the parallel access of DRAM. Successive 256-byte regions of device memory are assigned to successive partitions. When using Cartesian coordinates to map thread blocks to data blocks, global memory accesses may not be evenly distributed among DRAM partitions, and a phenomenon called partition camping may occur. In partition camping, memory requests are queued while other partitions remain unused. Because the diagonal coordinate mapping causes non-linear mappings from thread blocks to the data blocks they process, strided accesses are unlikely to fall into a single partition, and performance improves as a result.

For best performance, concurrent access to global memory by all active shards should be divided among partitions. Figure 4-29 illustrates partition camping when Cartesian coordinates are used. In this figure, suppose you have only two partitions, which helps visualize partition camping. Figure 4-30 shows how diagonal coordinate mapping avoids this.

# Expose More Parallelism with Thin Blocks

The simplest way to expose more parallelism is to adjust block size. Previous sections have already demonstrated the effectiveness of this technique for improving performance. Sample results of exhaustive block size are summarized in Table 4-11.

# TABLE 4-11: Effective Bandwidth of Kernels (L1 Disabled)

| KERNEL | BLOCK SIZE | BANDWIDTH |
| --- | --- | --- |
| NaiveCol | (32, 32) | 38.13 GB/s |
| NaiveCol | (32, 16) | 51.46 GB/s |
| NaiveCol | (32, 8) | 54.82 GB/s |
| NaiveCol | (16, 32) | 73.42 GB/s |
| NaiveCol | (16, 16) | 80.27 GB/s |
| NaiveCol | (16, 8) | 70.34 GB/s |
| NaiveCol | (8, 32) | 102.76 GB/s |
| NaiveCol | (8, 16) | 82.64 GB/s |
| NaiveCol | (8, 8) | 59.59 GB/s |

Matrix size: 2,048 x 2,048; Unit of Effective Bandwidth: GB/sec: Kernel the naive implementation that loads columns and rows

The optimal block size by far was (8, 32), even though it exposes some parallelism as (16, 16). This performance improvement is caused by the "thin" block dimensions of (8, 32), as shown in Figure 4-31.

A "thin" block improves the effectiveness of store operations (shown in Table 4-12) by increasing the number of elements stored by a thread block as a result of a larger value in the innermost dimension of the block. You can confirm this by using nvprof to measure the load and store throughput metrics.

TABLE 4-12: Effective Bandwidth of Kernels (L1 Cache Enabled)

| EXECUTION CONFIGURATION | LOAD THROUGHPUT | STORE THROUGHPUT |
| --- | --- | --- |
| (16, 16) | 660.89 GB/s | 41.11 GB/s |
| (8, 32) | 406.43 GB/s | 50.80 GB/s |
