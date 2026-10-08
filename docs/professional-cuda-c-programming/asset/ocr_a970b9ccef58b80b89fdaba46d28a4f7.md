thread blocks are initially contiguous by did become less contiguous over time as execution of thenkernel progresses.

Although you do not have direct control over how the block coordinates are scheduled, you can be flexible in how you interpret the block coordinates blockId.x and blockId.y. Figure
4-27 illustrated block coordinates corresponding to the Cartesian coordinate system. Figure 4-28
illustrates a different way of interpreting blockId.x and blockId.y: using a diagonal block coord-
dinate system.

# Diagonal coordinate

# Corresponding block ID

| | | | |
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

The diagonal coordinate system is used to determine ID thread block ID. However, for data access,
y still need to use the Cartesian coordinate system. Therefore, interpreting block IDs as
diagonal coordinates, you need to map from diagonal coordinates to Cartesian coordinates so that
You can access the correct data block. For a square matrix, this mapping can be calculated with the
following equation:

```
block_x = (blockId.x + blockId.y) % gridDim.x;
block_y = blockId.x;
```

Here, blockId.x and blockId.y are interpreted as diagonal coordinates. block_x and block_y
are their corresponding Cartesian coordinates. The row-based matrix transpose kernel uses dia-
alcoordinates as follows. At the beginning of the kernel, then calculate thread index (ix, iy) using mapped Cartesian
coordinates assigned to thread blocks. The example kernel below uses diagonal block coordinates to
to implement the transpose with coalesced reads and writes:

```
__global void transposeDiagonalRow(float *out, float *in, const
int nx, int ny) {
  unsigned int block_x = blockId.x;
  unsigned int block_y = (blockId.x+blockId.y)%gridDim.x;

  unsigned int ix = gridDim.x * block_x + threadIdx.x;
  unsigned int iy = blockDim.y * block_y + threadIdx.y;

  if (ix < nx && iy < ny) {
    out[ix*ny + iy] = in[iy*nx + ix];
  }
}
```