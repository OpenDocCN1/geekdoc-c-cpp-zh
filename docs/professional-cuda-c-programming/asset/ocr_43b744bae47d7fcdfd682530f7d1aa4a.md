# CUDA Debugging

the (cuda-gdb) prompt when a memory error occurs in the kernel. The following output indicates an error occurred at line 34 of debug-segfault.cu:

```
Program received signal CUDA_EXCEPTION_10, Device Illegal Address.
(Switching focus to CUDA kernel 1026, grid 1027, block (0,0,0), thread (0,0,0),
device 0, sm 1, warp 0)
kernel<<<1024,1,1>>>(arr=0xf0010000) at debug-segfault.cu:34
25
arr[tid] = foo(tid, id);
(cuda-gdb)
```

You can use the list command to inspect the source code for context:

```
(cuda-gdb) list
28  global void kernel(int **arr) {
29      int tid = blockDim.x * threadIdx.x;
30      int i;
31
32      for (tid = tid; tid < N; tid++) {
33          for (i = 0; i < M; i++) {
34              arr[tid][i] = foo(tid, i);
35          }
36      }
37 }
(cuda-gdb)
```

The line where the address occurs is reported on line 34. That line contains a multi-indirection reference to input arr. You can examine the contents of the arr being referenced at offset tid by printing the address in arr[tid]:

```
(cuda-gdb) print arr[tid]
$1 = (@global *) 0x0
(cuda-gdb)
```

That does not work. A NULL memory address cannot be dereferenced. You can attempt to dereference that location inside the cuda-gdb debugging session to double-check the problem:

```
(cuda-gdb) print arr[tid]
Error: Failed to read global memory at 0x0 on device 0 sm 1 warp 0
(error)
(cuda-gdb)
```

Clearly that is invalid, which means that the contents of arr are either having an invalid value written to or not properly initialized. Looking back at the source code, you should notice there is no cudaMemcpy that actually fills the array d_matrix. Adding the following line before the kernel launch fixes this error.

```
cudaMemcpy(d_matrix, d_ptr, N * sizeof(int), cudaMemcpyHostToDevice);
```

The corrected version can be downloaded from wrox.com in debug-segfault.fixed.cu. You are still in the cuda-gdb debugging session, you can also examine the state of other threads on the GPU. Use the cuda command to get the current device, block, and thread, as follows:

```
(cuda-gdb) cuda device block thread
block (0,0,0), thread (0,0,0), device 0
(cuda-gdb)
```