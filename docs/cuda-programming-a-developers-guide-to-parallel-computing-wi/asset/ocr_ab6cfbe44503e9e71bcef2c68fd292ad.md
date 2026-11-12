| Thread 0-15, Block 0 | Thread 16-31, Block 0 |
| Thread 32-47, Block 0 | Thread 48-63, Block 0 |
| Thread 64-79, Block 0 | Thread 80-95, Block 0 |
| Thread 96-111, Block 0 | Thread 112-127, Block 0 |
| Thread 0-15, Block 1 | Thread 16-31, Block 1 |
| Thread 32-47, Block 1 | Thread 48-63, Block 1 |
| Thread 64-79, Block 1 | Thread 80-95, Block 1 |
| Thread 96-111, Block 1 | Thread 112-127, Block 1 |
| Thread 0-15, Block 2 | Thread 16-31, Block 2 |
| Thread 32-47, Block 2 | Thread 48-63, Block 2 |
| Thread 64-79, Block 2 | Thread 80-95, Block 3 |
| Thread 96-111, Block 3 | Thread 112-127, Block 3 |
| Thread 0-15, Block 4 | Thread 16-31, Block 4 |
| Thread 32-47, Block 4 | Thread 48-63, Block 4 |
| Thread 64-79, Block 4 | Thread 80-95, Block 4 |
| Thread 96-111, Block 4 | Thread 112-127, Block 4 |

| Thread 0-15, Block 0 | Thread 0-15, Block 1 |
| Thread 16-31, Block 0 | Thread 16-31, Block 1 |
| Thread 32-47, Block 0 | Thread 32-47, Block 1 |
| Thread 48-63, Block 0 | Thread 48-63, Block 1 |
| Thread 64-79, Block 0 | Thread 64-79, Block 1 |
| Thread 80-95, Block 0 | Thread 80-95, Block 1 |
| Thread 96-111, Block 0 | Thread 96-111, Block 1 |
| Thread 112-127, Block 0 | Thread 112-127, Block 1 |
| Thread 0-15, Block 2 | Thread 0-15, Block 4 |
| Thread 16-31, Block 2 | Thread 16-31, Block 4 |
| Thread 32-47, Block 2 | Thread 32-47, Block 4 |
| Thread 48-63, Block 3 | Thread 48-63, Block 4 |
| Thread 64-79, Block 3 | Thread 64-79, Block 4 |
| Thread 80-95, Block 3 | Thread 80-95, Block 4 |
| Thread 96-111, Block 3 | Thread 96-111, Block 4 |
| Thread 112-127, Block 3 | Thread 112-127, Block 4 |

FIGURE 5.11 Alternative thread block layouts.

```
dim3 threads_square(16,8);
dim3 blocks_square(2,2);
```

In either arrangement you have the same total number of threads (32 x 4 = 128, 16 x 8 = 128). It's simply the layout of the threads that is different.

The dim3 type is simply a special CUDA type that you have to use to create a 2D layout of threads. In the rectangle example, you're saying you want 32 threads along the X axis by 4 threads along the Y axis, within a single block. You're then saying you want the blocks to be laid out as one block wide by four blocks high. You'll need to invoke the kernel with

```
some_kernel_func<<< blocks_rect, threads_rect >>>(a, b, c);
```

or

```
some_kernel_func<<< blocks_square, threads_square >>>(a, b, c);
```

As you no longer want just a single thread ID, but an X and Y position, you'll need to update the kernel to reflect this. However, you also need to linearize the thread ID because there are situations where you may want an absolute thread index. For this we need to introduce a couple of new concepts, shown in Figure 5.12.

You can see a number of new parameters, which are:

```
gridDim.x-The size in blocks of the X dimension of the grid.
gridDim.y-The size in blocks of the Y dimension of the grid.
blockDim.x-The size in threads of the X dimension of a single block.
blockDim.y-The size in threads of the Y dimension of a single block.
```